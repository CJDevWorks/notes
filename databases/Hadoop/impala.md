Impala 
Impala is an open source SQL engine that offers interactive query processing on data stored in Apache Hadoop file formats. As opposed to SQL-on-Hadoop databases such as Hive that are used for long batch jobs, Impala enables interactive exploration and fine-tuning analytic queries by using its Massively Parallel Process (MPP) model. Impala avoids data movement and enables the users to interact with the data stored in HDFS via a SQL front-end rather than the traditional HDFS jobs.


History 
The Impala project was announced in October 2012 with the objective to provide a SQL interface and Business Intelligence tools for data scientists. Impala supports various HDFS file formats, however it is optimized for Parquet, a column-oriented file format which was announced in early 2013. Impala was accepted into the Apache incubator on December 2, 2015.


Concurrency Control 
Not Supported

Impala does not support any Concurrency control mechanism. The transactional nature of the HiveMetaStore (HMS), which receives updates on inserts and updates raises an error incase parallel inserts are made into the same table.


Data Model 
Relational

Impala is a massively parallel query engine which is not strongly coupled with the underlying storage layer. Currently, impala only supports a flat relational schema. They plan to add support for nested schemas with complex column types.


Indexes 
Not Supported

Impala does not support indexes. Although HIVE provides limited index capabilities, they are not leveraged by Impala. Since Impala is not a monolithic DBMS, Impala is often unaware of the data the shows up in the HDFS files. Hence it is not possible for the index to stay in sync with the base data.


Isolation Levels 
Read Uncommitted Read Committed

Impala supports both Read Committed and Read Uncommitted isolation levels.


Joins 
Nested Loop Join Hash Join Broadcast Join Shuffle Join

Impala provides a variety of Join Options. Impala does not provide a command to hint on the type of join to be executed incase of Nested Loop Joins and Hash Joins. Impala internally decied on the most suitable join mechanism for the query. However, it supports query hints for choosing between Broadcast and Shuffle joins.


Logging 
Not Supported

Since Impala does not support transactions and is suited for analytical queries, it does not support logging.


Query Compilation 
Code Generation JIT Compilation

Impala uses the LLVM engine to perform just in time (JIT) query compilation. It uses runtime code generation for specific versions of the function by which performance improvements of more than 5x are achieved.


Query Execution 
Tuple-at-a-Time Model

Query Interface 
Custom API SQL

Impala supports SQL as its query language. It provides a high dgree of compatibility with the Hive Query Language (HiveQL). Additionally it also provides an impala-shell interpreter which processes all the SQL commands supported by Impala along with a few shell-only commands which can be used for performance tuning.


Storage Architecture 
Disk-oriented

Impala can access data stored on HDFS in any of the Apache Hadoop file formats, including, Parquet, Text, Avro, RCFile and SequenceFile. It also supports compressed file formats in order to reduce the disk space and I/O volume, although such formats induce a CPU overhead to decompress the data.


Storage Model 
Custom

Impala does not provide its own storage engine but rather reads data from any of the underlying storage format. Nonetheless, when data is stored in Parquet, a binary columnar storage format, it displays significant performance improvement as it substantially reduces the I/O volume.


Stored Procedures 
Supported

Support for stored procedures in Impala was added from the 1.2 release. It now enables users to write UDFs in C++ or Java based Hive UDFs. C++ UDFs achieve a significant performance improvement over the Java written UDFs. Currently support for User Defined Table Functions (UDTF) has not been added.


System Architecture 
Shared-Nothing

Impala is a distributed, Massively Parallel Processing (MPP) query engine which uses a Shared-Nothing architecture. Impala consists of the following three major components 1. Impala Daemon - A daemon process runs on each data node to read and write data for the accepted queries and parallelizes the work across the cluster. It transmits the query results to the central coordinator node. 2. Impala Statestore - It is a daemon process which continously monitors the health status of the daemons on the datanodes in the cluster. When a datanode goes down, it ensures that no requests are made to an unreachable datanode. It provides robustness, load balancing and high availability. 3. Impala Catalog Service - It relays the metadata changes from SQL statements to all the Imapala Daemons. The catalog server ensures that if the metadata change occured via SQL queries issued through Impala.


Views 
Virtual Views

Imapala supports virtual views as lightweight logical constructs to act as query aliases. It does not support materialized views since data updates in the Hadoop Environment make it difficult to keep them up-to date.