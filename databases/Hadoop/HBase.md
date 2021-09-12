HBase 
HBase is an open source, distributed, non-relational, scalable big data store that runs on top of Hadoop Distributed Filesystem. Hbase is suitable for storing large quantities of data, but it lacks many of the features that relational database management systems usually have, such as column types, secondary indexes, advanced query languages, etc. HBase stores the data in rows and columns. A row is referenced by a row key, and columns are grouped into "column families". HBase is written in Java, and is supported by Apache Software Foundation.


History 
HBase was initially a project by the company Powerset, a San Francisco-based search and natural language company. Microsoft acquired Powerset in 2008.


Checkpoints 
Non-Blocking

HBase Snapshots allows the users to make checkpoints of a table with little impact on RegionServers. Creating snapshots does not block reads and writes, but for each table only one snapshot can be created at a time.


Concurrency Control 
Multi-version Concurrency Control (MVCC)

HBase guarantees ACID semantics per-row. HBase uses a form of Multiversion Concurrency Control (MVCC) to avoid row locks for read operations. Write operations still need to acquire row locks.


Data Model 
Column Family

An HBase table consists of rows and columns. Rows are referenced by row keys which are raw byte arrays and are sorted by row key. The sort is byte-ordered. Each row contains columns. A column's content is also an uninterpreted array of bytes. All columns belong to a column family.


Indexes 
B+Tree

For each table, HBase only provide an B+Tree like index on row keys. HBase does not natively support secondary indexes. Users can use filters for querying on non-rowkey columns. There are some techniques to create another table which can be used as a secondary index.


Isolation Levels 
Read Uncommitted Read Committed

HBase only provide "read committed" isolation level. Users can downgrade the isolation level to "read uncommitted" by modifying the source code.


Joins 
Not Supported

HBase does not support join operations. Users can implement joins in their application code.


Logging 
Logical Logging

HBase's write-ahead-log is named HLog.


Query Compilation
Not Supported

Query Execution 
Tuple-at-a-Time Model

Query Interface 
Custom API

HBase does not provide native support for SQL. Unlike RDBMS, HBase has four primary operations: Get, Put, Scan and Delete. It also has some DDL operations, e.g., Create. HBase provides a shell which users can fire queries from. Users can specify table name, column names and apply filters in their query. HBase also offers Java Client API and Thrift/REST API. Some third-party drivers are also available for other programming languages.


Storage Architecture 
Disk-oriented

HBase leverages HDFS as the backend storage. Currently HDFS is disk-oriented.


Storage Model 
Decomposition Storage Model (Columnar)

HBase is schema-less column-oriented datastore.


Stored Procedures 
Not Supported

Stored procedures are not directly supported in HBase. But users can use coprocessors to resemble store procedures.


System Architecture 
Shared-Disk

HBase is organized as a cluster of HBase nodes that complies with the master-slave architecture. There are two types of nodes: a master node, and one or more slave nodes called RegionServers. RegionServers serve data for reads and writes. An HBase Region is a subset of an HBase table that has a continuous range of sorted rowkeys. Region assignment and DDL operations are handled by the HBase Master. HBase is built on top of Hadoop File System, thereby making it shared-disk. The Hadoop DataNodes store the data that RegionServers are managing. The HDFS Zookeeper maintains the server status in the cluster.


Views 
Not Supported

HBase does not provide views. But users can write MapReduce programs to approximate views. Apache Phoenix, a SQL interface for HBase, provides support for views.