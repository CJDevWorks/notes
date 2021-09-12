PostgreSQL
PostgreSQL is an object-relational database based on Postgres, developed from University of California at Berkeley. It is ACID-compilant and supports materialized view, stored functions, triggers, and foreign keys. PostgreSQL is a free and open-source software under the PostgreSQL License, still often referred to as Postgres by many people. Postgres has been continuously maintained since 1996 by the PostgreSQL Global Development Group, which consists of many companies as well as many individual contributors.


History 
PostgreSQL is derived from Postgres, developed by University of California at Berkeley. Postgres was created by Michael Stonebraker as a follow up project to Ingres and released in 1994 (the name is meant to be "Post Ingres"). Two Berkeley Ph.D. students, Andrew Yu and Jolly Chen, later brought a subset of SQL to Postgres and renamed the system to Postgres95. The system was then maintained and developed in the open source world outside of Berkeley, and finally renamed as PostgreSQL.


Checkpoints 
Consistent

PostgreSQL supports pg_dump to extract a consistent database into a file while concurrent transactions are running. While pg_dump only outputs a single database, pg_dumpall is used to dump all databases. For checkpoints, PostgreSQL supports periodic checkpointing as well as immediate checkpointing, which both guarantee that previous changes would be written to disk.


Concurrency Control 
Multi-version Concurrency Control (MVCC)

PostgreSQL applies Multi-version Concurrency Control for data consistency. For MVCC, not only the current status but also previous values of data are visible to the transaction, which provides transaction isolations. The primary advantage of MVCC over locking is that the writing operation won't conflict with the reading operation on the same block of data. Thus, MVCC reduces the lock contention to achieve high throughput.


Data Model 
Object-Relational

PostgreSQL is an object-relational database (i.e., similar to relational database with an object-oriented database model). This means objects are supported in database schemas and query languages. The object-relational database inherits the relational mathematical base with the flexibility to define complex datatypes. Particularly, new types of all objects inside PostgreSQL can be created, including: conversion, cast, functions, data types, domains, procedure languages and indexes.


Foreign Keys 
Supported

PostgreSQL allows user to define a foreign key constraint, which means the values in that column match the keys in other tables. PostgreSQL also supports a foreign key to contain multiple columns. Besides, a tabel is allowed to define multiple foreign key constraints in PostgreSQL, which is usually used in many-to-many relations among the tables. When the table contains the primary key, which is referenced as foreign key in another table, is deleted, PostgreSQL provides several options, including a) Disallow deleting the referenced table b) Delete the forieng key table as well c) something else.


Indexes 
B+Tree Hash Table Inverted Index (Full Text)

PostgreSQL provides the index methods including B-tree, hash, GiST and Gin. User can specify the method through an argument when creating the table. An extra parameter is required for those four methods. User needs to decide how full the index method packs the index page for B-tree, hash and GiST. For heavily updated workload, the parameter should be lower than the read-only workload to reduce the frequency of page split while sacrificing more space. For Gin index, users need to specify whether its fast update option is enabled.


Isolation Levels 
Read Uncommitted Read Committed Serializable Snapshot Isolation Repeatable Read

PostgreSQL provides snapshot isolation using the multiversion concurrency control (MVCC) architecture. User could requst Read Uncommitted, Read Committed, Repeatable Read and Serializable transaction isolation levels in PostgreSQL. However, PostgreSQL only implements three of them. When requesting Read Uncommitted, postgres actually does Read Committed and Dirty Read won't happen, thinking that this would give an inconsistent response and in any case is unnecessary because MVCC allows access to data even while it is being written.


Joins 
Nested Loop Join Hash Join Sort-Merge Join

PostgreSQL supports three join implementations: Nested-Loop, Hash and Sort-Merge. When number of join operations is less than a threshold, the default value is 12, PostgreSQL would conduct a near-exaustive to find the cheapest strategy, i.e. all possible plans are genearated to select the best one. When the threshold is exceeded, which suggests searching would be too time-consuming, PostgreSQL would apply heurisitc algorithms to decide join plan.


Logging 
Physical Logging

PostgreSQL allows users to control what SQL transactions are logged. The options are none, ddl, mod and all. For example, ddl option would only log the transactions that modify the database, such as CREATE, ALTER and Drop statements. While mod option record all ddl transactions with data-modifying statements such as INSERT, UPDATE and DELETE. The logging takes place when the execute message of a transaction is received.


Parallel Execution 
Intra-Operator (Horizontal)

Postgres added parallel execution for sequential scans, joins, and aggregations in 2016. Additional support for hash joins was added in 2018.


Query Compilation 
Not Supported

PostgreSQL currently does not support query compilation. While some researchers do implement LLVM JIT Compilation for PostgreSQL that the expressions in every query are compiled. Their JIT implementation might be included into the master in the future.


Query Execution 
Tuple-at-a-Time Model

Query Interface 
PL/SQL

PostgreSQL covers a wide range of SQL standards, including operations in transaction-level such as ABORT, BEGIN and END, the Data Definition Languge to create/modify/drop tables, like CREATE, DROP and ALTER as well as Data Manipulation Language, i.e. SELECT, INSERT and DELETE. It also supports procedural languages to create user-defined functions through multiple languages, such as Tcl, Perl and Python.


Storage Architecture 
Disk-oriented

PostgreSQL stores the table and its index in disk. Memory is used as shared-buffer to accelerate queries. The default size of size of memory is 128 megabytes, which can be changed in runtime config. The user could also changes the memory dedicated for internal operations such as sort, in case the default 4 megabytes are insufficient.


Storage Model 
N-ary Storage Model (Row/Record)

PostgreSQL is a row-oriented database server. Every table and its index is stored into a file separately. The file is named by its table or index's filenode number defined in the catalog. Along with the main file, a free space map is also kept to store informations about free space available in the relation. The file is divided to separate segments once its size is larger than 1 GB.


Storage Organization
Heaps

Stored Procedures 
Supported

A stored procedure is defined throught CREATE FUNCTION in PostgreSQL, which allows users to write multiple queries without round trips in a single function. A stored procedure usually returns no value, which means the return value should be specified as NULL. In other cases, which the procedure returns a result set, user should specify the return type as refcursor.


System Architecture 
Shared-Everything

PostgreSQL doesn't support multi-master shared-storage but cold standby failure for shared-storage. Which means a secondary server would be the backup of another identical primary system and it's installed and configured once the primary server breaks down. Using PostgreSQL in multi-master shared storage could result in data corruption. Thus, when a primary server is running, the standby server should never access the shared storage.


Views 
Virtual Views Materialized Views

PostgreSQL supports both virtual view as well as materialized view. For the virtual one, the create query is run everytime the view is referenced in a trasaction. For materialized view, the query is executed once the command is issued. The materialized view table may be refreshed later by REFRESHING MATERIALIZED VIEW command. PostgreSQL also replaces the view if the same name already existed.