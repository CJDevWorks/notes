Redis 
Redis ("REmote DIctionary Server") is a networked, in-memory, key-value store that can be used as databases, cache or message broker. It supports storage of various types of data structures including strings, lists hashes and sets, as well as different kinds of queries on those data structures. Redis also provides support for on-disk persistent, Timed key expiration, LRU eviction of keys, asynchronous master-slave replication, automatic failover and transactions. Redis is mainly developed by Salvatore Sanfilippo and released under BSD liscence.


History 
Italian software engineer Salvatore Sanfilippo, creator and main contributor of Redis, first started redis project in early 2009. The initial purpose of Redis is to improve the performance of LLOOGG, the product of a startup by Salvatore Sanfilippo. By June 2009, Redis is stable and feature-rich enough so that Salvatore Sanfilippo deployed Redis to production environment and retired MySQL from LLOOGG. Community of Redis grew rapidly over the following several months, thanks to Salvatore Sanfilippo's effort of maintaining and improving the software and eventually, in March 2010, VMWare hired Salvatore Sanfilippo to work full-time on Redis. In 2013 and later in 2015, Salvatore Sanfilippo joined Pivotal Software and RedisLabs respectively, and these two companies became the main sponsorship of Redis.


Checkpoints 
Non-Blocking

administrators can configure Redis to take a snapshot of all stored key-value pairs at some pre-defined frequency, such as once every 5 minutes. During checkpointing, the main Redis process forks a child and it is the child's responsibility to dump all its data to a .rdb file on disk, while the parent process may continue processing client requests without blocking. Redis checkpointing allows faster recovery and usually does not hurt the performance since all the parent process needs to do is to call fork() and no disk I/O is involved for the parent. However, in the case where the dataset is large and the hardware is slow, the fork() call may take several milliseconds or even seconds and the parent process will freeze.


Concurrency Control 
Not Supported

There is no concurrency control protocol in Redis because it does not need one. Redis is mostly a single-threaded program, in the sense that at any given point of time, for a Redis server there can be at most one request being processed. In other words, requests are processed sequentially, excluding the needs for concurrency control. Redis is mostly single threaded as from version 2.4, there are additional threads to do some background work such as disk I/O, but the fact that requests are processed seretially is not changed.


Data Model 
Key/Value

Primarily used as a fast cache, Redis is a key/value store. Unlike a naive dictionary, Redis supports various value data types, including strings, hashes, lists, sets, ordered sets, as well as range queries, bitmaps, hyperloglogs and geospatial indexes with radius queries to operate on those data types. The key is always a binary-safe string


Indexes 
Hash Table

Redis implements its own in-memory hashtable as the container for key-value pairs.


Joins 
Not Supported

Redis is key/value store, you cannot do SQL joins on Redis.


Logging 
Command Logging

The logging mechanism of Redis is called AOF, or append only file. Redis logs every command issued by requests, and as long as the command take effect (makes changes to the data stored), a log entry will be generated and append to the AOF. Note that Redis does not log the effect(consequense) of the command, but the command itself (such as SET myKey 'myValue'). This contrasts the physical logging scheme of many relational database management systems such as MySQL. This is because Redis is single threaded and there is no concurrency control scheme involved, therefore by replying the log topdown we are guaranteed to restore the state of Redis server. AOF are flushed (fsync) to disk on the frequency defined by administrator. AOF files are often larger than the RDB (Redis snapshot) file


Query Compilation
Not Supported

Redis queries are run as they are, there are no code generation or JIT.


Query Interface 
Custom API

As a fast in-memory key/value store, Redis defines its own concise query interface called Redis commands. For example, to set a key 'mykey' with value 'Hello', you can issue command: SET mykey "Hello", optional parameters such as expiration time and set condition can also be provided. Redis also supports transactions where a client issue a group of Redis commands and request Redis server to execute them in an all-or-nothing manner. Such transaction typically started with a 'MULTI' command similar to SQL's 'BEGIN TRANSACTION', and then commands of this transaction are entered one by one, queued on the Redis server. Finally a 'EXEC' is issued and Redis try to run all the queued commands together.


Storage Architecture 
Hybrid

Redis is usually a in-memory data store but has the option to store data persistantly on stable storage such as disks. Redis supports two types of persistent storage: RDB (checkpoint or snapshot) and AOF (log actions).


Storage Model 
Custom

Redis implements its own hash map, and key/value pairs are inserted into this hashmap. The hash function is, by default, MurmurHash 2. And in each hash bucket, new items are placed at the beginning of the chain instead of the end.


Stored Procedures 
Not Supported

Redis does not officially support stored procedures, but since it provides a powerful commands 'EVAL', clients can store a Redis commands as string in Redis and EVAL it when needed. Details can be found in this link: link


System Architecture 
Shared-Nothing

Each Redis server is an autonomous, single threaded program that can process requests. You can also configure Redis clusters to improve the performance, storage capacity and availability. Redis clusters can automatically split dataset among Redis machines in the cluster but again each machine is self-contained and does not share anything with others.