---
layout: wiki
title: Designing Data-Intensive Applications
last_updated: 2021-02-21
---
"The big ideas behind reliable, scalable, and maintainable systems."

Author: Martin Kleppmann [twitter](https://twitter.com/martinkl) [amazon](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321/ref=sr_1_1?dchild=1&keywords=Designing+Data-Intensive+Applications%3A+The+Big+Ideas+Behind+Reliable%2C+Scalable%2C+and+Maintainable+Systems&qid=1613920056&sr=8-1)

[![Book cover](/assets/2021/wiki/design-data-cover.jpg "Book cover")](/assets/2021/wiki/design-data-cover.jpg)

## Part 1: Foundations of Data Systems

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

- Throughdatabases:  where the process writing to the database encodes the data and the process reading it decodes it;
- RPC and REST, where the client encodes a request, the server decodes the request and encodes a response, and the client finally decodes the response
- Async message passing (brokers or actors): msgs needs to be encoded by the sender and decoded by recipient.


## Part 2: Foundations of Data Systems

### Chapter X: TBD
