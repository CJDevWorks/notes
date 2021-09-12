Solr 
Solr is an open source NoSQL enterprise search platform built on Apache Lucene. Supporting distributed search and index replication, Solr is highly reliable, scalable and fault tolerant. It runs as a standalone full-text search server with a REST-like API and provides features including hit highlighting, faceted search, near real-time indexing, dynamic clustering, database integration, and geospatial search. Currently, Solr powers some of the highest-traffic websites and applications in the world.


History 
In 2004, CNET Networks, an American media website, started Solr to support search capability and later donated to Apache Software Foundation as a open-source project in 2006. In 2007, graduated as a top-level project (TLP), Solr grew steadily with more features and supported several popular websites. Finally in 2010, Solr was merged with Lucene as a sub project and changed the version number to 3.1 after Solr 1.4 to match that of Lucene.


Checkpoints 
Consistent

For standalone mode, Solr provides support for checkpoints through replication handler and will back up the system from the latest index commit point. Checkpoints can be triggered manually or users can set customized configurations to back up automatically after each commit or startup. For SolrCloud mode, Solr utilizes the Collection API which will back up the indexes and configurations to a shared filesystem. The checkpoints will be taken across multiple shards. When restoring, a new collection with same number of shards will be created and will preserve all the shard structure like routing information.


Concurrency Control 
Optimistic Concurrency Control (OCC)

Solr uses Optimistic Concurrency Control to ensure that documents can not be concurrently modified by multiple client applications. All documents will be assigned a version field. When updating, clients are guaranteed to read the latest version and resubmit the document after local modification. When a version conflict is encountered, the transaction should be redone.


Data Model 
Document / XML

Solr stores data as documents which consist of different fields. Each field contains a piece of more specific information about the document and can have different data types. Using the index of documents, Solr can provide efficient search.


Indexes 
Inverted Index (Full Text)

Solr adopts the inverted index which lists the terms of all documents, each with a list of documents it appears in and the number of occurrence. The inverted index allows faster query processing. Solr also supports DocValue which is a column-oriented field mapping documents to values to support features like sorting and faceting.


Isolation Levels 
Read Committed

In Solr, updates is not visible to searchers until it has been committed to the index. The default action for commit is a "hard commit" which writes all the affected index segments to disk. Solr also supports "soft commit" which only commits the changes to the Lucene data structures to realize Near Real Time (NRT) search. In NRT, documents are available for search soon after being indexed without the need to wait for various background tasks to finish.


Joins 
Hash Join Sort-Merge Join

Solr supports joins (that of typical relational database systems) through Streaming Expressions which is designed to perform parallel computing tasks in SolrCloud. In Solr, Streaming Decorator expressions provide two types of joins by wrapping two streams: hash join / outer hash join and left outer join / inner join which is implemented using the idea of Sort-Merge Join.


Logging 
Physical Logging

On each update, Solr writes the entire documents as transaction logs (tlog) to disk in order to achieve reliability and consistency. When doing soft commits, Solr only changes the Lucene data structures and write the tlogs. When doing hard commits, Solr will truncate the tlogs and create a new one since all the previously affected index segments have been written to the disk. When doing the recovery, Solr follows the tlogs to redo updates that have not been fsync’d (hard committed).


Query Compilation 
Not Supported

Query Execution 
Tuple-at-a-Time Model

Solr processes queries by examining each document a time. By computing a score for each document, Solr generates a ranking and returns results based on that.


Query Interface 
Custom API

In Solr, the REST interfaces provide easy integrating with many languages. Customers can initiate HTTP requests to send command to Solr and receive responses through Client APIs. These custom APIs handle the work of sending requests and parsing responses.


Storage Architecture 
Disk-oriented

Solr stores its index files on disk. Uncommitted updates will be kept in memory as a small buffer.


Storage Model 
Decomposition Storage Model (Columnar)

Solr stores data in inverted index which stores the documents containing the same term contiguously in a block of data. This is an efficient storage model for OLAP workloads since search can be processed quickly by scanning over some terms.


Stored Procedures 
Not Supported

It's not supported in Solr currently. But people have proposed different approaches to handle that.


System Architecture 
Shared-Nothing

Solr can split an index across multiple shards to distribute data and forms the shared-nothing system architecture. Each shard is a partition of the collection, containing a subset of the documents. Each document will be stored in exactly one shard. SolrCloud also supports automatic distribution for both documents and queries, and ZooKeeper provides load balancing.


Views
Not Supported