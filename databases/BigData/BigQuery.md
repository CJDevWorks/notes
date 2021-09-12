BigQuery 
BigQuery is a cloud-based interactive query service for large datasets. It is built upon Google's Dremel, a scalable query system for analysis of read-only nested data. It uses columnar storage representation for nested records and tree architecture for fast query execution.


Data Model 
Document / XML

BigQuery/Dremel uses a variation of the complex value models and nested relational models. It supports strongly-typed nested records. Records consist of one or multiple fields. Each field is an key-value pair and the key can be repeated. Each fielded can be of type required or optional and must be defined in the schema. A required field must appear exactly once.


Query Interface 
SQL

BigQuery/Dremel is based on SQL. The language supports nested subqueries, inter and intra-record aggregation, top-k selection, joins, regular expression matching and user-defined functions.


Storage Architecture 
Disk-oriented

All the data are assumed to be stored in disk or other storage layer can be piped in. In the multi-level serving tree for query execution, all the leaf servers are responsible for communication with the storage layer or access the data on local disk.


Storage Model 
Decomposition Storage Model (Columnar)

BigQuery/Dremel uses a columnar storage for the nested records. Based on the schema, it will encode the record structure in a columnar format. Each column is stored as a set of blocks. Each block contains the compressed field values, repetition and definition levels. Repetition level indicates at what repeated field in the field's path the value has repeated. Definition level specifies how many fields in the path that could be optional or repeated are actually present. With these two levels and the schema, it can represent the record structure losslessly.


System Architecture 
Shared-Nothing