Elasticsearch 
Elasticsearch is a highly scalable open-source full-text search and analytics engine based on Lucene. It allows you to store, search, and analyze big volumes of data quickly and near real time. It is generally used as the underlying engine/technology that powers applications that have complex search features and requirements. A few sample use-cases including online web store catalog, collect and analyze logs for data mining, supervise and alerting system, business-intelligence needs. Elastic stack is used by many technology companies including Linkedin and Uber, its business counterpart is Splunk. Elasticsearch is the search engine part of Elastic stack. For most cases, you will also need Logstash, the data import and storage system, Kibana, the data visualization system.


History 
Compass is the precursor to ElasticSearch, created by Shay Banon in 2004. In the release of its 3rd version, Banon rewrite big parts of Compass to "create a scalable search solution". A solution built from the ground up to be distributed and used a common interface, JSON over HTTP. Shay Banon released the first version of Elasticsearch in February 2010. Elasticsearch BV was founded in 2012 to provide commercial services and products around Elasticsearch and related software. In March 2015, the company ElasticSearch changed their name to Elastic.


Checkpoints 
Blocking Fuzzy

By default, Logstash uses in-memory bounded queues absorbs bursts of events and buffer them on disk. Persistent queues provide durability of data within Logstash for Elastic systems. When it's enabled, Logstash will store events on disk, commit to disk using checkpointing. The persistent queue has two kinds of pages: head pages and tail pages. There is only one head page, when head page is of a certain size, it becomes a tail page. Tail page is immutable and head page is append only. When recording a checkpoint, Logstash will call fsync on the head page and atomically write to disk the current state of the queue. The process of checkpointing is atomic, any update to the file is saved if successful. If Logstash is terminated or there is a hardware-level failure, any data that is buffered in the persistent queue but not yet checkpointed is lost.


Concurrency Control 
Two-Phase Locking (Deadlock Detection)

Elasticsearch does not support ACID transactions for changes involving multiple documents, changes to individual documents are ACIDic. If your main data store is a relational database, and Elasticsearch is simply being used as a search engine or as a way to improve performance, then ACID transactions is dealt with in the relational database. If you are not using a relational store, these concurrency issues need to be dealt with the Elasticsearch level. The three practical solutions used by Elasticsearch are Global Locking, Document Locking, Tree Locking, with increasing fine-grained lock level. Each of them is kind of two-phase locking. Global Lock will block the entire storage system to enable only one writer at a time. Document Locking will lock for all involved files. Tree Lock will lock only a directory.


Data Model 
Document / XML

Elasticsearch is a document oriented distributed database. The entire object graph you want to search needs to be indexed, so before indexing your documents, they must be denormalized. Elasticsearch design mappings and store the document in a way that is optimized for search and retrieval. They are excellent for write-once-read-many-workloads. Like many other document oriented databases, Elasticsearch don't have constraints on data.


Indexes 
Hash Table

Elasticsearch target at text search, so different with most relational database index implementations. Elasticsearch use inverted index as its basic index structure. An index term is the unit of search. It turns everything to look like a string prefix problem. To favor search speed, Elasticsearch will compact the index because when searching over a smaller index, less data needs to be processed, and more of it will fit in memory. But there is also trade-off since compactness means sacrificing the possibility to efficiently update them. An Elasticsearch index is made up of one or more shards, which can have zero or more replicas. These are all individual Lucene indexes, which in turn is made up of index segments.


Isolation Levels 
Snapshot Isolation

Elasticsearch doesn't support transactions. Also, Elasticsearch is more preferable in read intensive workload. When you enable versioning feature, it could ensure one-session semantics. If not using versioning, all modification will come to the same document.


Joins 
Nested Loop Join Hash Join

Performing full SQL-style joins in a distributed system like Elasticsearch is prohibitively expensive. Instead, Elasticsearch offers two forms of join which are designed to scale horizontally, nested query, haschild and has parent queries. Nested query utilized similar idea of nested loop join, Documents may contain fields of type nested. These fields are used to index arrays of objects, where each object can be queried (with the nested query) as an independent document. Haschild and has_parent queries use hash join to return docs match parent in child or docs match child in parent within a single index.


Logging 
Logical Logging

Maybe different from relational database systems. Logging in Elasticsearch is supported by Log4j. It's event based logging. Elasticsearch allows you to update the logging settings dynamically. Its logs are used for analysis more than recovery. For data resiliency, Elastic stack use the checkpointing features introduced above.


Query Compilation 
Code Generation

Users of Elasticsearch encode their queries in a JSON. JSON will be parsed in server side to generate related code to perform the queries on index at different shards.


Query Execution 
Materialized Model

Distributed search execution has to consult a copy of every shard in the indices we're interested in to see if any matching documents. After finding all matching documents, results from multiple shards must be combined into a single sorted list before the search API can return a "page" of results. Elasticsearch is executed in a two-phase process called query then fetch.


Query Interface 
Custom API

Elasticsearch provides the search API allows you to execute a search query and get back search hits that match the query. The query can either be provided using a simple query string as a parameter, or using a request body. It's a RESTful service. You can use either URI search or Request Body Search. The search API contains advanced features like suggesters, count API, Validate API, Explain API, Profile API, etc.


Storage Architecture 
Disk-oriented

Elasticsearch does not rely on special hardware like GPU or FPGA. Documents are stored in disk. Elasticsearch uses Lucene under the hood to handle the indexing and querying on the shard level. The files in data directory are written by both Elasticsearch and Lucene. Lucene is responsible for writing and maintaining the Lucene index files while Elasticsearch writes metadata related to features on top of Lucene.


Storage Model 
Custom

Elasticsearch is document based database. It stores a record in a whole document. The document is a JSON object, all attributes are stored together in that object. In Elasticsearch, the term document has a specific meaning. It refers to the top-level, or root object that is serialized into JSON and stored in Elasticsearch under a unique ID.


Stored Procedures 
Not Supported

Elasticsearch does not have the concept of stored procedures. But you can write a scrip query to evaluate some custom expressions, although they are different with the idea of stored procedures, it just also provides some kinds of customize.


System Architecture 
Shared-Nothing

Elasticsearch is a distributed search engine. Each node is independent and contains its own Lucene indices. In terms of data store, it's shared nothing. But it still need some orchestrate mechanism to communicate metadata necessary to perform queries.


Views 
Virtual Views

Joins are not common use case in Elasticsearch. It does not support views directly but you can use a named query in Elasticsearch request body just like use view in a SQL query. Plugin for view support maybe released in the future.