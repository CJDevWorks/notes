ClickHouse 
CilckHouse is an open-source column-oriented OLAP DBMS. It is designed to provide linear scalability of queries.


History 
ClickHouse is developed by a Russian company called Yandex. It is designed for multiple projects within Yandex. Yandex needed a DBMS to analyze large amounts of data, thus they began to develop their own column-oriented DBMS. The prototype of ClickHouse appeared in 2009 and it was released to open-source in 2016.


Compression 
Dictionary Encoding Delta Encoding Naïve (Page-Level)

In addition to general-purpose encoding with LZ4 (default) or Zstd, ClickHouse supports dictionary encoding via LowCardinality data type, as well as delta, double-delta and Gorilla encodings via column codecs.


Concurrency Control
Not Supported

ClickHouse does not support multi-statement transactions.


Data Model 
Relational

ClickHouse uses the relational database model.


Foreign Keys
Not Supported

ClickHouse does not support foreign keys.


Indexes 
Log-Structured Merge Tree

ClickHouse supports primary key indexes. The indexing mechanism is called a sparse index. In the MergeTree, data are sorted by primary key lexicographically in each part. Then ClickHouse selects some marks for every Nth row, where N is chosen adaptively by default. Together these marks serve as a sparse index, which allows efficient range queries.


Joins 
Hash Join

ClickHouse uses hash join by default, which is done by placing the right part of data in a hash table in memory. If there's not enough memory for hash join it falls back to merge join.


Logging 
Physical Logging

ClickHouse replicates its data on multiple nodes and monitors data synchronicity on replicas. It recovers after failures by syncing data from other replica nodes.


Parallel Execution 
Intra-Operator (Horizontal) Inter-Operator (Vertical)

ClickHouse utilizes half cores for single-node queries and one replica of each shard for distributed queries by default. It could be tuned to utilize only one core, all cores of the whole cluster or anything in between.


Query Compilation 
Code Generation

ClickHouse supports runtime code generation. The code is generated for every kind of query on the fly, removing all indirection and dynamic dispatch. Runtime code generation can be better when it fuses many operations together and fully utilizes CPU execution units.


Query Execution 
Vectorized Model

Query Interface 
Custom API SQL HTTP / REST Command-line / Shell

ClickHouses provides two types of parsers: a full SQL parser and a data format parser. It uses SQL parser for all types of queries and the data format parser only for INSERT queries. Beyond the query language, it provides multiple user interfaces, including HTTP interface, JDBC driver, TCP interface, command-line client, etc.


Storage Architecture
Disk-oriented In-Memory Hybrid

ClickHouse has multiple types of table engines. The type of the table engine determines where the data is stored, concurrent level, whether indexes are supported and some other properties. Key table engine family for production use is a MergeTree that allows for resilient storage of large volumes of data and supports replication. There's also a Log family for lightweight storage of temporary data and Distributed engine for querying a cluster.


Storage Model 
Decomposition Storage Model (Columnar)

ClickHouse is a column-oriented DBMS and it stores data by columns.


Storage Organization
Indexed Sequential Access Method (ISAM) Sorted Files

Stored Procedures 
Not Supported

Currently, stored procedures and UDF are listed as open issues in ClickHouse.


System Architecture 
Shared-Nothing

ClickHouse system in a distributed setup is a cluster of shards. It uses asynchronous multimaster replication and there is no single point of contention across the system.


Views 
Virtual Views Materialized Views

ClickHouse supports both virtual views and materialized views. The materialized views store data transformed by corresponding SELECT query. The SELECT query can contain DISTINCT, GROUP BY, ORDER BY, LIMIT, etc.