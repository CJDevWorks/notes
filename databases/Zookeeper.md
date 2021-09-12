Zookeeper 
ZooKeeper is a distributed, open source coordination service from Apache for distributed applications. Distributed applications can build upon it to implement higher level services for synchronization, groups and naming, and configuration maintenance. It is often used as a fault-tolerant storage for meta-data in large-scale distributed systems. ZooKeeper is used by companies including Yelp, RackSpace, Yahoo!, Reddit, Facebook, and Twitter.


History 
ZooKeeper was originally developed at Yahoo! to streamline the processes running on big data clusters. It was developed to fix the bugs that occurred while deploying distributed big-data applications. It started out as a sub-project of Hadoop, but became a standalone Apache Foundation project in 2008.


Checkpoints 
Fuzzy

Zookeeper stores fuzzy snapshots of the data tree in a data directory.


Concurrency Control 
Not Supported

Zookeeper guarantees sequential consistency and atomicity, and does not allow concurrent writes.


Data Model 
Hierarchical

The namespace in ZooKeeper is similar to that of a standard file system. A name is a sequence of path elements separated by a slash, and every node in ZooKeeper's namespace is identified by a path. Each node can have data associated with it as well as children. The term znode refers to ZooKeeper data nodes. Znodes include version numbers for data changes; every time a znode's data changes the version number increases. The data stored in each znode is read and written atomically.


Isolation Levels 
Not Supported

Query Interface 
Command-line / Shell

ZooKeeper Command Line Interface interacts with the ZooKeeper ensemble to perform simple, file-like operations for debugging purposes.


Storage Architecture 
In-Memory

ZooKeeper servers each keep their state machine in memory, and write every mutation to a durable WAL (Write Ahead Log) on storage media. If a server crshes it can replay the WAL to recover its previous state.


Stored Procedures 
Not Supported

System Architecture 
Shared-Nothing

ZooKeeper follows a client-server model where clients are the nodes (machines) that make use of the service, and servers are the nodes that provide the service. The client library is responsible for the interaction between clients and ZooKeeper servers. ZooKeeper servers run in two modes: standalone and quorum. In standalone mode there is a single server, and the ZooKeeper state is not replicated. In quorum mode, a group of ZooKeeper servers--each of which maintains an in-memory database containing the entire data tree of state as well as a transaction log and snapshots stored persistently--replicates its state and serves client requests. This group of servers is called an ensemble. As long as a majority of the ensemble is up the service will be available. . Each client imports the client library. Every ZooKeeper client is connected to one ZooKeeper server, which can handle multiple client connections at the same time. The client periodically sends pings to the server it is connected to. The server responds with an acknowledgement of the ping to indicate that it is alive as well. If the client does not receive an acknowledgment within the specified time, the client connects to another server in the ensemble, and the client session is transferred over to the new server.