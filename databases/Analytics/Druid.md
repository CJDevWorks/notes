Druid 
Apache Druid is an open-source distributed real-time analytics database designed for business intelligence (OLAP) queries on streaming and historical data. It is optimized for time series scans and aggregations. It supports loading data from both deep storage system like HDFS and streaming sources like Kafka. Internally, Druid uses Zookeeper for cluster node coordination, a relational database like MySQL or Postgres to keep track of metadata, and a deep storage system such as HDFS for storing data. Druid also has low latency between the event creation and when it can be queried, which makes Druid desirable for real-time analytics. Druid stores incoming data in a unique format called a segment to allow fast aggregations for arbitrary dimensionalities of data. Druid is commonly used to power GUI-based analytical BI apps via JDBC and as a backend for AI apps via REST API. Druid is also used for clickstream analytics, network telemetry analytics, application performance analytics, advertising analytics. It is used by various companies including Netflix, eBay, Airbnb, Twitch, GameAnalytics, Nielsen, PayPal and Alibaba.


History 
Druid was originally developed by engineers at Metamarkets to solve the problem of analyzing high dimensional data set in real-time. Scan and aggregation of billions of records in traditional relational databases are not fast enough, and pre-computing aggregations with NoSQL architecture requires unacceptably long processing time which creates high latency between event occurrence and its availability for querying. Druid was released in April, 2011 to address the need for fast, real-time analytics for high dimensional time series data. It was open sourced in Oct, 2012 and is under active development.


Concurrency Control 
Multi-version Concurrency Control (MVCC)

Data Model
Column Family

Indexes
B+Tree

Druid index documents into data segment when data are first ingested.


Joins 
Sort-Merge Join

Logging 
Not Supported

Query Compilation
Not Supported

Query Execution 
Tuple-at-a-Time Model Vectorized Model

Query Interface 
Custom API SQL HTTP / REST

Druid uses customized query interface expressed in JSON for metadata, aggregation and search. Druid provides support for SQL via Apache Calcite.


Storage Architecture 
Hybrid

Druid was built with all in-memory. However such choice is costly given large amount of data. It then switches to use a combination of memory and disk pages and allow users to customize the behavior.


Storage Model 
Decomposition Storage Model (Columnar)

Druid uses segments files to stores its index. A segment file is a basically a columnar storage model consists of three basic column types: timestamp columns, dimension columns and metric columns. This structure allows fast aggregation across different fields.


Stored Procedures
Not Supported

System Architecture 
Shared-Nothing

Views
Not Supported