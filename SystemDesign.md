# SystemDesign


# Latency Numbers in System Design

"Latency numbers" refer to the typical time delays encountered in various operations within a computer system or network. These numbers help engineers and developers understand the relative costs of different operations and optimize system performance.

A common way to express these numbers is through an analogy that compares them to real-world time scales, giving a sense of the magnitude of delays. Below are some typical latency numbers for a modern computer system (circa 2020s):

## Example Latency Numbers (Scaled for Intuition)

1. **L1 Cache Reference**: ~0.5 nanoseconds (ns)
   - Equivalent to: 1 second.

2. **L2 Cache Reference**: ~7 ns
   - Equivalent to: 14 seconds.
   - 
3. **Main Memory Reference (DRAM)**: ~100 ns
   - Equivalent to:  3 minutes.

4. **SSD Random Read**: ~150 microseconds (µs)
   - Equivalent to:  5.8 hours.

5. **Rotational Disk Random Read**: ~5-10 milliseconds (ms)
   - Equivalent to: 1 to 2 days.

6. **Network Round Trip (Same Data Center)**: ~500 µs
   - Equivalent to: Equivalent to: 20 days.

7. **Network Round Trip (Cross Country)**: ~75 ms
   - Equivalent to:  4 to 8 years

8. **Network Round Trip (International, e.g., US to Europe)**: ~150 ms
   - Equivalent to: 10 to 20 years.

9. **Sending 1KB over a Network**: ~1 ms
   - Equivalent to:  1 to 2 months.

10. **Context Switch between Processes**: ~5 µs
    - Equivalent to:  2 hours.
    - 
## Why These Numbers Matter

- **System Optimization**: Understanding these latency numbers is crucial for system design, as they help engineers make trade-offs between different types of operations. For example, avoiding disk access in favor of keeping data in memory can drastically improve performance.

- **Performance Tuning**: When tuning performance, knowing which operations introduce significant delays allows developers to focus optimization efforts where they will have the most impact.

- **Architectural Decisions**: These numbers can also guide architectural decisions, such as whether to cache data locally, how to design distributed systems, or whether to parallelize certain operations.

Understanding these latency numbers provides a valuable perspective when designing and optimizing computer systems, allowing for more informed decisions about where to invest time and resources for performance improvements.

# Availability Number 

| Availability Percentage | Downtime per Year         | Downtime per Month         | Downtime per Week         |
|-------------------------|---------------------------|----------------------------|---------------------------|
| **90% ("one nine")**     | ~36.5 days                | ~72 hours                  | ~16.8 hours               |
| **99% ("two nines")**    | ~3.65 days                | ~7.2 hours                 | ~1.68 hours               |
| **99.9% ("three nines")**| ~8.76 hours               | ~43.2 minutes              | ~10.1 minutes             |
| **99.99% ("four nines")**| ~52.6 minutes             | ~4.32 minutes              | ~1.01 minutes             |
| **99.999% ("five nines")**| ~5.26 minutes            | ~25.9 seconds              | ~6.05 seconds             |
| **99.9999% ("six nines")**| ~31.5 seconds            | ~2.59 seconds              | ~0.605 seconds            |

# Estimate QPS and media storage 
####  Query per second (QPS) 
|Data|Usage|
|---|---|
|Monthly Active Users|300 Million|
|Daily Users| 50%|
|Avg Tweets per user|2 Tweets per day|
Tweets containing media|10%|
|Tweets storage span|5 years|

Daily active users -> 150 Million 

Average Tweets per user -> 150 x 2/(24x60x60) =  3472.22 tweets per second ~ 3500 tweets per second

Hence, QPS -> 3500 QPS

Peak QPS (100% Users) -> 3500 x 2 = 7000 QPS
 #### Storage Requirement Estimation
 |AVG Tweet Size|Size|
|---|---|
|Tweet_Id| 64 bytes|
|Text|140 bytes|
|Media|1 MB|

Media storage ->  3500 tweet/sec x 10% x 1 MB = 350 MB/Second = (350/(1/24x60x60)) 3,02,40,000 MB/day ~ 30 x 10^6 MB/day ~ 30 terabyte/day

5 Year media storage -> 5 Year x 365 day x 30 TB/Day = 54750 TB ~ 55 Petabyte

### What is Consistent Hashing?
It is a technique for storing data in a distributed databases, Content delivery networks (CDNs), Load balancers etc wherein it assigns each server and object a position on a virtual ring structure (hash ring). When a client needs to store or retrieve an object, it calculates the hash of the object's key and then stores or retrieves the object from the server at that position on the hash ring.


### What is Sharding?
Sharding is a database partitioning technique that splits a large database into smaller, more manageable parts. These smaller parts are called shards. Sharding is used to improve the scalability, performance, and availability of databases. There are two main types of sharding: 
Horizontal sharding: Horizontal sharding splits the data in a database across multiple tables. Each table contains a subset of the data, and all of the tables have the same schema.
Vertical sharding: Vertical sharding splits the columns in a database across multiple tables. Each table contains a subset of the columns, and all of the tables have the same rows.


### What are Bloom Filters?
 x 
