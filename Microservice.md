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

### microservice chassis: It basically provide chasis for software which helps in achieving Consistency, Efficiency, Maintainability, Scalability, Observability
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

# Service collaboration patterns 
In microservices refer to the various ways in which microservices interact with each other to fulfill business requirements. These patterns address communication, coordination, and data sharing between microservices. Here are the primary service collaboration patterns:

### 1. API Gateway Pattern
Description: An API Gateway acts as a single entry point for all client requests. It routes requests to the appropriate microservices and handles cross-cutting concerns such as authentication, logging, and rate limiting.

Benefits:

Simplifies client interactions by exposing a single endpoint.
Centralizes cross-cutting concerns.
Reduces the number of round trips between clients and microservices.
Challenges:

Introduces a single point of failure.
Can become a performance bottleneck if not properly scaled.
Example:
Netflix Zuul, Kong, or AWS API Gateway.

### 2. Service Discovery Pattern
Description: Service discovery allows microservices to dynamically find and communicate with each other. There are two types of service discovery: client-side and server-side.

Client-Side Discovery: Clients query a service registry to find service instances and directly communicate with them.
Server-Side Discovery: Clients send requests to a load balancer or API gateway, which queries the service registry and forwards requests to the appropriate service instances.
Benefits:

Enables dynamic scaling and management of services.
Improves fault tolerance by rerouting requests from failed instances.
Challenges:

Adds complexity to the system.
Requires maintaining an up-to-date service registry.
Example:
Eureka, Consul, or Zookeeper.

### 3. Circuit Breaker Pattern
Description: The circuit breaker pattern helps prevent cascading failures in a microservices architecture by stopping calls to a service that is likely to fail. It has three states: closed (normal operation), open (calls are prevented), and half-open (test calls are allowed).

Benefits:

Improves system resilience and stability.
Provides fallback mechanisms to handle service failures gracefully.
Challenges:

Requires careful configuration and tuning.
Can add complexity to service interactions.
Example:
Hystrix, Resilience4j.

### 4. Event-Driven Pattern
Description: In an event-driven architecture, services communicate by producing and consuming events. This decouples services and allows for asynchronous communication.

Benefits:

Decouples services, making the system more flexible and scalable.
Allows for asynchronous processing, which can improve performance.
Challenges:

Debugging and monitoring become more complex.
Requires a reliable event broker.
Example:
Apache Kafka, RabbitMQ.

### 5. Saga Pattern
Description: The saga pattern is used to manage distributed transactions in a microservices architecture. It breaks down a large transaction into a series of smaller transactions, each performed by a different service. If one transaction fails, compensating transactions are executed to undo the changes.

Benefits:

Manages distributed transactions without locking resources.
Provides a way to ensure data consistency across services.
Challenges:

Compensating transactions can be complex to implement.
Requires careful design to handle failure scenarios.
Example:
Choreography-based saga (each service produces and listens to events) or Orchestration-based saga (a central coordinator manages the transaction flow).

### 6. Aggregator Pattern
Description: The aggregator pattern collects data from multiple microservices and combines it into a single response. This is often used by an API Gateway or a backend-for-frontend (BFF) service.

Benefits:

Reduces the number of client requests.
Simplifies client interactions.
Challenges:

Can become a performance bottleneck.
Increases the complexity of the aggregator service.
Example:
GraphQL can serve as an aggregator by fetching and combining data from multiple microservices.

### 7. Proxy Pattern
Description: The proxy pattern involves a service acting as an intermediary for requests between a client and another service. This pattern is often used for logging, authentication, and authorization.

Benefits:

Simplifies client-side logic.
Centralizes cross-cutting concerns.
Challenges:

Adds an extra layer of communication.
Can become a performance bottleneck.
Example:
Envoy, Linkerd.

### 8. Database per Service Pattern
Description: Each microservice has its own database, ensuring that services are loosely coupled and can evolve independently.

Benefits:

Decouples services, enabling independent scaling and development.
Prevents the shared database becoming a single point of failure.
Challenges:

Managing data consistency across services can be challenging.
Implementing queries that span multiple services is complex.
Example:
Using separate databases like MySQL for one service and MongoDB for another.

### 9. Shared Data Pattern
Description: Multiple microservices share a common database. This is less common in microservices due to the tight coupling it introduces but can be used when strong consistency is required.

Benefits:

Ensures strong data consistency.
Simplifies data management.
Challenges:

Creates tight coupling between services.
Limits the ability to scale services independently.
Example:
A shared PostgreSQL database accessed by multiple services.

### 10. Sidecar Pattern
Description: The sidecar pattern involves deploying helper components (sidecars) alongside the main service containers to handle tasks such as logging, monitoring, and configuration management.

Benefits:

Offloads non-business logic tasks from the main service.
Standardizes the implementation of cross-cutting concerns.
Challenges:

Increases the complexity of the deployment model.
Requires coordination between main and sidecar containers.
Example:
Using a logging sidecar with Fluentd or a monitoring sidecar with Prometheus.







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
