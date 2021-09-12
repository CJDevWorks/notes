RocksDB
RocksDB is an embedded database using key-value data, and is developed by Facebook for high performance purposes. RocksDB is forked from LevelDB, which was developed by Google to exploit the best performance of many CPU cores as well as fast storage like SSD for I/O bound workloads. Based on a log-structured merge-tree, RocksDB is able to achieve very high performance and it is adaptable to different workloads (can be used for various of data needs). RocksDB also supports both basic and advanced database operations, including merging and compaction filters. RocksDB is written in C++ and it supports API bindings for C++, C, Java, Python, PHP, as well as many other third-party language bindings. RocksDB is used in production in several large companies such as Facebook, Yahoo!, and LinkedIn.


History 
In an attempt to extend HDFS's success from Data Analysis to Query Serving workloads (this workload requires low latency), Dhruba Borthakur enhanced HBase and make its latencies twice as slow as MySQL server. Then when flash storage came out, it became clear that a new storage engine was needed to serve a random workload efficiently. He started seeking for new techniques to build next generation key-value store, especially for serving data that resides on fast storage. Since he used flash storage, the network data access was 50% higher overhead than local data access, which meant that embedded database within an application could have much slower latency than applications that access data across the network. At that time, there were several existing embedded database: BerkeleyDB, SQLite3, as well as leveldb, which was the fastest according to open-source benchmarks, plus its written in c++, thus leveldb became the first choice for his benchmarking. Soon he found out that leveldb was not suitable for the Query Serving workloads. leveldb only works well when the size of the database is smaller than the size of RAM. Additionally, leveldb's single-threaded compaction process was insufficient to drive server workloads, and it was not able to consume all the I/Os that were offered by the underlying flash storage. Finally, he decided that the best path was to fork the leveldb code and change its architecture to suit the needs (use a database that can drive fast storage hardware), then RocksDB was born.


Checkpoints 
Non-Blocking Consistent

RocksDB supports snapshot checkpoints on a running database, which were took and stored in a separate directory. Checkpoints can be used for both full and incremental backups.


Concurrency Control 
Optimistic Concurrency Control (OCC)

RocksDB supports two kinds of transactions: TransactionDB and OptimisticTransactionDB. Transactions have BEGIN, COMMIT and ROLLBACK APIs, allowing applications to modify the data concurrently while RocksDB is checking conflicts. RocksDB supports both pessimistic and optimistic concurrency control.


Data Model 
Key/Value

RocksDB uses embedded key-value store, in which keys and values are arbitrary byte streams. RocksDB organizes all data in sorted order and the common operations are Get(key), Put(key), Delete(key) and NewIterator().


Indexes 
Log-Structured Merge Tree

All RocksDB's persistent data is stored in a collection of SSTs. For a Get() query, RocksDB scans through mutable memtable, list of immutable memtables, and SST files to find the target key. SST files are stored in levels.


Isolation Levels 
Snapshot Isolation

RocksDB supports SNAPSHOT isolation level.


Joins
Not Supported

Query Compilation
Not Supported

Query Execution 
Tuple-at-a-Time Model

The database provides Put, Delete, and Get methods to modify/query the database. This is not quite the same as query execution in other relational databases.


Query Interface 
Custom API

The database provides Put, Delete, and Get methods to modify/query the database. This is not quite the same as query execution in other relational databases.


Storage Architecture 
Disk-oriented In-Memory Hybrid

RocksDB is designed to make full use of the fast accessing speed of flash storage. However, it also supports pure memory storage.


Storage Model 
Custom

All RocksDB's data is organized in a collection of SSTs. They often use sst, table and sst file interchangeably.


Storage Organization
Log-structured

Stored Procedures
Not Supported

System Architecture 
Embedded

RocksDB supports flexible configuration settings, which may be tuned to run on various production environments, including pure memory, Flash, hard disks or HDFS.


Views
Not Supported