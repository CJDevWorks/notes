LevelDB 
LevelDB is a key/value store built by Google. It can support an ordered mapping from string keys to string values. The core storage architecture of LevelDB is a log-structured merge tree (LSM), which is a write-optimized B-tree variant. It is optimized for large sequential writes as opposed to small random writes.


History 
Two Googlers Jeff Dean and Sanjay Ghemawat were inspired by the design scheme of BigTable tablet. Tablets in BigTable are defined as segments of the table split along chosen row. They wanted to build one open-source system containing the characteristic of BigTable tablet.


Checkpoints 
Blocking

When operation logging file exceeds over the limit, it will do checkpoints. Data will be flushed to the disk. And compaction scheme will be called. So data will go down levels. Aside from that, leveldb will generate new logging file and memtable for new use.


Compression
Naïve (Record-Level)

Concurrency Control 
Two-Phase Locking (Deadlock Prevention)

Leveldb only allow one process to open at one time. The operation system will use the locking scheme to prevent concurrent access. Within one process, Leveldb can be accessed by multiple threads. For multi-writers, it will only allow the first writer to write to database and other writers will be blocked. For read-write conflicts, readers can retrieve data from immutable which is seperated from writing process. The updated version will come into effect in compaction process.


Data Model
Key/Value

Key/value store supports the mapping from the key to the corresponding value. In SSTable the layout of key and value is managed as adjacent string sequence.


Indexes
Skip List Log-Structured Merge Tree

It uses skip list in MemTable. Aside from that, LSM-tree is one type of write-optimized B-tree variants consisting of key-value pairs. The LSM-tree is a persistent key-value store optimized for insertions and deletions. LevelDB is an open source LSM-tree implementation.


Isolation Levels 
Snapshot Isolation

It saves the state of database at a given point and supports reference to it. Users can retrieve data from specific snapshot at the time the snapshot was created.


Joins
Not Supported

Logging 
Logical Logging

Before every insertion, update or delete, system need to add the message to log. In case of node's failure, uncommited messages can be retrieved and do operation again for recovery.


Query Compilation
Not Supported

Cannot find enough information about query compilation


Query Execution
Tuple-at-a-Time Model

Query Interface 
Custom API

Keys and values in leveldb are byte arrays with arbitrary length. It supports basic operations like Put(), Get(), Delete(). It also support Batch operations: Batch(). The whole process of operations will run together and return result in a single Batch operation. However, it does not support SQL queries because this is not a SQL type database. Aside from that, it has no support for indexing.


Storage Architecture 
Disk-oriented

It puts temporarily accessed data into MemTable and periodically moves data from MemTable into Immutable SSTable. Aside from that, it adopts compaction to reduce the invalid data in each level and then generates one new block at the next level. It uses mmap or native read syscall to read SSTable for querying. The OS caches SSTable for LevelDB. As LevelDB supports using snappy to compress the value, to avoid uncompress data for each query, it introduces Cache.


Storage Model 
N-ary Storage Model (Row/Record)

SSTable uses NSM to arrange data. It contains a set of arbitrary, sorted key-value pairs. At the end of the block, it provides the start offset and key value for each block. So bloom filter can be used to search for target block.


Storage Organization
Log-structured

Stored Procedures
Not Supported

System Architecture
Embedded

In leveldb immutable are stored on the disk which can be shared by different cluster nodes. There are totally 7 levels plus at most two in-memory tables. The procedure can be described as firstly the system buffers write operations in an in-memory table called MEMTable and flushes data to disk when it becomes full. On the disk, tables are organized into levels. Each level contains multiple tables called SSTable. The down level maintains larger capacity than the upper level. When the upper level is full, the system needs to push data to the down level, which might need to read and write multiple SSTables.


Views
Not Supported