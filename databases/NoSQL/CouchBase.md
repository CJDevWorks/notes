Couchbase 
Couchbase is an open-source, distributed NoSQL document database. It supports the Memcached client protocol and provides extra features like disk persistence, data replication.


History 
In 2010, the initial version of Couchbase, originally called Membase, was developed at NorthScale, which was founded by developers from Memcached project. In February 2011, the Membase project founders and Membase, Inc. merged with CouchOne (a company with many engineers behind CouchDB) as a new company called Couchbase, Inc. In January 2012, Membase was renamed to Couchbase Server.


Checkpoints 
Consistent

The checkpoint inside the Couchbase Server is a record of last sequenceID. The Sequence ID is an internal unique number for every change happened in Couchbase Server with chronological increasing order. The replicator of the Couchbase Server sends the checkpoint of last change to the target at the end of every replication cycle. The target could be any remote Couchbase Server database where the changes are replicated.


Compression 
Naïve (Record-Level)

Couchbase Server (Enterprise Edition) applies data compression to documents with the Snappy third-party library. There are three modes of compression in Couchbase Server. Off Mode: The Couchbase Server decompresses the document if it is compressed, and stores the uncompressed document in memory but recompresses it when storing on disk. Also, Couchbase server sends the document in uncompressed form. Passive Mode: When Couchbase Server receives the compressed document, it stores the compressed document in memory and disk. At the same time, the documents are sent in compressed form. * Active Mode: Couchbase Server stores and sends compressed document even if the document is uncompressed.


Concurrency Control 
Optimistic Concurrency Control (OCC)

Couchbase Server offers both optimistic and pessimistic locking to guarantee concurrency. The optimistic locking is implemented with Compare-and-Swap (CAS) value, which is a unique and atomic incrementing identifier inside the metadata of document. Couchbase Server verifies the CAS value before a document is modified. It also supports pessimistic locking which is less commonly used.


Data Model 
Key/Value Document / XML

The documents stored in Couchbase Server are in JSON or binary format.


Foreign Keys 
Not Supported

Couchbase Server does not support foreign keys.


Indexes 
B+Tree Skip List Hash Table Inverted Index (Full Text)

A few of indexes are available in Couchbase Server: Primary Index is based on the unique key of every item in a specified bucket. The bucket is introduced in "Storage Model". Primary index contains a full set of keys in a configured key space. Global Secondary Index (GSI) is the most frequently used index in Couchbase Server. The indexer for GSI creates a B+ tree for fast scans on the index key. Also, there is a Memory-Optimized GSI index which uses the skip-list structure as opposed to B-tree indexes. Full Text is provided by the Search Service and it contains targets derived from the contents of documents within one or more specified buckets. View index is generated with fields and information extracted from documents.


Isolation Levels 
Read Committed Serializable

Couchbase Server provides read committed isolation at the single document level. However, by enabling a more restrictive concurrency control scheme, supports serializable isolation for a single document.


Joins 
Nested Loop Join

Couchbase Server supports lookup join, index join and ANSI join in its N1QL interface.


Query Interface 
Custom API

Couchbase Server presents a new SQL language called N1QL which is a SQL extension for JSON as the query interface.


Storage Architecture 
Disk-oriented

Couchbase Server maintains hot data in the memory to achieve high performance. The data which is not recently used will be swapped on to disks.


Storage Model 
Custom

Couchbase Server stores items in the Buckets. There are two kinds of Buckets in the Couchbase. One is Couchbase Buckets which could reside both in memory and disks. Another is Ephemeral bucket which only stays in the memory.


Storage Organization 
Sorted Files

Couchbase Server uses Couchstore to store its data. Each Bucket (the smallest unit of Couchbase's storage model) is stored as a separate Couchstore file in the file system. B+tree structure is used to provide fast items access. Append-only write model is applied for efficient writes.


Stored Procedures 
Supported

A similar feature called "Prepared queries" is supported in Couchbase Server.


System Architecture 
Shared-Nothing

Each machine running Couchbase Server is a single node, and multiple nodes could join together as a cluster. Every node of the cluster has a Cluster Manager module for communication. The data inside the cluster is well distributed and replicated over the nodes.


Views 
Materialized Views

Three views are supported by Couchbase Server: MapReduce views, Spatial views and Global Secondary Indexes (GSI) views. They could be accessed by customized APIs or N1QL interface.