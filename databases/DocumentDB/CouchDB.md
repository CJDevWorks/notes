CouchDB 
CouchDB ("cluster of unreliable commodity hardware") is a document-oriented NoSQL DBMS.


History 
CouchDB was created by Damien Katz in April 2005, it was initially written in C++ and used the GNU General Public License. CouchDB then discarded C++ and moved to Erlang for development in February 2006. CouchDB became an Apache Incubator project and converted its license to Apache License in February 2008. The beta version 0.10.0 of CouchDB published in October 2009. The CouchDB published 1.2.0 in April 2012, 1.3.0 in April 2013, 1.4.0 in August 2013, 1.5.0 in November 2013, 1.6.0 in June 2014. In September 2016, CouchDB published 2.0.0, the prime feature of this version is that it support for clustering, this work is originally done in the BigCouch project, and it was merged into the 2.0.0 version of CouchDB. The latest version of CouchDB is 2.3.0 in December 2018.


Checkpoints 
Non-Blocking

In CouchDB, any changes to a document simply appends a new record to the database file, it is always non-blocking to take a snapshot of the file system to get the latest version of the database.


Compression 
Naïve (Record-Level)

CouchDB does compaction operation to reduce the disk usage similar like the vacuum in SQLite. CouchDB support user-defined number of revisions. The compaction operations can either be manually triggered or automatically.


Concurrency Control 
Multi-version Concurrency Control (MVCC)

The CouchDB uses Multi-version Concurrency Control (MVCC) as the concurrency control policy for read operations, each clients sees a consistent snapshot during the read operation.


Data Model 
Document / XML

The data model in CouchDB is document using JSON format.


Indexes 
B+Tree

The documents in CouchDB are indexed by their name and sequence id, these index are organized by B-trees.


Isolation Levels 
Snapshot Isolation

In CouchDB, a read request will always see the most recent snapshot of the database at the time of the beginning of the request because of MVCC.


Joins 
Not Supported

The data in CouchDB are store as documents, which is unnecessary for joins operations. The way to replace join operation is to do denormalization or stored with related data in documents.


Logging 
Shadow Paging

CouchDB uses shadow paging as its logging method, it only does appending operations to the current database file, which provides the MVCC features.


Query Interface 
HTTP / REST

CouchDB provide RESTful HTTP API as its query interface.


Storage Architecture 
Disk-oriented

CouchDB store its data on disk and all update are synchronously flushed to disk.


Storage Model 
Custom

The storage model of CouchDB is simply a large file, this database file contains variable-length data chunks, and a custom file critical header. As the CouchDB is append-only, the header of the database file is in the tail of the file to be access or re-append by each append operation.


Storage Organization 
Copy-on-Write / Shadow Paging

CouchDB implements append-only B+Tree and uses copy-on-write method to update the database file as well as the index.


Stored Procedures
Not Supported

System Architecture 
Shared-Nothing

CouchDB can provide the same version of replica in different peer, therefore, woyeach peer can provide same data for user to access. They do not share anything.