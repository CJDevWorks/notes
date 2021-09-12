TimescaleDB 
TimescaleDB is an open-source SQL database designed for scalable time-series data. It enables both high ingest rates and real-time analysis queries. It scales by automatically partitioning Hypertable (a single continuous table) into two-dimensional (time and space) proper-sized chunks. Inserts to recent time intervals can be parallelized by placing chunks across cluster or disks based on a specified partition key. Complex queries can be optimized by leveraging metadata of each chunk.


History 
TimescaleDB is in active development by a team of PhDs. It is implemented as a Postgres extension. A single-node version is open-sourced in April, 2017 and a clustered version is currently in private beta release.


Checkpoints 
Non-Blocking Fuzzy

It follows PostgreSQL.


Concurrency Control 
Multi-version Concurrency Control (MVCC) Two-Phase Locking (Deadlock Detection)

It supports transactions on a per-server basis. Like PostgreSQL, it uses MVCC and Serializable Snapshot Isolation (SSI). It also supports explicit locking with deadlock detection.


Data Model 
Relational

It follows PostgreSQL


Foreign Keys 
Supported

It follows PostgreSQL.


Indexes 
B+Tree Hash Table BitMap

It follows PostgreSQL, which has primary, secondary, derived, partial indexes. PostgreSQL supports B-tree, hash, GiST, SP-GiST, GIN, and BRIN indexes, and default is B-tree.


Isolation Levels 
Read Uncommitted Read Committed Serializable Repeatable Read

It follows PostgreSQL, which supports Read uncommitted, Read committed, Repeatable read, Serializable. Read Committed is the default. They are implemented with MVCC. Note that PostgreSQL's Read Uncommitted is in fact Read Committed.


Joins 
Nested Loop Join Hash Join Sort-Merge Join Semi Join

It follows PostgreSQL.


Logging 
Logical Logging Physical Logging

It follows PostgreSQL.


Query Compilation 
Not Supported

Not Supported


Query Execution 
Tuple-at-a-Time Model

Query Interface 
SQL PL/SQL PromQL

Since TimescaleDB is based on Postgres, it supports Postgres' SQL and PL/pgSQL interfaces. They also provide support for PromQL through a Prometheus adapter.


Storage Architecture 
Disk-oriented

It follows PostgreSQL


Storage Model 
N-ary Storage Model (Row/Record)

It follows PostgreSQL


Stored Procedures 
Supported

It follows PostgreSQL.


System Architecture 
Shared-Everything

Like Postgres, TimeScale is a shared-everything DBMS. Each table is partitioned across all space and time intervals.


Views 
Virtual Views Materialized Views

It follows PostgreSQL.