Delta Lake 
Delta Lake is an open-source storage layer for big data workloads. It provides ACID transactions for batch/streaming data pipelines reading and writing data concurrently. Developed from Databricks, it is highly compatible with Apache Spark API and can be incorporated on top of AWS S3, Azure Data Lake Storage, or HDFS.


History 
Delta Lake is developed by Databricks in 2019, aiming to build a simple data pipeline unifying batch and streaming workloads. Delta architecture beyond Lambda architecture handles problems and bottlenecks in data flow systems.


Checkpoints 
Non-Blocking Consistent

Any changes to Delta Lake are stored in ordered, atomic commits in the transaction log. Each commit generates a JSON file. For every 10 commits, Delta Lake will automatically do a checkpoint by combining previous JSON files into a parquet file. Delta Lake maintains an increasing sequence number for JSON files in the transaction log, and takes a checkpoint asynchronously by getting the sequence number atomically and only scan the previous commit file for checkpointing. New writes will be written into a new commit file with a higher sequence number.


Compression 
Dictionary Encoding Run-Length Encoding Bit Packing / Mostly Encoding

Delta Lake stores data in Apache Parquet format and it can use the efficient compression and encoding schemes that are native to Parquet. Users can specify whether the cached data be stored in a compressed format.


Concurrency Control 
Multi-version Concurrency Control (MVCC) Optimistic Concurrency Control (OCC)

Delta Lake supports table-level transactions with ACID. Specifically, it provides serializable ACID Writes via Optimistic Concurrency Control and natively supports Snapshot Isolation for Reads via MVCC, which maintains different versions of the metadata file and does not remove old data files from disk until users do vacuum. Delta Lake does not support multi-table transactions.


Data Model 
Column Family

Delta Lakes is a storage layer that adopts column-oriented storage by embedding Parquet regardless of the choice of data model. Since DataFrame in Apache Spark contains a schema, Delta Lake supports schema enforcement and schema evolution.


Foreign Keys 
Not Supported

Delta Lake does not support foreign keys.


Indexes 
Hash Table

Delta Lakes have indexes on the table level stored as key/value metadata in JSON. To speed up reads, Delta lake can partition columns (of low cardinality) into separate files and look up the data via the metadata of the column and partition. If the column has a high cardinality, users could specify Z-ordering (multi-dimensional clustering) for optimization.


Isolation Levels 
Serializable Snapshot Isolation

Delta Lake provides serializable writes and snapshot isolation for reads. Delta Lake on Azure Databricks supports serializable, the strongest serialization level.


Joins 
Not Supported

Delta Lake does not support joins natively. But it provides parameters/hints of range join and skew join for the upper layer to tune. However, Delta Lake supports Merge and uses partition pruning to optimize that.


Logging 
Physiological Logging

Delta Lake records operations into its transaction logs that will be directly stored to disk. Delta Lake never allows writers to overwrite any log files. Writers can delete a file by appending logs with tombstones. In Delta Lake, transaction logs record the actions done to tables and also file paths to that table or column.


Query Compilation
Not Supported

Storage Architecture 
Disk-oriented

Delta Lake is disk-oriented and even delta cache can be stored on disk with less negative impact given high read speeds of modern SSD. In contrast, Spark cache uses memory.


Storage Model 
Decomposition Storage Model (Columnar)

Delta Lake uses versioned Parquet files which is columnar storage.


System Architecture 
Shared-Disk

Delta lake provides a storage layer on top of AWS S3, Azure Data Lake Storage, or HDFS, while Spark is a scalable compute engine for batch/streaming workloads. The storage layer and compute layer are decoupled.