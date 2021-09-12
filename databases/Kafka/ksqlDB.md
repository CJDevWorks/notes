ksqlDB 
ksqlDB (Kafka SQL) is a streaming SQL engine that provides SQL interface to the streams in Apache Kafka. It is developed by Confluent Inc. and is built on the Kafka Streams API, which supports joins, aggregations, windowing and sessionization on streaming data. The data is stored in a Kafka cluster, which is a collection of Kafka brokers, segregated into topics. Each topic consists of a defined number of partitions, where each partition is an immutable sequence of messages. KSQL can be used as a library by applications to run SQL queries on top of the stream data stored in the Kafka cluster. As opposed to streaming systems like Spark Streaming which require using Java/Scala for development, KSQL provides a completely interactive, SQL only interface improving the ease of access. KSQL processes one message at a time, making it a true stream processing system instead of a micro-batching system. KSQL is licensed under the Confluent Community License


History 
Apache Kafka was created as a distributed publish-subscribe model streaming system, where messages are organized into topics, with each topic containing multiple partitions. Partitions are append-only log storage format, which are persisted to the disk, with user-specified replication. Kafka provides fundamental APIs called Producer and Consumer to produce and access data from Kafka topics respectively. Kafka Streams API was then developed on top of the Producer and Consumer APIs to simplify application development. The execution logic of the application is modeled into a topology of operations and processing nodes. Although simplified, the Streams API still requires the end-user to write application code in either Java/Scala. KSQL is the SQL engine created on top of the Kafka Streams API, which compiles the SQL queries into Stream topologies. This enabled the end-user to directly write SQL queries on the stream data without using Java/Scala. KSQL was rebranded as ksqlDB in 2019.


Checkpoints 
Not Supported

KSQL just provides a SQL interface for querying the data resident within a Kafka cluster. Hence, fault tolerance and resilience of the data is managed by the Kafka cluster rather than KSQL, by explicitly taking checkpoints.


Compression 
Naïve (Record-Level)

Kafka provides configuration for writing compressed data to the server, which is decompressed when processed by the consumer. Since data for a topic could be written by multiple producers, messages within a topic could be both compressed and non-compressed. Kafka supports GZIP, Snappy, and LZ4 compression schemes.


Data Model 
Relational Key/Value

The basic unit of storage in Kafka is a message, which consists of a key, value, timestamp, partition number and its offset in the partition. Key and value are just arrays of bytes, hence there is no restriction on the type of values they can hold. A schema can be associated with each topic, which is imposed upon the value part of the message. Hence, inherently it follows a key-value based model, with relational schema optionally enforced upon. KSQL provides two different concepts of organizing a topic's data, streams, and table. Messages within a stream are independent of each other and unbounded. A table, on the other hand, is a stateful entity where a new message is considered either as a new entry in the table or an update to the entry in the existing table with the same key. Hence, in the case of a KSQL table, the messages in the topic can be considered as a changelog/redo-log.


Foreign Keys 
Supported

Data in Kafka streams are organized as key-value pairs. On top of this, KSQL provides two important abstractions of the data, which are streams and tables. KSQL supports join operations between streams and tables based on the key but doesn't enforce any type of foreign key constraints.


Indexes 
Not Supported

KSQL queries are compiled to Kafka Streams topology, which basically process the entire stream of data using the provided logic. Data stored within Kafka as messages are append-only log storage and also don't support any indexing, resulting in KSQL not supporting indexing.


Isolation Levels 
Not Supported

KSQL only supports queries to read and process the Kafka stream data, which precludes the concept of isolation level. Although, the streams created during and after the completion of a KSQL query are accessible by the user based on the Access-Control-Lists (ACLs)


Logging 
Not Supported

KSQL doesn't implement any additional type of logging since it just provides a SQL layer on top of the streams in Kafka which themselves are distributed and fault-tolerant. The additional metadata that KSQL maintains is the state stores and meta store which is stored on RocksDB and Kafka topics respectively.


Query Compilation 
JIT Compilation

KSQL is an abstraction layer provided on top of the Kafka Streams API. The KSQL query is parsed into an abstract syntax tree, which combined with metadata is transformed into a logical plan. Currently, KSQL doesn't support any additional optimizations on the generated logical plan except predicate pushdown. The final logical plan is then compiled into a Kafka Streams topology based on the Kafka Streams API.


Query Execution 
Tuple-at-a-Time Model

Since messages are stored as append-only records in Kafka, the query execution model processes each of these messages in a tuple-at-a-time fashion. Although, inherent parallelism in query execution comes from the fact that the messages are stored in Kafka topics across partitions. Hence, messages in different partitions can be processed concurrently, provided intra-query parallelism.


Query Interface 
Custom API SQL Command-line / Shell

KSQL is a SQL-like query language with certain extensions for streams. As defined in the data model, tables and streams are the two major abstractions in KSQL. KSQL provides the following execution modes/interfaces: Interactive mode: Using command line interface or REST API Application mode: A list of queries can be provided as an input to the KSQL jar * Embedded mode: KSQL queries can be embedded within the statements of Kafka Streams API, similar to Spark SQL.


Storage Architecture 
Disk-oriented

Every message in the Kafka cluster is stored at the brokers on disks. In spite of disk-oriented storage, it performs comparably to in-memory message queues because Kafka only allows for sequential processing of messages, avoiding random disk access. Since Kafka is implemented in Java, instead of caching data on JVM heap, it relies on OS page cache and batching techniques for improved performance.


Storage Model 
N-ary Storage Model (Row/Record)

Messages in Kafka, which are the basic unit of data in KSQL are stored as records in an append-only log.


Storage Organization 
Log-structured

The basic unit of data in Apache Kafka is a message. Messages are organized into topics, with each topic split into a configurable number of partitions. A partition can be considered as a log that is immutable and append-only, with a guarantee that a message will be part of only one partition in a topic. The data is stored in a Kafka cluster, which is a distributed collection of Kafka brokers. Each partition has one leader broker and other replication/follower brokers for fault tolerance. Streams in KSQL are stateless entities, hence not requiring any additional state data. Tables, on the other hand, are stateful entities, and KSQL uses RocksDB for storing the state of the table. Any incoming message that updates the table will update this state store. Analogous to a catalog in an RDBMS, KSQL maintains a metastore that contains information about all the tables and streams in the Kafka cluster. This metastore itself can be configured to be stored as a Kafka topic for fault tolerance.


System Architecture 
Shared-Everything

Messages in Kafka are persisted to local disk storage of the Kafka brokers. The KSQL query is run independently to the Kafka broker cluster i.e. the KSQL queries are embedded within the application. Thus, KSQL queries are application logic written to access data residing in a separate fault-tolerant Kafka cluster.