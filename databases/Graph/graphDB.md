GraphDB 
GraphDB is a distributed RDF graph database that supports SPARQL queries. It is implemented as a Storage and Inference Layer over the RDF4J framework. It provides cluster support, and uses the TRREE engine for inference and reasoning. It also supports Lucene, Solr, and Elasticsearch connectors for fast aggregation searches.


History 
Ontotext and OWLIM started off within Sirma Group in its R&D division, where OWLIM was first developed. OWLIM comes from "OWL In Memory" since it was originally an in-memory database. Ontotext later spun off into its own business. OWLIM was then later renamed as GraphDB, after Ontotext acquired the rights from sones GraphDB, and is a commercial product.


Compression 
Naïve (Record-Level)

GraphDB uses the Snappy library to compress all masters and workers for replications.


Concurrency Control 
Timestamp Ordering

GraphDB supports transactions. GraphDB supports Timestamp Ordering Concurrency Control, where each transaction is given a timestamp and is queued based on its timestamp. Additionally, updating transactions do not block readers.


Data Model 
Triplestore (RDF)

GraphDB uses an RDF data model. The RDF data model describes the meaning of information and their relationships using triples. A triple is of the format subject-predicate-object and is a unique identifier.


Indexes 
Hash Table Patricia/Radix Trie

GraphDB supports several optional indices: predicate lists (subject-predicate and object-predicate), context indices, and literal indices, each optimized for different kinds of queries. These are implemented with hash tables. The GeoSPARQL plugin for GraphDB , which is used for geo-spatial data representation and querying, supports the quad prefix tree and geohash prefix tree for indexing.


Isolation Levels 
Read Committed

GraphDB supports the read committed isolation level, where an update is only visible to other users when it has been committed.


Joins 
Hash Join

GraphDB supports joins. RDF4J supports hash joins, and since GraphDB is implemented using the SAIL API over RDF4J, GraphDB uses RDF4J's query engines, and thus also supports hash joins.


Query Compilation 
Code Generation Stored Procedure Compilation

GraphDB allows users to define custom rulesets, which can be compiled using its internal rule compiler. The rulesets are used to generate java code and are then instantiated. These rulesets are similar to stored procedures.


Query Interface 
SPARQL

RDF4J supports SPARQL and SeRQL for RDF queries, and thus GraphDB supports these as well, since GraphDB is built on top of RDF4J.


Storage Architecture 
Disk-oriented

GraphDB supports a disk-oriented storage architecture, where all of the data is stored in disk files.


Stored Procedures 
Supported

GraphDB supports rulesets that are stored as .pie files and can be compiled and instantiated. These rulesets are similar to stored procedures and are used for inference.


System Architecture 
Shared-Everything

Every worker node has a copy of the repository, and updates are tried on one worker node and then propagated by the master to the other worker nodes. The master checks for synchronization between the worker nodes.


Views 
Virtual Views

GraphDB supports a Graph View interface which takes in SPARQL queries and retrieves data for the user, which is also visually shown.