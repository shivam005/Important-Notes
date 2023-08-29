# Kafka

Producer uses murmur2 algorithm which find the target partition by performing hashing over key.
Kafka producer serilizes the data into the broker which is further deserialized by consumer. Hence, kafka comes up with the bundle of serilizer and deserializer. 
We must not change the data type of key and value as the consumer also needs to know which deserilizer technique has to be used in order to read the topic.


