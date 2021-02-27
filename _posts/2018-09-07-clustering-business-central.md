---
layout: post
title:  "Clustering on Business Central 7 series: the missing manual"
permalink: /:year/:month/:day/:title:output_ext
date:   2018-09-28 00:00:00 -0500
---
One of our major goals in 7+ series of Business Central is to gradually move towards a cloud-ready environment. (Porcelli and I will talk about this on next [Oracle Code One](https://oracle.rainfocus.com/widget/oracle/oow18/catalogcodeone18?search=ignatowicz)).

In that direction, in 7.0 we did a major rewrite of BC clustering technology, moving away from Zookeeper and Helix in order to simplify the setup and take advantage of provided infrastructure, especially in a containerized environment like OpenShift.

This post gives a quick overview of the new Business Central cluster setup and also explains some implementation details for those who would like to go more in depth.

## New Cluster Setup

Before diving in some details, let’s have a quick overview and do a basic hello world in the new clustered setup of business central.

### Cluster Overview

The new Business Central cluster has three major components. A Shared File System Infrastructure to store our git filesystem (i.e. a Network File System), an indexing engine (used i.e. for listing and searching for assets) and a JMS based messaging system (used to share cluster messages i.e. NIO2 WatchEvents). In this post, we will explore storage and messaging aspects. Indexing subsystem will be a topic of a future blog post.

[![Cluster Architecture](/assets/2018/cluster.jpg "Cluster Architecture")](/assets/2018/cluster.jpg)

The old cluster setup was based on Zookeeper and Helix (for Global Lock and Intra Cluster Message). This setup is indeed powerful but the trade-off was an extra burden of setup and maintenance complexity on our users. Our goal for 7.0 was to provide the same functionality in a simpler, and yet container friendly architecture. Before diving into the details of this architecture let’s do a quick hello world?

#### Basic Cluster Setup

Let’s create basic configuration of Artemis for messaging and two business central instances running on the same machine.

For messaging, the first step is to download [Apache Artemis 2.3.0](https://archive.apache.org/dist/activemq/activemq-artemis/2.3.0/apache-artemis-2.3.0-bin.zip). After downloading it, unzip it and create a broker:

`./bin/artemis create --user admin --password admin  mybroker`

Inside mybroker/bin directory run this broker with:

`./artemis run`

Please note that Artemis itself could be also configured in a clustered high availability mode. Take a look at [artemis docs](https://activemq.apache.org/artemis/docs/1.0.0/ha.html).

Let’s configure wildfly instances. For this demo, we will use standalone mode but you can also use domain mode if that fits your use case.

[![Basic Setup](/assets/2018/basicsetup.jpg "Cluster Architecture")](/assets/2018/basicsetup.jpg)

On **wildfly1**, Copy business central war into standalone directory of Wildfly At the time of writing we support Wildfly 11.0.0.Final. Support for Wildfly 14 is on the way) and run it with:

`./standalone.sh -c standalone-full.xml -Dorg.uberfire.nio.git.dir=/tmp/niogit -Dappformer-jms-connection-mode=REMOTE  -Dappformer-jms-url="tcp://127.0.0.1:61616?ha=true&retryInterval=1000&retryIntervalMultiplier=1.0&reconnectAttempts=-1" -Dappformer-jms-username=admin -Dappformer-jms-password=admin -b 127.0.0.1`

Let’s give some basic details about the parameters:

appformer-jms-connection-mode: we have two connection modes for messaging in the cluster, REMOTE (to connect to a remote message provider — this is our case) and JNDI (to use messaging provider in the container itself).

* **appformer-jms-url:** the remote message provider URL
* **appformer-jms-username:** the remote message provider username
* **appformer-jms-password:** the remote message provider username

On the **wildfly2**, also copy business central war on standalone directory of Wildfly:

`./standalone.sh -c standalone-full.xml -Dorg.uberfire.nio.git.dir=/tmp/niogit -Dappformer-jms-connection-mode=REMOTE  -Dappformer-jms-url="tcp://127.0.0.1:61616?ha=true&retryInterval=1000&retryIntervalMultiplier=1.0&reconnectAttempts=-1" -Dappformer-jms-username=admin -Dappformer-jms-password=admin -b 127.0.0.1 -Djboss.socket.binding.port-offset=2000 -Dorg.uberfire.nio.git.daemon.port=9419 -Dorg.uberfire.nio.git.ssh.port=8002`

I have to to change some default ports of business central because we are running two instances on the same machine, but the most import thing that I would like to highlight is that **both wildfly instances** points to the same nio git dir (org.uberfire.nio.git.dir). This is a central requirement for business central clustering.

How can I check if my cluster is ready? Open business central on both nodes, import Mortgages project from samples and open the same file on both nodes (i.e. Dummy rule.drl). As soon as you start editing the file on one node it will lock the file on the other node. Locking a file is one of the cluster messages use case that we will explore on details in the next session.

[![Cluster Hello World](/assets/2018/chw.jpg "Cluster Hello World")](/assets/2018/chw.jpg)

Simpler than the 6.x version isn’t it? But how does this work under the hood? How do we keep the niogit state synced? How do we trigger messages in this new infrastructure?


## Architecture and Implementation

That is always my favorite part. Let’s understand how we implemented this solution. In order to achieve this let’s split this into two areas: messaging and global locking.

### Messaging

The new ClusterService interface could have multiple implementations and is responsible for connecting with message systems and also consume and broadcast messages.


<script src="https://gist.github.com/ederign/00b190223fd927d0e5d8369f74230673.js"></script>


For now, we only have one implementation of this interface that provides support for JMS ([ClusterJMSService.java](https://github.com/kiegroup/appformer/blob/ae323c023e1fab4a45fba3bf2e7f7c5f20987b8e/uberfire-commons/src/main/java/org/uberfire/commons/cluster/ClusterJMSService.java)). But where is this service used?

Our backend provides a GIT java NIO2 implementation ([uberfire-nio2-jgit](https://github.com/kiegroup/appformer/tree/master/uberfire-nio2-backport/uberfire-nio2-impls/uberfire-nio2-jgit)). Following the NIO2 implementation, our filesystem provides a [WatchService](https://docs.oracle.com/javase/7/docs/api/java/nio/file/WatchService.html) implementation and each filesystem event triggers specific WatchEvent.Kind<T>.

The responsibility of Business Central foundation platforms to extend this model to a cluster environment. In general, a File System change in Business Central should send this event via cluster messaging and regenerate it on each node.

The beautiful part of that solution, and maybe this can help you to understand the guidelines of how foundation team builds Business Central platform, is that from developer’s perspective when triggering or consuming watch events he doesn’t need to worry if he is running on a single instance or in a cluster environment.

*(Please don’t expect that this Watch Service event distribution works on cluster environment for regular NIO2 implementations. This is not the default NIO2 behavior and afaik we are the only NIO2 implementation doing this).*

The WatchService and WatchService events will work transparently because we are following the same NIO2 programming model and we do all the cluster magic behind the scenes. (We took the same approach on [CDI Events distribution](https://medium.com/ederign/transparent-cdi-events-distribution-in-a-cluster-environment-via-metaprogramming-4c57914df0d6)).

Pretty cool isn’t it? 😗

So every time that we do an FS operation we publish the regular watch events for same instance nodes and if the Business Central is on a cluster we trigger this message on cluster service:


<script src="https://gist.github.com/ederign/9f6b7419c5fc13cabaf0d9cdce191919.js"></script>


For each FS, we also create some consumer for the cluster messages. In that case, as soon as we receive a cluster message that contains a watch event, we process it and retrigger in the correct file system:


<script src="https://gist.github.com/ederign/5a3e4b38961ef377dd25813c464d9f32.js"></script>


But how does this work from developer’s perspective? Let’s take a look on the client side lock mechanism that we saw in the hello world.


<script src="https://gist.github.com/ederign/c1598552b157e86a4be576f2815b8c7f.js"></script>


This code follows the NIO2 watch service spec but also receives WatchService messages generated on the other nodes in a transparent way. ;)


## Locking

The second problem that we have to solve is locking. Basically, in a single instance environment, we avoid multiple threads changing the file system state concurrently (in our case, do a commit) by having a ReentrantLock for [each filesystem](https://github.com/kiegroup/appformer/blob/b92f6b5479b8539e6d902e6b58ec3da7c6322fc9/uberfire-nio2-backport/uberfire-nio2-impls/uberfire-nio2-jgit/src/main/java/org/uberfire/java/nio/fs/jgit/JGitFileSystemImpl.java#L78). But how do we approach locking when we have multiple instances of the same filesystem? Basically, how to ‘share’ a lock among all nodes of our cluster?

[FileChannel lock](https://docs.oracle.com/javase/7/docs/api/java/nio/channels/FileChannel.html#lock()) to the rescue!

Do you remember that all nodes share the same network filesystem? In order to have this lock, for each filesystem, we create a physical lock. Basically, we create a simple file in the root of git repository (we use bare git repositories) and before doing any write, a node request for java FileChannel APIs acquires a lock for this file.


<script src="https://gist.github.com/ederign/8973c8b8553a4144dd111ba64f873feb.js"></script>




In that way, we have two layers of lock for each filesystem. The physical lock that guarantees that just one instance writes on the FS at a specific time and also the ReentrantLock, that prevents concurrency access to the same FS.

With this simple and elegant solution and using native Java APIs and a Shared File System, we are able to reproduce locking functionality of zookeeper and helix in clustered business central


## Take Aways

In the end, I was really happy when we figured out this simple and elegant solution for our cluster stack. With this invention, our team was able to simplify the setup and take advantage of provided infrastructure, especially in a containerised environment like OpenShift.

Although this architectural approach might have some limitation (probably we are not able to scale to hundreds or thousands of nodes — but we already know how to fix this), applying this solution, we were able to remove the extra burden on Helix/Zookeeper setup and maintenance complexity from our users, providing the same functionality in a simpler and yet container friendly architecture.

Thanks for reading! I hope this could be useful for you — or just fun to read ;) ! 💖
