Neo4j 
Neo4j is a graph database that leverages data relationships as first-class entities. It provides ACID Transactions with online backups and high availability.


History 
Neo4j's first version was released in February, 2010 by Neo Technology in San Francisco. It is an ongoing project with the latest stable release 3.0 in April 2016. The idea behind developing Neo4j as a graph processing software was to store your relationships as first-class entities unlike NoSQL aggregate databases.


Checkpoints 
Non-Blocking

Neo4j can be backed up while it continues to serve user traffic (called “online” backup). Neo4j offers two backup options: full or incremental. These strategies can be combined to provide the best mix of safety and efficiency. Depending on the risk profile of the system, a typical strategy might be to have daily full backups and hourly incremental backups, or weekly full backups with daily incremental backups.


Concurrency Control 
Two-Phase Locking (Deadlock Detection)

Neo4j uses locks for transactions which may lead to deadlock. Deadlocks are detected and the transaction is marked for rollback. The transaction may be retried if needed by the user. The retry logic is left to the user.


Data Model 
Graph

Neo4j uses a Graph data model. The fundamental units which form a graph are nodes and relationships. This is stored with key-value style properties on both. Relationships connect two different nodes to each other, and are both typed and directed although we still have the flexibility to traverse the relationships in both the directions.


Foreign Keys 
Supported

The traditional notion of foreign keys in RDBMS is used in Neo4j as relationships.The simple abstraction of nodes and relationships in connected structures helps enable the concept of foreign keys in Neo4j.


Indexes 
B+Tree Inverted Index (Full Text)

Initially Neo4j did not support indexes however schema indexes were added in Neo4j 2.0, and automatically index labelled nodes by one or more of their properties. Those indexes are then implicitly used by Cypher as secondary indexes and to infer the starting point(s) of a query. As of Neo4j 3.5, indexes can also be used to skip sorting for ORDER BY clauses.


Isolation Levels 
Read Committed Serializable

Neo4j supports ACID Transactions and the default isolation provided is READ_COMMITTED. The user can however acquire locks on nodes and relationships to achieve the SERIALIZABLE isolation. Deadlock Detection is inbuilt in the system.


Joins 
Hash Join

NodeHashJoin API provided in the documentation joins the input coming from the left with the input coming from the right. The support for ValueHashJoins was also merged with the github Neo4j 3.0 repository.


Logging 
Logical Logging

Logical transaction logs in Neo4j are used in scenarios when the database needs to be recovered after a unclean shutdown. They are also used for online backup operations, especially for incremental backups. These transaction log files are rotated after surpassing a certain size (25 Mb in size). The amount of log files or the used space can be configured.


Query Compilation 
Code Generation JIT Compilation

Neo4j uses (byte) code generation in addition to JIT compilation. The JIT compilation is provided by the JVM.


Query Execution 
Tuple-at-a-Time Model

Query Interface 
Cypher

Cypher is a declarative, SQL-inspired language for describing patterns in graphs visually using an ascii-art syntax. One of the most powerful ability of Cypher is the notion to use the -> operator to define relationships.


Storage Architecture 
Disk-oriented

Neo4j has a disk-based, native storage manager optimised (optimisations typically revolve around using the cache effectively to avoid trips to the disk) for storing graph structures with maximum performance and scalability.


Storage Model 
Custom

Each node and its properties are stored on the disk using a doubly linked list. Layout : byte 0 : 4 high bits of previous, 4 high bits of next pointers, bytes 1-4 : previous property record, bytes 5-8 : next property record, bytes 9-40 : payload


Stored Procedures 
Supported

Stored procedures in Neo4j are called using Cypher calls. Arguments can be supplied directly within the query or taken from the associated parameter set. Procedures can be written in Java, compiled as jar files and put into the database as plugins.


System Architecture 
Shared-Nothing

Neo4j offers a shared-nothing architecture with a single write master and multiple read replicas thus consumes significant instance based storage.


Views 
Not Supported

Neo4j does not support the concept of views like traditional RDMS. However, one can create a special VIEW Node. Querying a view now implies querying the created view node, traversing the edges to find the results.