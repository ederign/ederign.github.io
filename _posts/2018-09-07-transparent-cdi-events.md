---
layout: post
title:  "Transparent CDI Events Distribution in a Cluster Environment via Metaprogramming"
permalink: /:year/:month/:day/:title:output_ext
date:   2018-09-07 00:00:00 -0500
fav: true
---
In my opinion, one of the great features of the JavaEE/Jakarta EE programming model is the  CDI event mechanism.

But how this mechanism works in a cloud environment?  Have you ever wondered what you can achieve if you are able to fire a CDI event on one machine and observe it on the other node? What if I tell you that we achieved this in almost a transparent way?

## Problem Statement

On Business Central (web tooling for Drools and jBPM projects) we make extensive use of the CDI programming model.

With Errai project we take the CDI programming model even further because Errai allows us to observe CDI events on the browser. So basically we have the same programming model working on client and backend of our application.

For instance, when we fire a [NewProjectEvent](https://github.com/kiegroup/appformer/blob/875f0efd9ea80ef9ad5fb104bb05ca81dcdf661e/uberfire-project/uberfire-project-api/src/main/java/org/guvnor/common/services/project/events/NewProjectEvent.java#L24) on the backend of the platform, the same event is triggered to all clients (browsers) connected (in order to quickly update the UI).

I'll talk more about this on other blog posts but we are gradually moving Business Central to a cloud-ready architecture. This movement gave us an interesting problem:

"Having the same event programming model on backend and frontend save us a lot of time and CDI proves himself as a great way to deal with events in a monolith. Is it possible to extend the same model to the cloud?  Can an event fired on one node be triggered to all other nodes and, via Errai CDI, to all connected clients in all nodes?"

## How

As I already mentioned, IMO one of the great features of the JavaEE/Jakarta EE programming model is the  CDI event mechanism. This model is one of the cleanest ways to decouple your applications.

However, this mechanism was designed to work in a single instance mode and doesn't fit well for clustered environments use case. Basically, there is no way to observes an event fired in another machine in the cluster, requiring to use some other event technology and event manual translation.

The main goal of this invention is to extend the  CDI event mechanism to a clustered environment, making easy and almost transparent for the users firing an event on one node and observes it on another node. But how?

### Metaprogramming to the rescue

First, let's create a new annotation called Clustered and let's add it for the events that we want to propagate on the cluster.

<script src="https://gist.github.com/ederign/31d2886f944394ea39f5d4800da41521.js"></script>

Now, we can add it for an event:

<script src="https://gist.github.com/ederign/160cc365a7f51a5cd786d65f75ffc400.js"></script>

Our users fires this event has a regular CDI event.

<script src="https://gist.github.com/ederign/f10476cd42f1248ebd5b8e2298fcae17.js"></script>

Behind the scenes, what this invention does:

* Observe all CDI events and check if a CDI event object type has @Clustered annotation [[check the code](https://github.com/kiegroup/appformer/blob/875f0efd9ea80ef9ad5fb104bb05ca81dcdf661e/uberfire-commons/src/main/java/org/uberfire/commons/cluster/events/ClusterEventObserver.java#L93)]:

<script src="https://gist.github.com/ederign/9623242e2c7057403cff80635f92ebf6.js"></script>

* If this event has @Clustered annotation, we serialised it and sent a serialised cluster message with all event data. (on Business Central we use AMQ/Artemis for this) [[check the code](https://github.com/kiegroup/appformer/blob/875f0efd9ea80ef9ad5fb104bb05ca81dcdf661e/uberfire-commons/src/main/java/org/uberfire/commons/cluster/events/ClusterEventObserver.java#L101)]:

<script src="https://gist.github.com/ederign/337966ec40879e710edb331c11da3bc2.js"></script>

In each other node, we receive this event, deserialise it and fire as a regular CDI event (reproducing it): [[check the code]](https://github.com/kiegroup/appformer/blob/875f0efd9ea80ef9ad5fb104bb05ca81dcdf661e/uberfire-commons/src/main/java/org/uberfire/commons/cluster/events/ClusterEventObserver.java#L77)

<script src="https://gist.github.com/ederign/a5c3ce09581d60832a2f0d6f57bd418d.js"></script>

So basically, what my invention do is to observe all CDI events and if a CDI event object type has @Clustered annotation, we sent a serialised cluster message with all event data, deserialise on other nodes and regenerate a new CDI event.

[![CDI Events](/assets/2018/cdievent.png "CDI Events")](/assets/2018/cdievent.jpg)

Using that invention doesn’t matter if the event was fired on the local instance or fired in other nodes because all CDI observables will receive the same event data, making the same CDI event programming model that works on a single instance works almost transparently on cloud environments.

## Pull Request

If you are curious about the full details, you can take a look on the full [PR](https://github.com/kiegroup/appformer/commit/875f0efd9ea80ef9ad5fb104bb05ca81dcdf661e) of this solution.


## Take Aways

In the end, I was really happy when I figure out this simple and elegant solution.

As I already mention with this invention our team are able to use the CDI programming model to distribute events in single node and in cluster environments, reducing the complexity of our codebase.

A future improvement would be to use the annotation processing framework in order to generate specific observers instead of observing [all cdi events](https://github.com/kiegroup/appformer/blob/875f0efd9ea80ef9ad5fb104bb05ca81dcdf661e/uberfire-commons/src/main/java/org/uberfire/commons/cluster/events/ClusterEventObserver.java#L93). This could be a good and fun contribution to our codebase and if you are interested ping me!

Thanks for reading! I hope this could be useful for you — or just fun to read ;) ! 💖
