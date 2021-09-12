Hive 
Apache Hive is a data warehouse software built on top of Hadoop that facilitates reading, writing and managing large datasets residing in distributed storage using SQL. Hive provides the necessary SQL abstraction so that SQL-like queries can be integrated with the underlying Java code without having to implement the queries in the low-level Java API. It allows structure to be projected onto data that is already in storage. Hive also provides a command line tool and a JDBC driver that users can use to connect to Hive.


History 
Apache Hive was co-created by Joydeep Sen Sarma and Ashish Thusoo during their stint at Facebook. Both of them realized that in order to make the best use of Hadoop, they would have to write some fairly complex Java Map-Reduce jobs. They realized that they would not be able to teach their fast growing engineering and analyst teams the skill set needed to be able to exploit Hadoop across the organization. SQL was the interface used widely by the engineers and analysts. While SQL could cater to most analytics requirements, the creators also wanted to bring in the programmability that Hadoop provides. Apache Hive was born out of these dual goals - an SQL-based declarative language that also allowed engineers to be able to plug in their own scripts and programs when SQL did not suffice. To facilitate the creation of data driven organizations, it was also built to store centralized metadata(Hadoop based) about all the datasets in the organization.


Checkpoints 
Non-Blocking

Apache Hive is built atop Hadoop. The checkpointing mechanism is the same as in HDFS.


Concurrency Control 
Two-Phase Locking (Deadlock Prevention)

Apache Hive allows concurrent access through the use of locks. It supports shared lock and exclusive lock. In order to avoid deadlocks, all the objects to be locked are sorted in a lexicographic manner, and the locks are acquired in order.


Data Model 
Relational

All the data is stored in HDFS as files. Within a particular database, the data in the tables is serialized and each table has its own corresponding HDFS directory. The data within the table can be sub-divided into partitions that can in turn determine how data is distributed within sub-directories under the table directory. The partition data can further be divided into buckets.


Indexes 
BitMap

Hive supports Bitmap indexing and compact indexing. The Bitmap index is implemented as a byte-aligned bitmap compression.


Isolation Levels 
Snapshot Isolation

Currently, Apache Hive only supports Snapshot Isolation. When the query begins, it is provided with a consistent snapshot of the database which it uses till the end of its execution. Other isolations may be added in the future depending on demand. With the addition of transactions in Hive 0.13, full ACID semantics is now provided at the row level, so that one application can add rows while another reads from the same partition without interfering with each other. Initially it was only at the partition level.


Joins 
Hash Join Sort-Merge Join

Apache Hive supports Hybrid Grace Hash join(called map join in Hive). During the partitioning phase, an in-memory hash table is built for the first partition of R. Similarly, the first partition of S can do the probing directly against the in-memory partition of R. This enable the join of the first pair of partitions of R and S to be done at the end of the partitioning phase. Sort-Merge join is implemented as sort-merge bucket join in Hive. Each mapper reads a bucket from the first table and the corresponding bucket from the second table and then a merge sort join is performed.


Query Compilation 
Not Supported

LLAP is the new hybrid execution model that is being shipped with HIVE 2.0 version and above, that makes queries much more efficient. It enables caching of columnar data, creates JIT-friendly operator pipelines, allows multi-threaded processing and pre-fetching to name a few. However, it is still in the early stages and we need to see how it matures.


Query Execution 
Tuple-at-a-Time Model Vectorized Model

Query Interface 
SQL

The query interface used by Hive is HiveQL. While it is based on SQL, HiveQL does not strictly follow the full SQL-92 standard.


Storage Architecture 
Disk-oriented In-Memory Hybrid

Hive has predominantly been a disk-based architecture since it was mainly used in data warehousing on multi-petabyte datasets spanning thousands of nodes. However, there are many interesting use cases with smaller datasets which require a more interactive setting. This called for a shift to in-memory architectures. Hive2 marks the beginning of Hive’s journey from a disk-centric architecture to a memory centric architecture through Hive LLAP ( Live Long and Process). Since memory costs are 100x times more than a disk, this shift has required a careful redesign of the system architecture to make best use of available resources while meeting the brief.


Storage Model 
Decomposition Storage Model (Columnar) N-ary Storage Model (Row/Record) Hybrid Custom

In Apache Hive, all the data is present in HDFS as files. The tables in Hive are similar to tables in Relational Databases. Databases contain tables, which are in turn made up of partitions. Apache Hive supports the following File Formats - 1. Text File - Data is laid out in lines, with each line being a record. Lines are terminated by a newline character in the typical unix fashion. 2. SequenceFile - They encode a key and a value for each record. The records are stored in a binary format and hence occupies lesser space than a text-based format would. 3. Columnar File Formats (RCFile, Parquet) - Allows column values to be stored adjacent to each other and provides all the advantages of DSM model. 4. Avro Files - The format encodes the schema of its contents directly in the file which allows the user to store complex objects natively. Avro is not really a file format, it’s a file format plus a serialization and deserialization framework. 5. ORC fIles - This is the Optimized Row Columnar file format that provides a highly efficient way to store Hive data and overcomes the limitations of other Hive file formats. 6. Custom INPUTFORMAT and OUTPUTFORMAT


Stored Procedures 
Supported

Hive Hybrid Procedural SQL On Hadoop (HPL/SQL) is an opensource tool that implements procedural SQL for Hive. It provides support for richer language in terms of allowing advanced expressions, various built-in functions and conditions to generate SQL on the fly based on the user configuration.


Views 
Virtual Views

In Apache Hive, the view is purely a logical object and does not have any associated storage. Creating on a view follows the same process as executing any other query. Hive does not yet support updatable views and all views are read-only.