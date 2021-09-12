Splunk 
Splunk is a database system designed for extracting structure and analyzing machine-generated data. It takes in data from other databases, web servers, networks, sensors, etc. and then offers services to analyze the data, and produce dashboards, graphs, reports, alerts, and other visualizations. All this data is captured in a searchable repository and served via a web interface called Splunk Web. Splunk is a horizontal application and is useful for many different kinds of users with different knowledge bases in an organization, such as monitoring IT operations, security, and performing business analytics. It is also possible to extend the Splunk environment by installing or developing an app. An app runs on the Splunk platform and includes inputs, lookups, and reports to display information about the data to add specific functionality.


History 
Splunk was founded by Erik Swan, Michael Baum, and Rob Das in 2002. Prior to founding Splunk, all three founders were dealing with large-scale search infrastructures and were unhappy about the tools available for analyzing log files at the time. Early customers of Splunk reported their experience of debugging their environments as ‘digging through caves’ and ‘crawling through the muck to find the problems’, which inspired the founders to name the company after the word for exploration of caves, spelunking.


Checkpoints 
Consistent

Splunk stores data in indexes organized in a set of buckets by age. The hot buckets contain data that is currently being written to. This is eventually rolled to the warm, cold, and frozen buckets. The hot bucket cannot be backed up, but Splunk provides the ability to create a consistent snapshot of the other buckets. This is done either using incremental ongoing backups (using the user's preferred snapshot utility) or a single backup of all data. Taking periodic snapshots from a healthy environment allows you to recover from the last valid checkpoint in the event of a catastrophic event.


Compression 
Naïve (Record-Level)

A Splunk index stores the raw data in compressed form along with index files that contain metadata that is used to search the event data. For indexes, it supports gzip (default), lz4, and zstd for compression and can handle different buckets compressed with different algorithms. Splunk calculates disk storage using the formula (daily average indexing rate) * (retention policy) * 0.5 because it compresses raw data to up to approximately "to approximately half its original size."


Concurrency Control 
Optimistic Concurrency Control (OCC)

Splunk has bucket locks that are used during file system consistency checks, deletions, and other operations that need to modify buckets after the hot phase. Locked buckets can still be searched but prevent these operations from conflicting.


Data Model 
Key/Value

Splunk is a NoSQL database management system with a key value store data mode. This allows users to retrieve data as collections of key-value pairs and perform Create-Read-Update-Delete (CRUD) operations on individual records.


Foreign Keys 
Supported

Splunk supports referential integrity. The correlate command can be used to return the co-occurrence between fields in data in a matrix format.


Hardware Acceleration 
GPU FPGA

FPGA and GPU can be used to accelerate Splunk's performance.


Indexes 
Inverted Index (Full Text)

Splunk adds all incoming data to indexes after processing it. It indexes data by breaking them into events, based on the timestamp. After breaking the data up into events, the events are passed through the indexing pipeline where additional steps are taken, such as breaking the events into segments so indexing and searching can be done efficiently, building data structures for the indexes, and writing the events out to disk. Splunk supports events and metrics indexes. Events indexes are the default index type, impose minimal structure, and can accommodate any type of data. Metrics indexes are highly structured and designed to handle high volume and low latency demands. These indexes have better performance and less space utilization compared to events indexes.


Isolation Levels
Not Supported

Joins 
Index Nested Loop Join

Splunk supports inner (default), outer, and left joins using the join command. It can also join a search result set with itself using the selfjoin command. Since Splunk stores all data in indices, it can use the index on the join attribute to combine the left and right-hand data.


Logging 
Not Supported

Splunk does not support recovery logging. Disasters are recovered from by restoring from backups or archives of frozen data.


Parallel Execution 
Intra-Operator (Horizontal) Inter-Operator (Vertical)

Splunk supports intra-operator parallelism for high cardinality searches. It also supports concurrent search but limits the number in order to preserve performance. It allows you to configure the maximum number of concurrent searches between scheduled and summarization queries based on your usage. Splunk also supports concurrent users. A user uses exactly one CPU core on each indexer for the duration of the search. By default, a search on Splunk cannot use multiple cores.


Query Execution 
Vectorized Model

Splunk uses MapReduce to speed up searches. Unlike typical implementations where there is a map phase and only one reduce phase, Splunk introduces an intermediate reduce phase to this paradigm, which serves as intermediate reducers. In the map phase, Splunk finds matching event data using the indexers. During the reduce phase, the sorted field-value pairs are processed processed and aggregated to produce a final result set by the search heads.


Query Interface
Custom API

Storage Architecture 
Disk-oriented

Splunk is disk-oriented.


Storage Model 
N-ary Storage Model (Row/Record)

Splunk stores data in a flat file format. All data in Splunk is stored in an index and in hot, warm, and cold buckets depending on the size and age of the data. It supports both clustered and non-clustered indexes.


Stored Procedures 
Supported

The dbxquery command in Splunk DB Connect allows executing stored procedures. The SQL explorer is used to edit and write the queries.


System Architecture 
Shared-Nothing Shared-Disk

Splunk supports distributed search. Independent search heads can manage search queries for independent indexers. Indexer clusters have many indexers replicate the same data for high availability, with a master node that controls the queries. Search head pooling is a distinct topology in which the search heads share storage for configuration and user data, though it is being deprecated.


Views
Not Supported

Splunk does not support database views.