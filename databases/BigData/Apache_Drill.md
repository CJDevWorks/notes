Drill 
Drill is a database system designed for Big Data exploration. It is an open-source, distributed SQL query system based on Google's Dremel query system, and it features a columnar execution engine. Drill is the only distributed SQL engine in the world that does not require schemas. It supports the querying of many NoSQL databases and file systems, with the ability to join data from different types of datastores within the same query.


History 
In 2010, Google published a paper titled "Dremel: Interactive Analysis of Web-Scale Datasets" that described a scalable database system designed for "interactive analysis of nested data". This Dremel query engine is now available today under Google's BigQuery system. Development of Apache Drill began in 2012, with the goal of replicating the capabilities of Dremel. Initial goals of the system included support for multiple storage systems, file formats, query languages, and data sources, as well as the ability to scale over 10,000 servers and process petabytes of data in seconds.


Checkpoints 
Not Supported

Drill adopts optimistic query execution, which assumes that failures occur rarely during queries. Therefore, it does not take checkpoints. With its pipelined query execution model, single queries are simply reran when they fail.


Concurrency Control 
Optimistic Concurrency Control (OCC)

Drill supports Optimistic Concurrency Control. It plans queries in fragments, assuming that all of the fragments can be completed in parallel without interfering with each other. Larger fragments are broken into smaller fragments, which are run in clusters until the whole fragment is complete.


Data Model 
Column Family

Drill features a JSON self-describing data model that supports language independence and loosely defined, weak data typing. This data model uses on-the-fly schema discovery, also known as late binding, to begin the execution of queries without having to know the structure of the data. Through this data model, Drill can handle data with evolving schemas or even no schemas at all. Drill's internal data representation is columnar and hierarchical, which allows for efficient SQL processing without the need to flatten data into rows. The data model supports queries on complex/nested data as well as evolving data structures.


Foreign Keys 
Supported

Drill supports the usage of foreign keys within the schemas of the datastores that it gathers data from.


Joins 
Nested Loop Join Hash Join Sort-Merge Join Broadcast Join

Drill makes use of both distributed and broadcast joins to perform hash, merge, and nested loop join operations. In distributed joins, both sides of the join are hash distributed on one or more join keys. In broadcast joins, one side of the join is broadcasted to all other nodes in the join.


Parallel Execution 
Intra-Operator (Horizontal)

Drill supports parallel execution through intra-operator parallelism. Physical plans are split into phases called fragments. Large fragments, known as major fragments, are then split into minor fragments. The minor fragments run in parallel with each other, each in their own thread, until the major fragments, and eventually the plan, is fully complete.


Query Compilation 
Code Generation

Drill supports code generation and runtime query compilation. In fact, Drill is the only query engine in the world that both compiles and re-compiles queries at runtime, as part of its on-the-fly schema discovery that allows it to begin executing queries without knowing the structure of the data. Through this mechanism, queries are compiled during their execution phase.


Query Execution 
Vectorized Model

Drill supports a vectorized model of distributed query execution. This is due to its parallel execution design, in which queries are broken up into fragments of work. Together, these fragments compose a multi-level execution tree. The root fragment reads queries and table metadata, and then routes them to lower levels in the execution tree for execution to be processed in parallel. Partial results are passed up the tree level by level, with higher-level fragments performing further aggregation of these results, up until the completion of entire queries.


Query Interface 
SQL HTTP / REST

Drill supports the running of queries via industry standard ANSI SQL and RESTful APIs. Since data in the queries may be schema-less, Drill will implicitly convert this data into correctly-typed data in some cases. In other cases, casting the data is necessary, and the need for casting varies by query and data source.


Storage Architecture 
Hybrid

The overall storage architecture of Drill is a hybrid of in-memory and disk. Drill optimizes for columnar storage and execution by utilizing an in-memory data model that is both hierarchical and columnar. Query execution happens in memory as much as possible, persisting to disk only when there is memory overflow.


Storage Model 
Decomposition Storage Model (Columnar)

Drill supports an in-memory columnar data storage model. The design of this model allows for the optimization of in-memory, parallel query execution. It also provides an execution layer that performs SQL processing on this columnar data without the need for row materialization.


Stored Procedures 
Not Supported

Drill does not support stored procedures.


System Architecture 
Shared-Nothing

The core of Apache Drill is the "Drillbit" service. Drillbits are processes that accept query requests, execution queries, and return the results to the client. This query process is split over clusters of multiple Drillbits, which follow the shared-nothing architecture. Each Drillbit has its own cache and storage engine. When a query is issued, any one of the Drillbits in the cluster can accept it, turning this Drillbit into the "driving Drillbit". The driving Drillbit will parse the query optimize the query, and then generate a distributed query plan over the available Drillbits in the cluster. Together, these will each execute according to the plan and return data to the driving Drillbit, which ultimately returns the result to the client.