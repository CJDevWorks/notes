Greenplum 
Greenplum is an open-source data warehouse. It uses massive parallel processing to provide large-scale analytics on petabyte scale data. It uses the Orca cost-based Cascades-style framework query optimizer.


History 
Greenplum was founded in September 2003 by Luke Lonergan and Scott Yara. The company releases the database management system software based on PostgreSQL in 2005. The company is acquired by EMC in 2010, and its database management system is known as Pivotal Greenplum Database. The company became part of the Pivotal Software in 2012.


Checkpoints 
Non-Blocking Consistent

Greenplum performs checkpoint in the same way as Postgres.


Concurrency Control 
Multi-version Concurrency Control (MVCC)

Greenplum uses PostgreSQL MVCC as the concurrency control scheme for each database instances. Each transaction reads from a consistent snapshot that's not modified by any concurrent transactions. MVCC generally performs better than lock-based concurrency control in Greenplum because transactions performing read will not block transactions updating the table.


Data Model 
Relational

Greenplum is a relational database. It is implemented based on PostgreSQL


Foreign Keys 
Supported

Greenplum supports all features in SQL1992 standard, users can define foreign keys in Greenplum and it will be stored in the system catalog.


Indexes 
B+Tree BitMap

Greenplum supports PostgreSQL index type B-tree and Gist. B-tree index is the default index type as it fit with most common situations. Bitmap index is also supported in Greenplum to accelerate analytics queries in data warehouse applications and desicion support systems.


Isolation Levels 
Read Uncommitted Read Committed Serializable

Greenplum supports three isolation levels, read uncommitted, read committed and serializable. The default mode is read committed, which allows more concurrency than serializable. Requesting repeatable read in Greenplum will produce an error.


Joins 
Nested Loop Join Hash Join Sort-Merge Join Semi Join

Three types of join algorithms, nested loop join, hash join and sort-merge join are supported in Greenplum. According to the blog article for their optimizer, semi join type is also supported.


Logging 
Command Logging

Greenplum achieves fault tolerance for data tables via segment mirroring. Each table is divided into several segments, and each segment has two copies, primary and mirror, stored in different nodes. The primary and mirror perform the same operation and keeps the same data. For master nodes, they also do mirroring by storing transaction level logging in a stand-by node. DBAs are able to view the status of the database by checking the command logging.


Query Compilation 
JIT Compilation

Greenplum utilizes query compilation for predicate evaluation, tuple deform and primitive type functions, etc. It doesn't compile the execution engine into a push-based model. As it is mentioned in the Query Execution section, the execution model is volcano pull style.


Query Execution 
Vectorized Model

Query Interface 
SQL PL/SQL

Greenplum supports all features in SQL 1992 standard, most of the features in SQL 1999 standard and some features in SQL 2003 standard. Users interact with Greenplum in the same way as they interact with PostgreSQL. They can directly enter query statements in SQL clients such as psql to perform view, change and analyze in the database. The system also support PL/pgSQL, but features such as triggers, scrollable cursors and updatable cursors are not supported.


Storage Architecture
Disk-oriented

Greenplum takes the disk-oriented storage architecture from Postgres.


Storage Model 
Decomposition Storage Model (Columnar) N-ary Storage Model (Row/Record) Custom

Greenplum supports both the N-ary storage model and Decomposition storage model. Clients can specify the storage model options using WITH clause of the CREATE TABLE command. The default is row-oriented(N-ary) storage model.


Stored Procedures 
Not Supported

Greenplum does not support stored procedure


System Architecture 
Shared-Nothing

Greenplum uses massive parallel processing architecture to execute large-scale analytical queries, the workload is distributed among nodes to parallelize query execution. Each machine runs an PostgreSQL database instance, which is modified to support parallel query execution. All the nodes are connected via Greenplum interconnect(the netwrok layer) to perform the behaviour as a single database instance. Greenplum differs from Postgres in 3 ways, first it leverages Orca as a query planner, second it supports column store, third it has declarative partitioning and sub-partitioning.


Views 
Virtual Views

Views are not materialized, they are generated every time the query executes.