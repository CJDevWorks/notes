Cassandra 
Apache Cassandra is a free and open source NoSQL distributed database management system. It provides high availability, high scalability, and fault tolerance, even while running on commodity hardware. Cassandra has no single-point of failure, and is well-suited for clusters spanning multiple datacenter. Cassandra is decentralized and master-less. Therefore, data in a Cassandra cluster is distributed/partitioned across multiple nodes in the cluster. It provides fault tolerance by asynchronously replicating data across different nodes. Thus, Cassandra is immune to even whole data centers going down. One salient feature of Cassandra is it’s ability to scale linearly in both read and write throughput as the number of nodes grows.


History 
Cassandra was started as a project at Facebook, and was later open-sourced in 2008 as a Google Code project. It finally became an Apache Project in 2009-2010. The database has been named after the Greek mythological prophet Cassandra.


Checkpoints 
Non-Blocking Consistent Blocking Fuzzy

Snapshots/Checkpoints in Cassandra can be taken by using the nodetool command. By default, this command takes per-node snapshots, but can be used to take global snapshots by using a parallel ssh utility like pssh. Automatic incremental backups are disabled by default.


Concurrency Control 
Two-Phase Locking (Deadlock Prevention) Optimistic Concurrency Control (OCC)

Cassandra does not support RDBMS ACID transactions spanning multiple rows/tables. It also does not roll back when a write succeeds on one replica, but fails on other replicas. As far as concurrent reads and writes are concerned, Cassandra simply performs an isolated/atomic replacement of rows within mem-tables (the in-memory structure where all writes are buffered). These are implemented using Optimistic Concurrency Control. However, under high contention on a single partition, Cassandra switches to Pessimistic Concurrency Control to counter the (potentially) high abort rate. Cassandra uses per-tuple locks when it switches to Pessimistic Concurrency Control. It thus has a hybrid of Optimistic Concurrency Control and Pessimistic Concurrency Control.


Data Model 
Column Family Key/Value

Cassandra’s data model revolves around efficiently storing and retrieving key-value pairs. Each row is identified by a unique row key, and has key-value pairs for the columns (identified by name, value, and timestamp) within that row. Rows are grouped together to form “column families”. Column families are synonymous to tables in a relational database management system. In fact, since CQL 3, column families are also called tables. The first component of a table’s primary key is called the “partition key”. Since Cassandra partitions tables across multiple nodes, the rows within a cluster can be conveniently clustered by the remaining columns. Thus, a table in Cassandra can be considered to be a distributed multi-dimensional map. One interesting feature of Cassandra is that not all rows within a table need to have values for all columns. Furthermore, columns can be added to any number of rows within a table (unlike a relational database where each row must have values for all columns, and adding a new column results in a new column for all rows).


Indexes
Skip List Hash Table BitMap

Cassandra does not use one single type of index clustered on the Primary Key. Cassandra first uses a partitioner to map the key to a node in the cluster. Then it uses bloom filters to exclude some of the SSTables. This is followed by passing the key through a partition index per SSTable. It then goes through a compression index, and finally, Cassandra searches for the key within the sorted keys present in the SSTable. Furthermore, rows within a partition can be indexed, when the partition is above a certain size. Thus, there is no one right answer as to which index is used by Cassandra. All of the above mentioned data structures are either implemented as Concurrent Hash Maps, Concurrent Skip Lists, or Bit-Maps.


Isolation Levels 
Serializable

Although Cassandra does not offer RDBMS-styled ACID transactions, it does offer “light-weight transactions” on a per-row basis that are implemented as simple “compare-and-set” operations through Paxos. In all cases, there is only a single lock to acquire, and hence deadlock is not an issue in Cassandra. Moreover, since there are no multi-row transactions, the light-weight transactions that Cassandra does offer, offer Serializable Isolation Level.


Joins
Not Supported

Logging
Logical Logging Physical Logging Physiological Logging

Query Execution
Tuple-at-a-Time Model

Query Interface 
Custom API

Cassandra has its own client interface, called the Cassandra Query Language (CQL), which closely resembles SQL. It is designed to be a simple client interface that hides and abstracts away all the complexities of Cassandra. Client drivers are present for Java (JDBC), Python (DBAPI2), Node.JS (Helenus), Go (gocql) and C++, and use the Cassandra Binary Protocol (wire protocol) to communicate with Cassandra.


Storage Architecture 
Disk-oriented

Cassandra is a purely disk-based database system. However, since its storage structured is similar to a log structured merge tree, it may buffer some data in a memory buffer (until it has enough data to perform a log write) before flushing it out to disk.


Storage Model
N-ary Storage Model (Row/Record)

Stored Procedures 
Not Supported

Cassandra doesn’t have stored procedures. Instead, developers are expected to write their business logic in application level code, and communicate with Cassandra using a client driver to read and write data.


System Architecture 
Shared-Nothing

Cassandra has a shared-nothing architecture. Since data is partitioned across several nodes, each partition is responsible for all compute related to data on its own private shard. However, this partitioning of data across nodes in a cluster can lead to a single point of failure. Cassandra counters this by making replicas of the data.


Views
Not Supported