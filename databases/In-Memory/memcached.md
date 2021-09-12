Memcached 
Memcached (pronunciation: mem-cash-dee) is a distributed in-memory key-value storage system, usually used for caching objects in memory to speed up database applications. Typically, users wrap database queries with Memcached get/set operations to cache recently-used objects.


History 
Memcached was originally developed by Brad Fitzpatrick from Danga Interactive for LiveJournal. It was originally written in Perl, but is rewritten in C by Anatoly Vorobey. Now Memcached is used widely in many systems, including YouTube, Twitter, Facebook, and Wikipedia. It is also provided in many cloud platform services, including Google App Engine, Microsoft Azure, and Amazon Web Services.


Concurrency Control 
Not Supported

Memcached doesn't have the concept of transactions. The get/set operations are atomic, though. For example, multiple sets on the same key can be issued concurrently, but only the last will stay.


Data Model 
Key/Value

Memcached servers maintain a key-value map. Keys are up to 250 bytes long and values are up to 1 MB large. There are no relational schemas.


Indexes 
Hash Table

Memcached stores a key-value hash table on every server. As of May 2017, it uses MurmurHash 3 as the hash function.


Joins 
Not Supported

Memcached only supports get/set and related operations on a key-value store. There is no support for SQL queries. Therefore, there is no need to support joins.


Logging 
Not Supported

There is no logging in Memcached, since it is intended for being a caching system. The cache is not persistant between restarts.


Query Compilation 
Not Supported

Memcached only supports get/set and related operations on a key-value store. There is no support for SQL queries. Therefore, there is no need for query compilation.


Query Execution 
Tuple-at-a-Time Model

Query Interface 
Custom API

Memcached provides get/set and related operations. It also allows users to specify how long a cache item should last.


Storage Architecture 
In-Memory

In Memcached, everything is stored in memory, since it is intended for caching objects stored in a disk-oriented database. By storing everything in memory, it achieved the needed latency and speed. The cache is not persitent between restarts, which is an intended feature.


Storage Model 
Custom

Memcached stores a hash table. As of May 2017, it uses MurmurHash 3 as the hash function. Values items are slab-allocated.


Stored Procedures 
Not Supported

Memcached only supports get/set and related operations on a key-value store. There is no support for SQL queries. Therefore, there is no need to support stored procedures.


System Architecture 
Shared-Nothing

In Memcached, a client knows all servers. Servers do not communicate with each other. Each key is hashed to determine which server is used to store the key-value pair. If all clients use the same hash function, then a client can read other clients' cached data.


Views 
Not Supported

Memcached only supports get/set and related operations on a key-value store. There is no support for SQL queries. Therefore, there is no need to support views.