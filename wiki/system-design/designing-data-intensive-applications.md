---
layout: wiki
title: Designing Data-Intensive Applications
last_updated: 2021-02-21
---
"The big ideas behind reliable, scalable, and maintainable systems."

Author: Martin Kleppmann [twitter](https://twitter.com/martinkl) [amazon](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321/ref=sr_1_1?dchild=1&keywords=Designing+Data-Intensive+Applications%3A+The+Big+Ideas+Behind+Reliable%2C+Scalable%2C+and+Maintainable+Systems&qid=1613920056&sr=8-1)

[![Book cover](/assets/2021/wiki/design-data-cover.jpg "Book cover")](/assets/2021/wiki/design-data-cover.jpg)

## Part 1: Foundations of Data Systems

Part 1 discusses aspects of data systems that apply when data is stored on a single machine.

### Chapter 1: Reliable, Scalable, and Maintainable Applications

The book discusses three concerns in software systems:

* **Reliability**. To work *correctly* even in the face of *adversity* (hardware/software faults, human errors);

  * A system that can cope with faults and anticipate them are called *fault-tolerant or resilient*
* **Scalability**. Reasonable ways of dealing with growth (data/traffic volume, complexity).

  * It is meaningless to say "X is scalable" or "Y doesn't scale". The load can be described by *load parameters* (if the system grows in this way, what will happen?). This  highly depends on system architecture, i.e.
    * for online systems, response time;
      * Percentiles are usually the best way to measure: p50, p95, p99, p999.
    * for batch processing, *throughput*, number of records we can process per second;
* **Maintainability**. Be able to work on it *productively* (system maintance and new features).

  * Majority of the cost of the software
  * Three design principles for software systems:

  1. Operability - easy for operations teams to keep the system running smoothly;
  2. Simplicity - easy for new engineers to understand the system;
  3. Evolvability - easy for engineers to make changes to the system in the future;

### Chapter 2: Data Models and Query Languages

Data models have a profound effect on systems, not only on how it is written but also on how *we think* about the problem that we are solving, i.e., Relational Models vs. Document model;

- Relational Versus Document Databases Today
  - Document data model pros: schema flexibility, a better performance due to locality and close to data structures used by the application;
  - Relational data model pros: better support for joins, and many-to-one and many-to-many relationships;
  - Data locality for queries
    - documents are usually stored as a single string. If the system needs to fetch all data from a doc, it provides a better data locality than the same data distributed/normalized over multiple tables
  - *Document databases:* use cases where data comes in self-contained docs and relationships between docs are rare;
  - *Graph databases*: use cases where data are usually related to other data
  - Document and graph databases usually don't enforce a schema (easier to adapt for new requirements, but the application still assumes that the data has a certain structure
    - schema explicit (enforced on write) or implicit (assume on reading)

## Chapter 3: Storage and Retrieval

A database needs to do two things: when you give it data, it should store it; and when you ask it again later, it should give it back to you.

To select and tune a storage engine to perform well for some kind of workload, you need to have a rough idea of what the storage engine is doing under the hood. (i.e., big difference between storage engines optimized for transactional workloads (OLTP) and those optimized for analytics (OLAP).

**Data Structures That Power Your Database**

Many database tables use a *log*, an append-only data file. (very efficient to append but O(n) to lookup). To speed this up, we need an index. Any index slow down writes (index must be updated every time data is written).

Let's says our data storage consists only of appending to a file, and you want to create an index based on a hash:

*Hash indexes*: in-memory hash map where every key is mapping to a byte offset in the data file;

* well suited for use cases where the value for each key is updated frequently. There are lots of writes, but not too many distinct keys.
* To reduce disk space, throw away duplicated keys in the log, keeping only the most recent update
* Considerations: File format: binary preferred to csv, Deleting records, Crash recovery, Partially written records: checksums, Concurrency control
  * **append-only logs** are good because:
    * appending and merging become sequentially (faster than random writes);
    * concurrency and crash recovery become simpler;
* Limitations:
  * Hash table must fit in memory. It could maintain on disk, but super painful and slow.
  * Range queries are not efficient. Looking for sequences requires looking up every key.

*B-Trees*: standard index implementation in almost all relational databases, and many non-relational databases use them too,

* keep key-value pairs sorted by key, allowing efficient key-value lookup and ranged queries
* breaks the database into fixed blocks or pages (usually 4kb)
* the number of references to child pages in one page is called branching factor (i.e. the branching factory in the above image are 6).
* The algorithm ensures that the tree remains *balanced*, n keys always have depth O(log n).

[![B tree](/assets/2021/wiki/btree.png "B Tree")](/assets/2021/wiki/btree.png)

LSM-trees are typically faster for writes, B-tress are faster for reads.

OLTPs (transaction processing) has two schools of though:

1. **Log-structure school**, which only permits appending to files and deleting obsolete files but never update a file that has been written. (Cassandra, LSM-trees, Lucene)
2. Update-in-place school, which treats the disk as a set of fixed-size pages that can be overwritten. B trees are the bigger example of this (being used on all major relational DB)

## Chapter 4:  Encoding and Evolution

Evolvability: we should aim to build systems that make it easy to adapt to change. We should focus on encoding on the efficiency perspective and architectural options to evolve them (schemas).

Most of the changes require changes also to data in stores, two ways of coping with that:

- Relational databases: schemas assume all data conforms to one schema, which can be changed (via scheme migrations)
- Schema on read ('schemaless/document"): don't enforce a schema and can contain a mixture of anolder and newer format written in different times (versions of the app).

When a schema changes, we probably need also to change the application code. In large applications, this cannot happen instantaneously, on:

- Server-side applications: rolling upgrade (staged rollout), deploying this new app to few nodes at a time (to check if everything is correct);
  - No downtime in theory;
- Client-Side: user should update his applications;

We must assume that different nodes/clients are running different schemas. All data flowing in the system should be encoded in a way that provides backward compatibility (new code read old data) and forward (old code read new data)

So, newer and older versions of the code should coexist in a system, achievable by a guarantee of compatibility in both directions:

- Backwardcompatibility: new code can read data that was written by older code. (should be easy because new code knows the format of data)
- Forward compatibility: older code can read data written by newer code. (harder to achieve, requires old code to be able to ignore new data by new version and adapt to changes in the encoding)

**Formats to encoding data**

Programs usually works with two representations of data.

- In memory (cpu efficient): objects, arrays, structs, lists etc;
- When  you want to send it over the network (you need  to convert it to a sequence of bytes)

Translating between representations is called *encoding* (used in the book), *serialization* or *marshalling*; and the reverse is called *decoding*, *parsing*, *deserialization* or *unmarshalling*.

**Language-Specific formats**

Only use language-specific encoding for transient purposes because they have some issues:

- Encoding tied to a programming language (i.e. java serialization)
- To restore the data, the decoder needs to instantiate arbitrary classes (security issue)
- Not all language formats are efficient (i.e. java built in serialization)

**JSON, XML & Binary Variants**

Textual formats, "human-readable", but with some caveats:

- Ambiguity about numbers representation;
- Lack of support for binary strings (if you use base-64-encoded it will increase the data size by 33%
- Optional schema support for XML, JSON and no schema support for CSV.
- Use a lot of spaces comparing to bynary formats;

**Apache Thrift and Protocol Buffers***

Both are binary encoding libraries that requires a schema for any data encode, i.e. in Protocol Buffer:

```
message Person {
	required string user_name = 1;
	optional int64 favourite_number = 2;
	repeated string interests = 3;
}
```

They both come with a code generation tool, that produces classes (encode/decode) in many languages.

**Field tags and schema evolution**

Schema changes related to field names can be easily done if you maintain code tags (keeping forward compatibility), but changing datatypes of fields are risky (check details on framework docs).

*Apache Avro* is another option for binary encoding format. How it does schema evolution?

When an app wants to encode data, it does with whatever schema it knows (writer's schema).

When an app wants to decode some data, it's expected that the data is on some scheme (reader schema).

The idea of Avro is that reader/writer schema doesn't have to be the same; they only need to be compatible. Avro library resolves the difference and tries to translate the data. (in the Avro docs, there are more details of how this evolution works), but as an example:

[![Schema Migration](/assets/2021/wiki/avroSchemaConverstion.png "Avro migration")](/assets/2021/wiki/avroSchemaConverstion.png)

Forward/backward compatibility is possible but with some caveats, i.e. adding/removing fields that only have default values and changing the name of the field would require alias usage.

Compared with Protocol Buffers and Thrift, Avro is more friendly to dynamically generate schemas. In most cases, you can automatically generate reader/writer schemas (for protbuff and thrift you need to add tags manually).

** Models of Dataflow**

Different scenarios where data encodings are important:

- Through databases:  where the process writing to the database encodes the data and the process reading it decodes it;
- RPC and REST, where the client encodes a request, the server decodes the request and encodes a response, and the client finally decodes the response
- Async message passing (brokers or actors): msgs needs to be encoded by the sender and decoded by recipient.


## Part 2: Distributed Data

Part II discusses what happens if multiple machines are involved and storage and retrieval of data?

Reasons for distributing a database across multiple machines: scalability, fault tolerance/high availability, latency (across multiple locations).

*Scaling to higher load:*
- Shared-memory/shared disk architecture (vertical scaling or scaling up): all components can be treated a single machine (cons: cost grow faster than linear, 2x CPUs/memory/disk costs usually more than 2x price; limited fault tolerance)
- Share nothing architectures (horizontal scaling or scaling out): each machine is an independent node, coordination between nodes is done at the software level. (cons: incurs additional complexity for applications and sometimes limits the expressiveness of data models).
  
Two ways of distributing data across multiple nodes:

- Replication: keeping a copy of the data on various nodes (provides redundancy);
- Partitioning: split a big dataset into smaller ones called partitions, allowing different partitions being assigned to different nodes (sharding).


### Chapter 5: Replication

Replication means keeping a copy of the same data on multiple machines connected to a network. Why?

- Keep data geographically close to users and reduce latency.
- Allow the system to continue even if parts have failed, increasing availability.
- Scale the number of machines that can serve read queries, increase read throughput.

And replication can serve several purposes:

- High availability: keeping the system running, even when one machine (or several) goes down;
- Disconnected Operation: Allowing an application to continue working when there is a network interruption
- Latency: placing data geographically close to the users so that users can interact with it faster;
- Scalability: being able to handle a higher volume of reads than a single machine could handle by performing reads on replicas


In this chapter, the author assumes that the dataset fits on a single machine. Chap 6 will discuss if they don't (partitioning/sharding).

All the challenges related to replication lies in handling changes to the replicated data. It is a tricky problem because it involves thinking about concurrency, all the things that can go wrong when a node is down, and its consequences.

 Some popular algorithms for this: 
 - Single-leader replication: the client sends all the writes to a single node (the leader), which sends a stream of data change events to the other replicas (followers). Reads can be performed on any replica, but reads from followers might be stale; it is popular because it's relatively easy to understand and there is no conflict resolution to worry about;

- Multi-leader replication: clients send each write to one of several leader nodes, any of which can accept writes. The leaders send streams of data to change events to each other and any follower nodes;
  
- Leaderless replication: the client sends each writes to several nodes and read data from several nodes in parallel to detect and correct nodes with stale data;
 
 Both can be more robust in the presence of faulty nodes, network interruptions, and latency spikes. Still, there is a cost of being harder to reason about and provide only a weak consistency guarantee.
 
 Almost all distributed databases use one of these approaches.

#### Leaders and followers

Each node that stores a copy of the database is called a replica. With multiple replicas, the challenge is: How do we ensure that all data ends up to all replica? (to avoid inconsistency)

The most common solution for this is leader-based replication (also called active/passive or master-slave replication).

This is the mode used by most relational databases and consists of designing one replica as the leader, all client requests go through it, and the leader writes the data on local storage.

Then, the leader sends the data to the followers as part of the replication log or change stream. (they must apply the changes in the same order as the leader)

Then clients can query any node for reads. Writes must go only via leader.

#### Synchronous Versus Asynchronous Replication

The client sends an update request to the leader. At some point the leader will forward this change to the followers, and only then notify the client that the update was sucessful.

- Synchronous: leader waits for confirmation from followers before notifying the client. No guarantee of how long this would take.

Pro: followers are always updated and consistent with the leader. 

Con: If any follower doesn't respond, the write cannot be processed, and the leader must block all writes until the replica is available again;

Impractical for all followers to be synchronous. In practice, usually, one is synchronous. If it becomes unresponsive, an asynchronous follower then becomes synchronous. It is called semi-synchronous replication.

- Asynchronous: leader send the data change but doesn't wait for confirmation before notifying the client.
Pro: Leaders can continue processing writes even if all of the followers have fallen behind;

Con: If the leader fails and is not recoverable, any writes that have not yet been replicated to followers are lost. Writes are not guaranteed to be durable even if confirmed to the client.

There are cases where followers can lag behind the leader by several minutes, i.e., network issues or recovering from a failure.

#### Setting up new followers

From time to time, you need to set up new followers (i.e., increase replicas, replace a failure node). How to ensure that new follower has an updated copy of leader's data? Here is a suggested process:

- Take a consistent snapshot of the leader's database at some point in time without taking a lock on the entire database.
- Copy snapshot to the new follower.
- The Follower connects to the leader and requests all data changes since the snapshot. (via replicated log)
- When the follower has processed all the backlog, we say that it has caught up. Now it can continue to process data changes from the leader as they happen.

Remember: copy data from one node to another is not sufficient because clients keep writing to the database. If we lock the leader for this copy, we will lose HA.

#### Handling node outages

Any node can go down anytime (fault, maintenance). And we should be able to restart a node without downtime, keeping the system as a whole running, keeping the impact of the node outage as small as possible. 

But how to achieve high availability with leader-based replication?

- Follower failure: Catch-up recovery

In the case of a fault, the follower can recover because it keeps a log of data changes received from the leader, knowing the last transaction processed before failure from the log. So, it can request from the leader all data changes that occurred since the failure.

- Leader Failure: Failover

Trickier, because One of the followers needs to be promoted to be the new leader, clients need to be reconfigured to send their writes to the new leader followers need to start consuming data changes from the new leader.

Failover is fraught with things that can go wrong:

If asynchronous, the new leader may not have received all of the old leader's writes before it failed. If the former leader rejoins, what happens to the writes? Commonly, they are discarded, violating the client's durability expectations.
- Discarding writes are especially dangerous if other storage systems outside the database need to be coordinated with the database contents.
- In specific fault scenarios, two nodes might believe they are leaders, split-brain situation. If both accept writes, and there is no process to resolve conflicts, data is likely to be lost or corrupted.
- What is the right timeout before the leader is declared dead? A longer timeout means a longer time to recover, if the timeout is too short, there could be unnecessary failovers. A temporary load spike could raise response time above the threshold; an unnecessary failover would make the situation worse, not better.
  
These node failures, unreliable networks, and trade-offs around replica consistency, durability, availability, and latency are fundamental problems in distributed systems.


#### Implementation of replication logs

How does leader-based replication work under the hood? Here are some of the approaches:

##### Statement-based replication: 
 
Leader logs write every write request (statement) that it executes and sends that statement log to followers. The leader sends all INSERT, UPDATE or DELETE statements to followers, and the follower parses and executes SQL statements as if it had been received from a client.

Problems with this approach:

- Any statement with a nondeterministic function like NOW() or RAND() - will generate a different value on each replica.
- If statements use autoincrementing column or depend on the existing data in the database, they must execute them in the same order on each replica. Limiting when there are multiple concurrently executing transactions.
- Statements with side-effects (triggers, stored procs, user-defined functions) may result in different side effects on each replica.

It's possible to work around those issues. However, there are so many edge cases, and usually, other replication methods are preferred.

##### Write-ahead log (WAL) shipping

Used by most of the storage engines, every write is appended to a log. Usually, if it's a log-structured (SStables, LSM-Trees) the log is the main storage place. In B-Tree, which overwrites individual blocks, every modification is first written to a write-ahead log to restore the index to a consistent state after a crash.

The log is an append-only sequence of bytes containing all writes to the database. We can use the exact same leader log to build a replica on another node, building the same data structure as found on the leader.

Con: Log describes data on a very low level. WAL contains details of which bytes were changed in which disk blocks. Therefore replication is closely coupled to the storage engine if the DB changes the storage format, not typically possible to run different versions of the database software on the leader and followers.

It can have a big operational impact. If the replication protocol allows the follower to use a newer software version than the leader, you can perform a zero-downtime upgrade of the software. If the replication protocol does not allow this version mismatch, as often happens with WAL, upgrades require downtime.

##### Logical (row-based) log replciation
Use different log formats for replication and storage engine. Allows replication log to be decoupled from the storage engine internals. This is a logical log, distinguished from the physical data representation.

Logical log for relational DB is a sequence of records describing write to tables:

- Inserted row: log contains new values of all columns.
- Deleted row: contains info to identify the deleted log, typically PK.
- Updated row: identify update row & contains new values of columns.
It can be kept backward compatible, allowing leader and follower to run different versions of the software. Easier for external applications to parse.

##### Trigger-based replication
If you need more flexibility, i.e. only want to replicate the subset of the data, you may need to move the replication up to the application layer.

Triggers let you register custom application code that is automatically executed when a data change occurs in a database system. The trigger then logs this change into a separate table, which an external process can then read.

Con: Trigger typically has a great overhead than other replication methods and is more prone to bugs and limitations than the built-in database replication. However, it can be useful due to its flexibility.

#### Problems with replication lag

Node failures are just one reason for wanting replication. Other potential ones are scalability and latency. Leader-based replication requires all writes go through a single node, but read-only queries can go to any replica.
This is a read-scaling architecture, you can increase the capacity for serving read-only requests simply by adding more followers, but this only really works on asynchronous replication.

With the async approach, a follower may fall behind, leading to inconsistencies in the database (eventual consistency). This is called replication lag and could be a fraction of a second or several seconds/minutes, so some problems may arise. How to solve them?

##### Read-after-write consistency: users should always see data that they submitted themselves.

How to implement it?

- When reading something that the user may have modified, read it from the leader;
- Track the time of the last update, for one minute after the last update, make all reads from the leader;
- Client can remember the timestamp of the most recent write, and the system can use it to ensure that we are reading from a replica updated.
If your replicas are distributed across multiple data centers, any request needs to be routed to the data center containing the leader.

##### Monotonic reads: after users have seen the data at one point in time, they shouldn't later see the data from some earlier point in time

We should make sure that each user always makes their reads from the same replica. The replica can be chosen based on a hash of the user ID. If the replica fails, the user's queries will need to be rerouted to another replica.

##### Consistent prefix reads

Users should see the data in a state that makes casual sense: for example, seeing a question and its reply in the correct order. This is a particular problem in partitioned (sharded) databases as there is no global ordering of writes. 

A solution is to make sure any writes casually related to each other are written in the same partition.

##### Solutions for replication lag
Transactions exist, so there is a way for a database to provide stronger guarantees so that the application can be simpler.



#### Multi-Leader replication

Leader-based replication has one major downside: there is only one leader, and all writers must go through it.

A natural extension is to allow more than one node to accept writes (multi-leader, master-master, or active/active replication) where each leader simultaneously acts as a follower to the other leaders. 

It rarely makes sense to use a multi-leader set up within a single datacenter, but let's discuss some use cases:

##### Multi-datacenter operation

One leader in each datacenter. Inside the same datacenter, regular leader-follower replication is used. Between datacenters, each datacenter leader replicates its changes to the leaders in other datacenters.

Compared to a single-leader replication model deployed in multi-datacenters

- Performance. With single-leader, every write must go across the internet to wherever the leader is, adding significant latency. In multi-leader, every write is processed in the local datacenter and replicated asynchronously to other datacenters. The network delay is hidden from users, and perceived performance may be better.
- Tolerance of datacenter outages. In single-leader, if the datacenter with the leader fails, failover can promote a follower in another datacenter. In multi-leader, each datacenter can continue operating independently from others.
- Tolerance of network problems. Single-leader is very sensitive to problems in this inter-datacenter link as writes are made synchronously over this link. Multi-leader with asynchronous replication can tolerate network problems better.


Some relational DBs implement Multi-leader replication, but it's common to fall on subtle configuration pitfalls, i.e., autoincrementing keys, triggers, and integrity constraints can be problematic. 

Multi-leader replication is often considered dangerous territory and avoided if possible.


Other examples of this type of operation are on clients with the offline operation (i.e. calendar app) and also collaborative editing (i.e google docs)


##### Handling write conflicts

The biggest problem with multi-leader replication is when conflict resolution is required. This problem doesn't happen for single-leader databases because the conflict detection happens synchronously; only one writer can write each time.

But for multi-leader, if both writes are successfull, the conflict is only detected asynchronously later. Some ways to deal with it:

- Conflict avoidance: if all writes for a particular record go through the same leader, conflicts cannot occur.
Converging towards a consistent state, all replicas should converge for the same state when all changes are replicated. 
  
Some ways to achieve that is to give each write a unique ID (i.e. timestamp, UUID) and select the winner based on that, give some replica precedence (but can prone to data loss), merge the values, record the conflict and maybe prompt the user to fix it manually.


#### Multi-leader replication topologies

Describes the communication path along which writes are propagated from one node to another. It could be circular, star, all-to-all.

#### Leaderless replication

Any replica can directly accept writes from clients. This is used on some databases like Amazon's in-house Dynamo datastore. Riak, Cassandra and Voldemort follow the Dynamo style.

In a leaderless configuration, failover does not exist. Clients send the write to all replicas in parallel. Read requests are also sent to several nodes in parallel. The client may get different responses. Version numbers are used to determine which value is newer.

Eventually, all the data is copied to every replica. After an unavailable node come back online, it has two different mechanisms to catch up:

- Read repair. When a client detects any stale responses, write the newer value back to that replica.
- Anti-entropy process. There is a background process that constantly looks for differences in data between replicas and copies any missing data from one replica to the other. It does not copy writes in any particular order.

Dynamo-style databases are generally optimized for use cases that can tolerate eventual consistency. There are some quorums algorithms for reading and writing for cases where the database needs to determine if an operation happened before another or whether they happened concurrently.

### Chapter 6: Partitioning

