MongoDB 
MongoDB is a free and open-source cross-platform document-oriented program. It is a NoSQL database uses JSON-like documents with schemas-less. Ad hoc queries, indexing and real time aggregation provide powerful ways to access and analyze the data. It is a distributed database at its core that provides high availability, horizontal scaling, and geographic distribution.


History 
The software company 10gen began developing MongoDB in 2007 as a component of a planned platform as a service product. In 2009, the company scraped its cloud platform and focus on maintaining MongoDB instead. It shifted to an open source development model, with the company offering commercial support and other service. In 2013, 10gen changed its name to MongoDB Inc.


Checkpoints 
Consistent

When writing to disk, WiredTiger writes all the data in a snapshot to disk in a consistent way across all data files. The now-durable data act as a checkpoint in the data files. The checkpoint ensures that the data files are consistent up to and including the last checkpoint; i.e. checkpoints can act as recovery points. MongoDB configures WiredTiger to create checkpoints (i.e. write the snapshot data to disk) at intervals of 60 seconds or 2 gigabytes of journal data. During the write of a new checkpoint, the previous checkpoint is still valid. As such, even if MongoDB terminates or encounters an error while writing a new checkpoint, upon restart, MongoDB can recover from the last valid checkpoint.


Concurrency Control 
Two-Phase Locking (Deadlock Prevention) Optimistic Concurrency Control (OCC)

In MongoDB 3.0, concurrency control has been separated into two levels: top-level, which protects the database catalog, and storage engine-level, which allows each individual storage engine implementation to manage its own concurrency below the collection level. MongoDB uses reader-writer locks that allow concurrent readers shared access to a resource, but in MMAPv1, give exclusive access to a single write operation. WiredTiger uses OCC for concurrency control.


Data Model 
Document / XML

MongoDB stores data in a binary representation called BSON (Binary JSON). The BSON encoding extends the popular JSON (JavaScript Object Notation) representation to include additional types such as int, long, date, floating point, and decimal128. BSON documents contain one or more fields, and each field contains a value of a specific data type, including arrays, binary data and sub-documents. Documents that tend to share a similar structure are organized as collections. With the MongoDB document model, data is more localized, which significantly reduces the need to JOIN separate tables. The result is dramatically higher performance and scalability across commodity hardware as a single read to the database can retrieve the entire document containing all related data


Indexes 
B+Tree

Fundamentally, indexes in MongoDB are similar to indexes in other database systems. MongoDB defines indexes at the collection level and supports indexes on any field or sub-field of the documents in a MongoDB collection. MongoDB provides a number of different index types to support specific types of data and queries. The unique indexes will reject insertion or update with existing value. The compound indexes is useful for queries that specify multiple predicates. For fields that contain an array, each array value is stored as a separate index entry, this is array indexes. Time to Live indexes allow the user to specify a period of time after which the data is automatically deleted from the database. Geospatial index optimize queries related to location within a two dimensional space. Partial indexes only index the documents in a collection that meet a specified filter expression. The sparse property of an index ensures that the index only contain entries for documents that have the indexed field. MongoDB uses b-tree for the data structure of index.


Isolation Levels 
Read Uncommitted

Read Uncommittedis the default isolation level and applies to mongod standalone instances as well as to replica sets and sharded clusters. Write operations are atomic with respect to a single document. When a single write operation modifies multiple documents, the modification of each document is atomic, but the operation as a whole is not atomic and other operations may interleave. Due to this reason, MongoDB exhibits non-point-in-time read operations, non-serializable operations and reads may miss matching documents that are updated during the course of the read operation.


Joins 
Not Supported

MongoDB does not support joins. In MongoDB some data is denormalized, or stored with related data in documents to remove the need for joins. However, in some cases it makes sense to store related information in separate documents, typically in different collections or databases. MongoDB applications use one of two methods for relating documents: Manually references and DBRefs. Using manual references is the practice of including one document’s id field in another document. The application can then issue a second query to resolve the referenced fields as needed. DBRefs are a convention for representing a document, rather than a specific reference type. They include the name of the collection, and in some cases the database name, in addition to the value from the id field.


Logging 
Physiological Logging

