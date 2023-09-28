# SystemDesign

### What is Consistent Hashing?
It is a technique for storing data in a distributed databases, Content delivery networks (CDNs), Load balancers etc wherein it assigns each server and object a position on a virtual ring structure (hash ring). When a client needs to store or retrieve an object, it calculates the hash of the object's key and then stores or retrieves the object from the server at that position on the hash ring.


### What is Sharding?
Sharding is a database partitioning technique that splits a large database into smaller, more manageable parts. These smaller parts are called shards. Sharding is used to improve the scalability, performance, and availability of databases. There are two main types of sharding: 
Horizontal sharding: Horizontal sharding splits the data in a database across multiple tables. Each table contains a subset of the data, and all of the tables have the same schema.
Vertical sharding: Vertical sharding splits the columns in a database across multiple tables. Each table contains a subset of the columns, and all of the tables have the same rows.


### What are Bloom Filters?
