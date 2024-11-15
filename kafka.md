# Kafka

#### Default Port for :: 
Zookeeper :: 2181
Kafka Server / Broker :: 9092
#### To Start Zookeeper followed by Kafka Server (Windows)
```
 .\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
 .\bin\windows\kafka-server-start.bat .\config\server.properties
```
#### To Create Topic
```
 .\bin\windows\kafka-topics.bat --bootstrap-server localhost:9092 --create --topic shivam-topic --partitions 3 --replication-factor 1
// Herein we are defining the kafka server port with topic name and partitions and replication factor 
```
#### To List Topics
```
 .\bin\windows\kafka-topics.bat --bootstrap-server localhost:9092 --list
```
#### To Describe any Particular Topic 
```
 .\bin\windows\kafka-topics.bat --bootstrap-server localhost:9092 --describe --topic  shivam-topic
```
#### To Create Producer 
```
 .\bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic shivam-topic
// herein we are producing and consuming from the same topic. 
```
#### To create Consumer 
```
 .\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic shivam-topic --from-beginning
```
#### To run the kafka server without ZooKeeper. (Kraft post 3.3 version is production ready)
""""""POST 4.0 version Zookeerper support will be completely removed"""""""""""""""""""
When running Kafka without ZooKeeper, it operates in what is known as KRaft mode (Kafka Raft mode). In this mode, Kafka uses an internal consensus protocol called Kafka Raft (Algorithm) (KRaft) to manage metadata within broker and handle leader election tasks that were previously managed by ZooKeeper. 
It can be done using Kraft using following steps: 
1. Create some UUID either using some online generator or command.
2. Using this uuid to create some kraft logg directory. 
```
 .\bin\windows\kafka-storage.bat format --standalone -t <UUID> -c .\config\kraft\reconfig-server.properties
 .\bin\windows\kafka-storage.bat format --standalone -t "f2381f67-755e-4ac0-aea6-99bdd9653bd4" -c .\config\kraft\reconfig-server.properties
```
3. Start the kafka server directory
```
 .\bin\windows\kafka-server-start.bat .\config\kraft\reconfig-server.properties
```
#### To Decode log file, we can use kafka-dump-log.bat  
```
..\..\..\kafka_2.12-3.9.0\bin\windows\kafka-dump-log.bat --cluster-metadata-decoder --files .\00000000000000000000.log --print-data-log
```
#### To check the status of cluster (Kafka metadata quorum)
```
 .\bin\windows\kafka-metadata-quorum.bat --bootstrap-server localhost:9092 describe --status
```
#### To run the kafka and zookeeper as the docker container (Docker Compose File). 
```
version: '3'
services:
  zookeeper:
    image: wurstmeister/zookeeper
    container_name: zookeeper
    ports:
      - "2181:2181"
  kafka:
    image: wurstmeister/kafka
    container_name: kafka
    ports:
      - "9092:9092"
    environment:
      KAFKA_ADVERTISED_HOST_NAME: localhost
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
```

## Kafka Integration with Spring-boot
#### Application.properties for producer
```
spring.kafka.producer.bootstrap-servers=localhost:9092
spring.kafka.producer.key-serializer= org.apache.kafka.common.serialization.StringSerializer
spring.kafka.producer.value-serializer= org.springframework.kafka.support.serializer.JsonSerializer
```

#### Application.properties for consumer
```
spring.kafka.consumer.bootstrap-servers=localhost:9092
spring.kafka.consumer.group-id=myGroup
spring.kafka.consumer.key-deserializer=org.apache.kafka.common.serialization.StringDeserializer
spring.kafka.consumer.value-deserializer=org.springframework.kafka.support.serializer.JsonDeserializer
```
#### Service 
```
    @Autowired
    KafkaTemplate< String, Object> kafkaTemplate;
    
    public void pubishMessage(String message){
        CompletableFuture<SendResult<String, Object>> publishMessage = kafkaTemplate.send("mytopic", message);
        publishMessage.whenComplete((res, ex) -> {
           if(ex==null){
               System.out.println(res.getRecordMetadata().toString() +" "+ res.getRecordMetadata().topic());
           } else {
               System.out.println(ex.fillInStackTrace());
           }
        });
    }
```
```
    @KafkaListener(topics="mytopic")
    public void consumeMessage(String message){
        System.out.println(message);
    }
```

## Kafka Configuration
Configuring storage in a Kafka server involves setting parameters in the `server.properties` file (or equivalent configuration file) that control how Kafka uses disk space, stores data, and manages log files. Here’s a detailed guide on defining and managing storage for a Kafka server:

### 1. **Log Directory**
   - The storage location where Kafka stores topic data is known as the **log directory**. Each topic's partitions will have corresponding log files stored in this directory.
   - You can specify one or more directories for Kafka to store data using the `log.dirs` property.

#### Example:
```properties
log.dirs=/var/lib/kafka/data
```

- If you have multiple disks, you can use a comma-separated list to specify multiple directories:
```properties
log.dirs=/var/lib/kafka/data1,/var/lib/kafka/data2
```

- Kafka will automatically balance partitions across these directories.

### 2. **Log Retention Settings**
   - Kafka allows you to manage how much data is stored by defining **retention policies** based on time, size, or a combination.

