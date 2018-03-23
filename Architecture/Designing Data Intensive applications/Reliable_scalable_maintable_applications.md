
1. Store Data - *Databases*.
2. Speed - *Caches*
3. Query, Search - *Search Indexes*
4. Async message communication between processes - *Stream processing*
5. periodicaly crunching large amount of data - *Batch processing*

Whats Redis(DB)? and Apache Kafka(message queues)? How redis provides message queue features and 
Kafka is providing database like durability?

Memcached as caching layer(Distributed Caching)

Full text search server - Elastic Search and Solr.

- How do you ensure that the data remains correct and complete, even when things go wrong internally?

- How do you provide consistently good performance to clients, even when parts of your system are degraded?
 
- How do you scale to handle an increase in load? 

- What does a good API for the service look like?

Non Software Factors -

including the skills and experience of the people involved, 

legacy system dependencies, 

the timescale for delivery, 

your organization’s tolerance of different kinds of risk, regulatory constraints, etc.

Reliable System or Fault tolerent system -

- what is it? Is there any metric involved or its absolute? 
System behaves correctly even when things(not any thing) go wrong(performing correct function at **desired level of performance**)
This is different for different systems. 
As per system requirement if the application is apple to meet user expectation in case of known failures then its fault tolerent.

- Whats difference between a fault and failure?
A fault is usually defined as one component of the system deviating from its spec, 
whereas a failure is when the system as a whole stops providing the required service to the user. 
It is impossible to reduce the probability of a fault to zero; 
therefore it is usually best to design fault-tolerance mechanisms that prevent faults from causing failures.

- Can faults be minimized to zero?
NO

How to make more fault tolerent/Reliable system?
1. Increase the rate of faults trigerring it deliberately and observe system performance (testing).
Randomly kill application. eg-Netflix Chaos Monkey.

2. Tolerate faults over preventing faults. In some situation you cant tolerate faults so its better to prevent it.
User accessing not authorized data etc...
