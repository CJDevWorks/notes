Prometheus 
Prometheus is an open-source time series database developed by SoundCloud, and serves as the storage layer for the Prometheus monitoring system. Inspired by the Gorilla system at Facebook, Prometheus is specially designed for monitoring and metric collection. Prometheus contains a user-defined multi-dimensional data model and a query language on multi-dimensional data called PromQL. Apart from local disk storage, Prometheus also has remote storage integrations via Protocol Buffer. Prometheus is written in Go and supports Go/Java/Ruby/Python clients. Prometheus also has unofficial client bindings for other programming languages.


History 
Prometheus was started in at SoundCloud as an open-source project for system monitoring, therefore the system requires an efficient and fault-tolerant storage layer for incoming metrics as well as metadata for these metrics. Thus, they built the Prometheus time series database as the backend for the whole monitoring platform. The Prometheus time series database has gone through three major versions. Prometheus v1 is a basic implementation, where all time series data and label metadata are stored in LevelDB. V2 addressed several shortcomings of v1 by storing time series data on a per time series basis and adoption of delta-of-delta compression. V3 made further improvements by implementing write ahead logging and better data block compaction.


Checkpoints 
Non-Blocking Consistent

Prometheus supports periodic checkpoints, which is done every two hours by default. Checkpoints in Prometheus is done by compacting write ahead logs in the most recent time range and include the latest checkpoint if it exists. All the checkpoints are stored in the same directory with the name checkpoint.xxx, where the xxx suffix is a number monotonically increasing. Therefore when Prometheus recovers from crash, it can restore the checkpoints in the checkpoint directory with the order as the suffixes.


Compression 
Delta Encoding

Since each metric data sample in Prometheus can be viewed as a tuple of a timestamp and a numerical value, therefore Prometheus has different compression techniques for timestamps and value respectively. For the compression of timestamps, the algorithm that Prometheus uses is similar to that of Facebook's Gorilla time-series database, called the delta-of-delta compression algorithm. For example, given a series of timestamp 1496163646, 1496163676, 1496163706, 1496163735, 1496163765, storing this timestamps in raw bytes are not efficient since these values only change very little over time. A better approach is to encode timestamp with deltas, i.e. 1496163646, +30, +30, +29, +30. Due to the fact that metrics usually come in a constant rate, Prometheus adopts the delta-of-delta encoding, i.e. 1496163646 +30 +0 -1 +1. If metrics come in a constant rate, then most of these delta-of-deltas will become 0. In addition to timestamp compression, Prometheus also compresses numerical values. Its approach is similar to existing floating point compression algorithms. The idea is that the XOR value of neighboring floating point data in a time series often has clustered 0s. Therefore the compression algorithm leverages this fact to compress numerical values. With regard to integration with remote storage engines, Prometheus uses a snappy-compressed protocol buffer encoding over HTTP for both read and write protocols.


Concurrency Control
Not Supported

Data Model 
Key/Value

Prometheus stores data as time series. A time series is defined by a metric and a set of key-value labels. Therefore a time series can be formally defined as <metric>{<label_1>=<value1>, <label_2>=<value2>...}. A data sample in a time series contains a float64 value, a unix timestamp, and the label values for this metric. Prometheus supports the following metric types: - Counter: monotonically increasing/decreasing data, e.g. the number of requests. It supports Inc() and Add(float) operations. - Gauge: numeric data point, e.g. CPU usage. It supports Set(float), Inc()/Dec(), Add(float)/Sub(float), and SetToCurrentTime() operations. - Histogram: samples in a given time range, e.g. request latencies. It supports Observe(float) operation. - Summary: similar to histogram, but only stores quantile data. Its supports Observe(float) operation.


Indexes 
Inverted Index (Full Text)

In Prometheus, a series can have queries on a particular label value. Therefore it is necessary to build an index that returns a list of series data samples given a label value. Prometheus uses inverted indexes for this purpose. For example, given a time series tcp_packets_total{source_ip}, if a query will fetch all the data samples where "from_ip=127.0.0.1", it does not have to iterate through all the series. On the other hand, it can directly get all the series with the label "from_ip=127.0.0.1" by a single query to the inverted index. With respect to the index on the timestamp dimension, Prometheus partitions tables horizontally based on timestamps into non-overlapping blocks. Therefore, each block contains the data for the series in that time window. For a timestamp query over a series, Prometheus does a sequential scan over the blocks of the series.


Joins
Not Supported

Logging 
Physical Logging

Prometheus ensures data durability by write ahead logging (WAL). The format of how logs are stored on disk in Prometheus is largely inspired by LevelDB/RocksDB. A data sample's log record is a triple (series_id, timestamp, value), therefore Prometheus does physical logging.


Query Compilation
Not Supported

Query Execution 
Tuple-at-a-Time Model

Prometheus internally use a SeriesIterator to fetch series samples from disk.


Query Interface 
HTTP / REST PromQL

Prometheus has a custom query language called PromQL, which is specially designed to query time-series data. Prometheus query interface also implements math/datetime related functions as well as aggregation. Prometheus also provides a RESTful interface over HTTP.


Storage Architecture 
Disk-oriented

Prometheus supports two storage architectures. The first is local disk storage: data are compressed and stored on local disk. The second is remote storage: Prometheus supports third-party storage (e.g. Kafka, PostgreSQL, Amazon S3) via ProtoBuffer adaptor.


Storage Model
N-ary Storage Model (Row/Record)

The underlying data representation of each series in Prometheus is a list of key-value pair.


Storage Organization
Sorted Files

Prometheus maintains database files under the trunk directory. Each file contains metadata of the min/max timestamps of the data samples in the file. Timestamps in all the files jointly comprises the whole time series.


Stored Procedures
Not Supported

System Architecture 
Shared-Disk

Prometheus supports flexible configuration to choose backend storage service. Prometheus itself maintains a on-disk checkpoint of series data and also supports remote read/write to other storage systems, making Prometheus's integration with other systems much easier.


Views
Not Supported