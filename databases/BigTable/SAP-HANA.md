HANA 
SAP HANA is a column-oriented, in-memory relational DBMS developed by SAP SE that is designed for hybrid (OLTP + OLAP) workloads. HANA also supports multiple advanced analysis, such as financial predictions, graph-data processing, as well as text analytics. It also offers Platform as a service on multiple cloud providers currently.


History 
The early development of SAP HANA was based on TREX search engine, P*Time, and MaxDB, which was mainly designed for the real-time data analytics and aggregation at first. SAP HANA also offers Platform as a service on multiple cloud providers currently. In 2016, SAP HANA 2 was released, which can also support Earth Observation Analysis and Text Analysis, apart from optimizing database and application management functionalities.


Checkpoints 
Fuzzy

SAP HANA supports fuzzy checkpoints, where any updates are still stored in storage snapshots even if transactions are not committed. In that case, extra work is needed to remove those updates, if transactions are aborted. SAP HANA also supports encrypted snapshots when the original database is encrypted first.


Concurrency Control 
Multi-version Concurrency Control (MVCC)

SAP HANA supports Multi-version Concurrency Control as the default mechanism to ensure data consistency. When one user connects to the database, a snapshot is provided for each user, where the changes from one user can only be seen by others only after transactions are committed. No rollback segment is supported by the insert method in SAP HANA. Distributed locking with a global deadlock detection mechanism and distributed snapshot isolation are both supported in SAP HANA to achieve synchronization. Moreover, one optional background garbage collection thread is also supported to remove expired versions.


Data Model 
Column Family

SAP HANA is based on the columnar storage structure, where data are stored in columns to minimize the storage footprint because repeating values are only stored once. Specific. it is very easy to modify other structures to the columnar structure in SAP HANA due to its fast in-memory design.


Foreign Keys 
Supported

SAP HANA supports foreign key constraints to enforce integrity.


Indexes 
B+Tree Hash Table Inverted Index (Full Text)

SAP HANA supports multiple index data structures, including B+Trees, Compressed Prefix B+Tree, and Inverted indexes.


Isolation Levels 
Read Committed

In SAP HANA, the default isolation level is ReadCommited, and the maximum level is Serialization. Snapshot Isolation is not supported by default.


Joins 
Nested Loop Join Hash Join

Both Hash Join and Nested Loop Join are supported by SAP HANA. Different variants of Hash Join are used in SAP HANA mostly.


Logging 
Physical Logging

Similar to other in-memory databases, persistent storage is also used for logging in SAP HANA. During the logging phase, only the real payload without any header is written service-specifically in SAP HANA. Moreover, it also supports third-party logging tools.


Query Compilation 
JIT Compilation

SAP HANA adopts LLVM JIT as the compilation backend for both stored procedures and query plans. One self-designed language called "Llang" is used to make the creation of LLVM-IR much easier. SQL-Semantics, Compile time, the degree of parallelism, keep running are key challenges that SAP HANA has to handle now.


Query Execution 
Vectorized Model

SAP HANA leverages the vectorized framework which can evaluate complex predicates and classify them based on the complexity to boost the performances. It works smoothly on the results extraction and unpacking for scanning predicates in the compressed in-memory columns currently.


Query Interface 
Custom API SQL

Apart from supporting SQL queries in SAP HANA, SQLScript, one self-designed scripting language similar to stored procedures in SAP HANA, is also supported, which can make users write complex queries more conveniently . In addition, MDX(multiple dimension eXpressions) is also supported, and it works to connect different analytics applications such as financial plannings directly.


Storage Architecture 
In-Memory

SAP HANA is an in-memory database. It uses in-memory computing technologies to store data with a complex data compression, which will improve the performance by avoiding too much disk I/O. Permanent storage of the data on disk is still required to achieve fault tolerance and the back-up operations will be executed asynchronously as a background task that will not influence the performance.


Storage Model 
Decomposition Storage Model (Columnar) N-ary Storage Model (Row/Record)

SAP HANA supports both N-ary Storage Model and Decomposition Storage Model. However, it is optimized for DSM as a default storage model in order to provide high performance on a hybrid workloads of analysis and transaction. SAP HANA allows joining row-oriented tables with column-oriented tables and also supports altering the storage model of an existing table.


Stored Procedures 
Supported

SAP HANA supports stored procedure features by allowing clients to describe a sequence of data transformations and define as a reusable processing block. A Procedure can be created with SQP HANA SQL queries or Using the Modeler wizard (Modeler and Development perspectives). The stored procedures can be parameterized and reused in another procedure.


System Architecture 
Shared-Nothing

For scalability support, SAP HANA uses multiple servers in one cluster and partitions the data to distribute across the servers with a shared-nothing architecture. The system has three components. The Name servers keep track of the location of data and store information on the topology of the entire system. The Index servers contain the actual data partitions and process the data as required. The last component is Statistics servers which collect information about status, performance and resource consumption from the system.


Views 
Virtual Views Materialized Views

SAP HANA supports both materialized and virtual views. When a materialized view is created, the system validates the definition and precomputes the result set from the database, which is stored on disk to improve the performance. SAP HANA also allows virtual views which replace the stored result set by on-the-fly calculation and are derived each time when they are used.