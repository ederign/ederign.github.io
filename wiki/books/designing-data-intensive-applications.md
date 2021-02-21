---
layout: wiki
title: Designing Data-Intensive Applications
last_updated: 2021-02-21
---
# Designing Data-Intensive Applications

"The big ideas behind reliable, scalable, and maintainable systems."

Author: Martin Kleppmann [twitter](https://twitter.com/martinkl)

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

### Chapter 3: Storage and Retrieval

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

### Chapter 4: TODO
