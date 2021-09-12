DocumentDB
Amazon DocumentDB is a document database service that supports MongoDB workloads.


Data Model
Document / XML

Indexes 
Not Supported

Amazon DocumentDB supports various different types of indexes. Single field indexes are user-defined indexes on a single field of a document. Compound indexes are user-defined indexes on multiple fields of a document. Multikey indexes are indexes on array fields - although DocumentDB does not support this yet, its query planner can use multiple indexes in a single query, and so it can emulate a multikey index by creating an individual index for every desired array field. There are additional properties available for all indexes. The TTL property removes documents from collections after an interval of time specified by the user. The Unique property rejects duplicate values for indexed fields. The Sparse property skips documents which do not contain the desired field. The Background property builds the index in the background so that other applications are able to access data even when the index is being built.


Isolation Levels 
Not Supported

Within a single document, a write operation to a DocumentDB cluster is atomic. A read operation returns only data that was durable before the query execution started, and does not return any data that was modified after. Dirty reads are not possible.


Joins 
Not Supported

DocumentDB does not support joins (unlike MongoDB which supports the left outer join via the $lookup operator).


Logging 
Not Supported

Logging is done via AWS CloudTrail, which logs all API calls by the clients as events and makes the most recent events available on the CloudTrail console under 'Event history'. It is also possible to configure CloudTrail so that the logs are stored in an Amazon S3 bucket.


Query Interface 
Custom API Command-line / Shell

DocumentDB can be accessed using a Mongo shell to create, read, update and delete documents. It can also be accessed programmatically using the MongoDB drivers for Python, Node.js, PHP, Go, Java, and C#.


Stored Procedures 
Not Supported

Amazon DocumentDB does not support stored procedures, and unlike MongoDB it does not support stored javascript either.