#### Key Retention Properties:
1. **`log.retention.hours`**: Sets the maximum time Kafka will retain a log before deleting it. Default is 168 hours (7 days).
   ```properties
   log.retention.hours=168
   ```
   - You can use `log.retention.minutes` or `log.retention.ms` for more granular control.

2. **`log.retention.bytes`**: Sets the maximum size (in bytes) that a log can grow before Kafka starts deleting the oldest segments.
   ```properties
   log.retention.bytes=1073741824  # 1 GB per partition
   ```
   - If set to `-1`, there is no size limit, and data is retained based on time only.

### 3. **Segment Size Configuration**
   - Kafka breaks down logs into smaller **segments** for better manageability. Segments are individual files on disk within each partition.

#### Key Segment Properties:
1. **`log.segment.bytes`**: Defines the maximum size (in bytes) for a single log segment file. When the segment reaches this size, Kafka creates a new segment.
   ```properties
   log.segment.bytes=1073741824  # 1 GB per segment
   ```
   - A smaller segment size can be beneficial for frequent compaction and deletion.

2. **`log.segment.ms`**: Defines the maximum time before a new segment is rolled out, regardless of size.
   ```properties
   log.segment.ms=604800000  # 1 week (in milliseconds)
   ```

### 4. **Log Cleanup Policies**
   - Kafka offers different strategies for cleaning up old data, depending on the use case:

#### Key Cleanup Properties:
1. **`log.cleanup.policy`**: Controls how log segments are deleted. There are two main options:
   - `delete` (default): Old segments are deleted based on the retention policy.
   - `compact`: Kafka retains the latest record for each key, removing older duplicates.
   ```properties
   log.cleanup.policy=delete
   ```
   
2. **`log.cleaner.enable`**: Enable or disable log compaction (used when `log.cleanup.policy=compact`).
   ```properties
   log.cleaner.enable=true
   ```

### 5. **Disk Usage and Quotas**
   - To prevent Kafka from exhausting disk space, you can configure quotas and triggers.

#### Key Quota Properties:
1. **`log.dir.size.management.enable`**: Controls whether Kafka should monitor the disk usage of `log.dirs`. If set to `true`, Kafka will delete older data when it reaches the configured size.
   ```properties
   log.dir.size.management.enable=true
   ```

2. **`log.dirs.size.limit`**: Configures the size limit for each `log.dirs`. When this limit is reached, Kafka will start deleting old data.
   ```properties
   log.dirs.size.limit=10737418240  # 10 GB per directory
   ```

### 6. **Recovery and Flush Policies**
   - Kafka can periodically **flush** data to disk to ensure durability and manage memory usage.

#### Key Flush Properties:
1. **`log.flush.interval.ms`**: Specifies the interval (in milliseconds) at which logs are flushed to disk.
   ```properties
   log.flush.interval.ms=1000  # Every second
   ```

2. **`log.flush.interval.messages`**: Flush after a certain number of messages.
   ```properties
   log.flush.interval.messages=10000
   ```

3. **`log.recovery.offset.gap.bytes`**: Defines the maximum number of bytes between the high-watermark (the last committed offset) and the log end offset before forcing a log recovery.
   ```properties
   log.recovery.offset.gap.bytes=10485760  # 10 MB
   ```

### 7. **I/O Optimization**
   - Disk I/O can be optimized by tuning how Kafka writes data to the filesystem.

#### Key Optimization Properties:
1. **`num.recovery.threads.per.data.dir`**: The number of threads for log recovery in each log directory.
   ```properties
   num.recovery.threads.per.data.dir=4
   ```

2. **`num.io.threads`**: The number of threads for handling I/O tasks.
   ```properties
   num.io.threads=8
   ```

### Example Configuration Summary for `server.properties`
Here’s a sample configuration snippet for managing storage in `server.properties`:

```properties
# Log directories (multiple directories for better I/O performance)
log.dirs=/var/lib/kafka/data1,/var/lib/kafka/data2

# Retention policies
log.retention.hours=168            # Retain data for 7 days
log.retention.bytes=1073741824     # 1 GB per partition

# Segment size
log.segment.bytes=1073741824       # 1 GB per segment

# Log cleanup policies
log.cleanup.policy=delete
log.cleaner.enable=true

# Flush data to disk frequently for durability
log.flush.interval.ms=1000         # Flush every second
log.flush.interval.messages=10000  # Flush every 10,000 messages

# Disk usage limits and quotas
log.dir.size.management.enable=true
log.dirs.size.limit=10737418240    # 10 GB per log directory

# Recovery settings
num.recovery.threads.per.data.dir=4
```

### Recommendations
1. Use **multiple log directories** if you have multiple disks to distribute load.
2. Set appropriate **retention policies** to manage disk usage and avoid running out of space.
3. Monitor **disk usage** regularly, especially in a production environment.
4. Ensure that **segment sizes** and **flush policies** align with your use case to balance performance and durability.

By configuring these properties properly, you can fine-tune how Kafka handles storage to meet your requirements.

Producer uses murmur2 algorithm which find the target partition by performing hashing over key.
Kafka producer serilizes the data into the broker which is further deserialized by consumer. Hence, kafka comes up with the bundle of serilizer and deserializer. 
We must not change the data type of key and value as the consumer also needs to know which deserilizer technique has to be used in order to read the topic.