To provide durability in the event of a failure, MongoDB uses write ahead logging to on-disk journal files. With journaling, WiredTiger creates one journal record for each client initiated write operation. The journal record includes any internal write operations caused by the initial write. MongoDB configures WiredTiger to use in-memory buffering for storing the journal records. Threads coordinate to allocate and copy into their portion of the buffer. All journal records up to 128 kB are buffered. Operations that modify a database on the primary replica set member are replicated to the secondary members using the oplog (operations log). The oplog contains an ordered set of idempotent operations that are replayed on the secondaries. The size of the oplog is configurable and by default is 5% of the available free disk space. For most applications, this size represents many hours of operations and defines the recovery window for a secondary, should this replica go offline for some period of time and need to catch up to the primary when it recovers.


Query Compilation 
JIT Compilation

The MongoDB JavaScript engine uses SpiderMonkey, which implements Just-in-Time (JIT) compilation for improved performance when running scripts.


Query Execution 
Tuple-at-a-Time Model

Query Interface 
Custom API

MongoDB provides native drivers for all popular programming languages and frameworks to make development natural. Supported drivers include Java, Javascript, .NET, Python, Perl, PHP, Scala and others, in addition to 30+ community-developed drivers. MongoDB drivers are designed to be idiomatic for the given language. The mongo shell is a rich, interactive JavaScript shell that is included with all MongoDB distributions. Additionally MongoDB Compass is a sophisticated and intuitive GUI for MongoDB. Offering rich schema exploration and management, Compass allows DBAs to modify documents, create validation rules, and efficiently optimize query performance by visualizing explain plans and index usage.


Storage Architecture 
Hybrid

Starting in MongoDB Enterprise version 3.2.6, MongoDB added in-memory storage engine into the storage engines. MongoDB replica sets allow for hybrid in-memory and on-disk database deployments. Data managed by the In-Memory engine can be processed and analyzed in real time, before being automatically replicated to MongoDB instances configured with the persistent disk-based WiredTiger storage engine. In-memory storage engine does not maintain any on-disk data, including configuration data, indexes, user credentials, etc. The in-memory storage engine does not persist data after process shutdown. In-memory storage engine requires that all its data must fit into the specified in-memory size. By default, the in-memory storage engine uses 50% of physical RAM minus 1 GB.


Storage Model 
Custom

MongoDB uniquely allows users to mix and match multiple storage engines within a single deployment. This flexibility provides a more simple and reliable approach to meeting diverse application needs for data. MongoDB uses memory mapped files for managing and interacting with all data. Memory mapping assigns files to a block of virtual memory with a direct byte-for-byte correlation. MongoDB memory maps data files to memory as it accesses documents. Unaccessed data is not mapped to memory. Once mapped, the relationship between file and memory allows MongoDB to interact with the data in the file as if it were memory.


Stored Procedures 
Not Supported

MongoDB currently does not support stored procedures function. However, there is similar function store a JavaScript Function in MongoDB. There is a special system collection named system.js that can store JavaScript functions for reuse.


System Architecture 
Shared-Nothing

MongoDB uses sharding as an implementation of shared-nothong system architecture. Sharding is a method for distributing data across multiple machines. A sharded cluster consists of three components: shard, mongos, and config servers. Each shard can be deployed as a replica sets. Each replica set contains a unique range of data. The data is distributed amongst replica sets based on a sharding key. Mongos acts as a query router, providing an interface between client applications and the sharded cluster. Config servers store metadata and configuration settings for the cluster. This allows each shard to process a subset of cluster operations. Both read and write wordloads can be scaled horizontally across the cluster by adding more shards and increases the storage capacity of the cluster.


Views 
Virtual Views

Views are new in MongoDB 3.4, which are non-materialized views, and behind the scenes the engine runs an aggregation. Creating a view requires that we specify a collection or a previous existing view. When a view is the source collection from another view, it allows us to execute a chained aggregation. Views are read-only; write operations on views will error. Cascading aggregations (creating views of views) can be slow, as the view does not have any data and therefore cannot be indexed. MongoDB neither checks the collection fields nor the collection existence before creating the view. If there is no collection, the view returns an empty cursor.