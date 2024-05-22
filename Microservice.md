### Dora (DevOps Research and Assessment) Metrics:
It is meant to assess the devops best practices, It is analyzed based on below mentioned points:
 1. Frequency of deployments 
 2. The amount of time between acceptance and deployment 
 3. How frequently deployments fail 
 4. How long it takes to restore service—or recover from a failure

Every architecture can also be tested based upon the outcome of dora metrics. 

### Service collaboration pattern:
There are 4 service collaboration pattern:
1. Saga, which implements a distributed command as a series of local transactions
2. Command-side replica, which replicas read-only data to the service that implements a command
3. API composition, which implements a distributed query as a series of local queries
4. CQRS, which implements a distributed query as a series of local queries

### Services can communicate using Messaging and Remote Procedure Invocation:
#### Messaging: There are several different styles of asynchronous communication:
1. Request/response - a service sends a request message to a recipient and expects to receive a reply message promptly
2. Notifications - a sender sends a message a recipient but does not expect a reply. Nor is one sent.
3. Request/asynchronous response - a service sends a request message to a recipient and expects to receive a reply message eventually
4. Publish/subscribe - a service publishes a message to zero or more recipients
5. Publish/asynchronous response - a service publishes a request to one or recipients, some of whom send back a reply
#### RPI : There are numerous examples of RPI technologies:
1. REST
2. gRPC
3. Apache Thrift

### Log Aggregation
While the ELK stack is a powerful and popular solution for centralized logging, there are several other options available, each with its own advantages. Fluentd and Fluent Bit offer lightweight and flexible logging solutions, Graylog provides a robust open-source alternative, Splunk offers comprehensive enterprise features, AWS CloudWatch Logs is ideal for AWS environments, and Azure Monitor is perfect for Azure-based infrastructure. The choice of logging solution depends on your specific requirements, infrastructure, and budget.

### Application Metrics: Instrument a service to gather statistics about individual operations
Instrumentation libraries:
1. Coda Hale/Yammer Java Metrics Library
2. Prometheus client libraries
Metrics aggregation services
1. Prometheus
2. AWS Cloud Watch

### Distributed tracing: to understand behavior of an individual service
1. Instrument services with code that Assigns each external request a unique external request id
2. Passes the external request id to all services that are involved in handling the request
3. Includes the external request id in all log messages
4. Records information (e.g. start time, end time) about the requests and operations performed when handling a external request in a centralized service
Example:
Open Zipkin - service for recording and displaying tracing information
Open Tracing - standardized API for distributed tracing.

### Exception tracking: 
Report all exceptions to a centralized exception tracking service that aggregates and tracks exceptions and notifies developers.

### microservice chassis: Consistency, Efficiency, Maintainability, Scalability, Observability
#### Spring Boot (Spring Cloud):
Spring Boot, together with Spring Cloud, provides a comprehensive microservice chassis. Spring Cloud includes tools for service discovery (Eureka), configuration management (Config Server), circuit breakers (Hystrix), and distributed tracing (Sleuth).

#### Netflix OSS:
Netflix provides several open-source tools as part of their microservice chassis, including Eureka (service discovery), Hystrix (circuit breaker), Ribbon (client-side load balancing), and Zuul (API gateway).
Istio:

#### Istio 
It is a service mesh that provides many features of a microservice chassis, including traffic management, security, and observability. It works by injecting sidecar proxies (Envoy) alongside microservices to handle these cross-cutting concerns.

#### Micronaut:
Micronaut is a modern JVM-based framework designed for building microservices. It provides features such as dependency injection, configuration management, service discovery, and HTTP client abstraction.
#### Go-Kit:
Go-Kit is a toolkit for building microservices in Go. It provides components for service discovery, logging, metrics, tracing, and more.





How do you decide on the boundaries of a microservice?
Scenario: You have to design a new microservice for a large e-commerce website. How would you go about identifying the boundaries of this microservice?

https://stackoverflow.com/questions/50562495/how-to-handle-microservice-interaction-when-one-of-the-microservice-is-down

How do you handle communication between microservices?
Scenario: Two microservices need to communicate with each other to complete a business transaction. How would you handle this communication in Java?

What is service discovery, and how can you implement it in Java?
Scenario: You are building a microservices-based application, and you need to implement service discovery. How would you do this in Java?

How do you handle failures and retries in microservices?
Scenario: A microservice fails to complete a task. How would you handle this failure in Java, and how would you ensure that the task is retried?

How do you implement security in microservices?
Scenario: You are developing a microservice that needs to access sensitive data. How would you ensure that the microservice is secure, and what security protocols would you use in Java?

How do you handle versioning in microservices?
Scenario: You need to make changes to a microservice, but you don't want to break the existing APIs that other microservices are using. How would you handle versioning in Java?

How do you implement load balancing in microservices?
Scenario: You have multiple instances of a microservice running, and you need to distribute the traffic evenly between them. How would you implement load balancing in Java?

How do you ensure data consistency between microservices?
Scenario: Two microservices need to access the same data, and you need to ensure that the data remains consistent. How would you handle this in Java?

How do you handle asynchronous communication between microservices?
Scenario: One microservice needs to send a message to another microservice asynchronously. How would you handle this in Java, and what protocols would you use?

How do you handle scaling and deployment of microservices?
Scenario: You have to deploy a new microservice, and you need to ensure that it can scale easily. How would you handle scaling and deployment in Java?
