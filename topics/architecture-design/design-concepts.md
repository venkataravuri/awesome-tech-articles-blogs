
# Modern System Design Concepts

**Table of contents**

- [Cloud-Native Applications]()
  - [Twelve Factor App]()
- [SOLID Principles]()
- [Domain-driven Design (DDD)]()
  - [Event Sourcing & CQRS]()
- [Resiliency Patterns]()
  - [Circuit Breaker]()
  - [Event Loop]()
- [CAP Therom]()   
- [Microfrontends]()
- [Chaos Engineering]()
- [GraphQL]()
- [Cache Strategies]()

### Cloud Native Applications

Cloud native apps are designed and built to exploit scale, elasticity, resiliency, and flexibility provided by in public, private, and hybrid clouds.

- Usually designed as self contained services or microservices, packed as containers for portability, deployed to immutable infrastructure.
- Microservices are the core of cloud native application architecture
- Cloud native microservices communicate with each other via APIs and use event-driven architecture, which makes them loosely coupled, serves to enhance the overall performance of each application.
- Adheres to 12-factor principles

## Twelve-Factor App

12 Factor App is a set of best practices that guide you to build a great cloud native application.

- In order that an application be deployed in the cloud and enjoy features such as auto scaling, it first needs to be cloud native
- Using methodology, you can make scalable and resilient apps that can be continuously deployed with maximum agility.
- Acts as a acceptance criteria when evaluating whether software is production ready.

**Notes**

- [Twelve Factor App Principles Quick Summary](https://dzone.com/articles/12-factor-app-principles-and-cloud-native-microser)
- [Twelve Factor App Principles Detailed Summary](https://newrelic.com/blog/best-practices/twelve-factor-app)

### Domain Driven Design

:star::star::star: https://medium.com/ssense-tech/domain-driven-design-effective-domain-modeling-and-its-perks-e4e3e3e0d5ee

- Domain-Driven Design (DDD) is about **mapping 'business domain' concepts into software artifacts**. 
- It **emphasizes on rich domain model over anemic domain model**
- The domain concepts & logic is modeled as Entities, Value Objects, and Aggregates with clear boundaries.
- In anemic domain models, entities are represented by classes with data and connections to other entities. **Business logic is absent in these classes** and **logic is usually placed in managers, services, utilities, helpers, etc**.
- Traditonal anemic domain models, leads to a **fat Service Layer where facade classes accumulate more business logic** with time and domain objects become mere data carriers with getters and setters. **Since proper responsibility boundaries are not defined, domain-specific business logic and responsibilities may leak into other components.**
- DDD architecture promotes a rich model and thin services.

- Bounded contexts are defined with explicit boundaries and the relationships

- In DDD, each aggregate requires one repository. This means we have fewer repositories in DDD than the number of DAOs required to load and persist entities in an application with an anemic model.
- In DDD, since the Order aggregate must contain all the business operations that can be performed on it, we need to move the logic to change the order status and to add an item, from the Service Layer to the Domain Layer

DDD Architecture Layers 

- Domain Layer contains entities & value objects along with **repository interface**. All the business logic will live in this layer.
- UI Layer will contain the controller. 
- Application Layer will contain the services. There is now a separate service for each operation that is performed on a specific area of the domain.
- Infrastructure Layer will contain the implementation of the interfaces defined in the domain, as well as classes that provide this implementation. Any operations that require our application to communicate with the outside world should be implemented in this layer too.

### How DDD benefits? Is it worth?

### SOLID Principles

- S – Single Responsibility Principle
- O – Open-Closed Principle
- L – Liskov Substitution Principle
- I – Interface Segregation Principle
- D – Dependency Inversion Principle

**Design Pattern** - is like a cure against some disease. And **Disease** - is violation of _S.O.L.I.D._

https://www.slideshare.net/DrTrucho/python-solid

All Design Patterns compliance S.O.L.I.D principles, and other principles: Prefer composition to inheritance Incapsulate changes Do high cohesion and low coupling etc 

https://stackoverflow.com/questions/3085285/difference-between-cohesion-and-coupling

https://www.linkedin.com/pulse/solid-design-principles-python-examples-hiral-amodia

**Single Responsibility Principle** states that **a class should have only one primary responsibility and should not take other responsibilities**. “A class should have only one reason to change”.

**Open-Closed Principle** states that “Software entities (classes, modules, functions, etc.) **should be open for extension, but closed for modification**_.”

Following this principle ensures that a class is well defined to do what it is supposed to do. Adding any further features can be done by creating new entities that extend the existing class’s features and add more features to itself.

Open-close is a principle which strategy pattern is a good way to implementing that, There are other patterns that help achieve OCP, like Abstract Factory. You can achieve OCP in a class by externalizing some of its responsibilities to a Strategy and writing new Strategies instead of modifying the class itself, but it is not the only way of respecting OCP. 

Collections.sort works on any collection of objects that implement the Comparable interface, it is not limited to sorting just integers or just strings — it is not limited to any specific type. The sorting algorithm will work as it was designed, so we can say that it is closed to modification, but the sorting criteria will vary depending on the compareTo method implementation

_**Liskov Substitution Principle**_ states that "Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program."

The Interface Segregation Principle states that “No client should be forced to depend on methods it does not use”.

The Dependency Inversion Principle states that:

a). High level module should not depend on low level modules. Both should depend on abstractions
b). Abstractions should not depend on details. Details should depend on abstractions. 

### Event Sourcing & CQRS

CQRS — Command Query Response Segregation - allows to scale system read functions and write functions independently. It is often that a system handles more reads than writes.

CQRS is often DDD-oriented, associated with Event-Source and Eventual Consistency.

The patterns employs "One Write Model, N Read Models"

- One internal model it writes with: the write model, altered by Commands
- One or several read models it and other applications read from.

The Read Models can be read by front-ends or by APIs.

### Resiliency Patterns

In a distributed system, failures can happen. Network can have transient failures, hardware can fail, storage disks can corrupt. Therefore, design an application to be self-healing when failures occur. 

This requires a three-pronged approach:
- Detect failures.
- Respond to failures gracefully.
- Log and monitor failures, to give operational insight.

Resiliency is the capability to handle partial failures while continuing to execute and not crash. Applications that communicate with remote services and resources must be sensitive to transient faults. 

Transient faults include the momentary loss of network connectivity to components and services, the temporary unavailability of a service, or timeouts that arise when a service is busy. These faults are often self-correcting, and if the action is repeated after a suitable delay it is likely to succeed.

We decorate network-bound calls with resiliency aspects in following order:

** Retry ( CircuitBreaker ( RateLimiter ( TimeLimiter ( Bulkhead ( Function ) ) ) ) ) **

Retry is applied at the end (if needed).

The execution order:
1. supplier, then decorate in order with resilience:
2. RateLimiter (prevent a call if rate-limit exceeded)
3. TimeLimiter (time-out a call)
4. CircuitBreaker (fail-fast)
5. Retry (retry on exceptions)
6. Fallback (fallback as last resort)

A suitable reference order is for example auto-configured in the Spring-Boot extension. See the official Guides, Getting started with resilience4j-spring-boot2 about Aspect order.

Resilience4j is a lightweight fault tolerance designed for functional programming.

### Circuit Breaker

A technique to avoid cascading failures in an interdependent microservices environment, where dependent service has outage or degraded performance. 

Circuit Breaker framework monitors communications for failures. Once the failures reach a certain threshold, the circuit breaker trips, and all further calls to the circuit breaker return with an error or with some alternative service or default message

It make sure system is responsive & resilient and threads are not waiting for an unresponsive call. 

The circuit breaker has three distinct states: Closed, Open, and Half-Open:
* Closed – remains in the closed state and all calls pass through to the services. When the number of failures exceeds a predetermined threshold the breaker trips, and it goes into the Open state.
* Open – The circuit breaker returns an error for calls without executing the function.
* Half-Open – After a timeout period, the circuit switches to a half-open state to test if the underlying problem still exists. If a single call fails in this half-open state, the breaker is once again tripped. If it succeeds, the circuit breaker resets back to the normal, closed state.

### Bulkhead

Bulkehead for concurrency controller (limits concurrent handling) and circuit breaker to control constant overlaod.

Will protect from bursts & spikes. With bulkhead pattern, components of an application are isolated into pools so that if one fails, the others will continue to function.

The benefits of this pattern include:
- Isolates consumers and services from cascading failures. An issue affecting a consumer or service can be isolated within its own bulkhead, preventing the entire solution from failing.
- Allows you to preserve some functionality in the event of a service failure. Other services and features of the application will continue to work.
- Allows you to deploy services that offer a different quality of service for consuming applications. A high-priority consumer pool can be configured to use high-priority services.

**References**

https://dzone.com/articles/resilient-microservices-pattern-bulkhead-pattern

### Idempotency

Perform an operation multiple times without changing the result.

Ex. Update the contact details of a user in the system, delete a file.

Not idempotent operations - send payment, create orders. REST - POST, PATCH

Receives a request with the same idempotence key (could be UUID (or) request/reference id), it knows that it’s a retry.


### CAP Theorm

CAP (Consistency, Availability, and Partition tolerance) theorem helps us to make our choice while designing distributed systems. We can incorporate any two of these 3 functionalities into our system, not all of them.
Consistency:

Partition Tolerance:

Tolerating partition means we are agreed to embrace distributed system - our machines are in different networks. There might have some sorts of network outage between different networks in distributed systems, but in that case our system should be operational. If our system does not tolerate network partition, then it is an application with one machine - not a distributed system.

If we choose to implement distributed system, that means, we are tolerating network partition. So, in the presence of P(Partition tolerance), we either choose C(Consistency) or A(Availability).

#### Which database falls under which category (AP, CP)?
https://bikas-katwal.medium.com/mongodb-vs-cassandra-vs-rdbms-where-do-they-stand-in-the-cap-theorem-1bae779a7a15

## Optimistic Lock Vs. Pessimistic Lock

Optimistic Locking allows a conflict to occur, but it needs to detect it at write time. This can be done using either a physical or a logical clock. However, since logical clocks are superior to physical clocks when it comes to implementing a concurrency control mechanism, we are going to **use a version column** to capture the read-time row snapshot information.

The version column is going to be incremented every time an UPDATE or DELETE statement is executed while also being used for matching the expected row snapshot in the WHERE clause.

Pessimistic locking aims to avoid conflicts by using locking.

optimistic locking can help you **_prevent Lost Updates_** even when using application-level transactions that incorporate the user-think time as well.

optimistic locking works even across multiple database transactions since it doesn’t rely on locking physical records.

Pessimistic locking is suitable when the cost of retrying a transaction is very high or when contention is so large that many transactions would end up rolling back if optimistic locking were used.

#### Database Isolation Vs. Optimistic/Pessimistic Locks

Depending on isolation level you've chosen, specific resource is going to be locked until given transaction commits or rollback - it can be lock on a whole table, row or block of sql. It's a pessimistic locking and it's ensured on database level when running a transaction.
Optimistic locking on the other hand assumes that multiple transactions rarely interfere with each other so no locks are required in this approach. It is a application-side check that uses @Version attribute in order to establish whether version of a record has changed between fetching and attempting to update it.


### Peer to peer task choreography & Orchestration Engine

Initially we adopted peer to peer task choreography. process flows are orchestrated in ad-hoc manner using a combination of event  driven pub/sub, making direct REST calls, and using a database to manage the state.

As the number of microservices grow and the complexity of the processes increases, getting visibility into these distributed workflows becomes difficult without a central orchestrator.

Process flows are “embedded” within the code of multiple applications

A JSON DSL based blueprint defines the execution flow.

A workflow blueprint defines a series of tasks that needs be executed. Each of the tasks are either a control task (e.g. fork, join, decision, sub workflow, etc.) or a worker task

Workflow engine is a state machine, As workflow events occur combines with workflow blueprint with current state, to identify next state and schedules tasks, updates states machine

Task Workers are intended to be idempotent stateless functions. The polling model allows us to handle backpressure on the workers and provide auto-scalability based on the queue depth when possible.

Workers are language agnostic, allowing each microservice to be written in the language most suited for the service.

https://netflixtechblog.com/netflix-conductor-a-microservices-orchestrator-2e8d4771bf40


### An note on HTTP error codes

https://www.yeahhub.com/1xx-2xx-3xx-4xx-5xx-http-status-codes/


https://medium.com/javarevisited/completablefuture-usage-and-best-practises-4285c4ceaad4

### Explan Event Loop in Node.js

The key building blocks in non-blocking IO are: Event Demultiplexer, Event Queue, Event Loop

https://tusharf5.com/posts/node-design-patterns-reactor-pattern

Non blocking I/O - handle all I/O activities asynchronously

#### Event Demultiplexer
Also called Event Notification Interface is another way to react to events. In this mechanism the system collects and queues I/O events coming from a set of watched resources. It blocks the process until new events are available. So no CPU time is wasted waiting for events. This is also called the Event loop.

### Inversion of Control & Dependency Inversion

IOC can be done using Dependency Injection (DI). It explains how to inject the concrete implementation into a class that is using abstraction, in other words an interface inside.

The IoC container creates an object of the specified class and also injects all the dependency objects through a constructor, a property or a method at run time and disposes it at the appropriate time.

### Microfrontends

https://medium.com/bb-tutorials-and-thoughts/7-different-ways-to-implement-micro-frontends-with-react-907b5e262230

## BFF - Backends for Frontends

BFF are a lightweight translation layers (aka backend services) that decouple individual clients from downstream services and serve only a single frontend. Adopt separate backend services for different types of clients, . That way, a single backend service doesn't need to handle the conflicting requirements of various client types. This pattern can help keep each microservice simple, by separating client-specific concerns.

https://blog.bitsrc.io/bff-pattern-backend-for-frontend-an-introduction-e4fa965128bf

## Backend-as-a-Service (BaaS)

Backend-as-a-Service allows to hook up mobile/webapps to the backend with a set of core app features, including authentication, authorization, managing users, sending push notifications, and connecting to third-party cloud providers.

### GraphQL

GraphQL, I see it as query language for API

https://www.slideshare.net/nburk/react-graphql?qid=e496f1f4-ad5f-43fa-9b8b-e74762825f3e&v=&b=&from_search=5


3 operation types:
- Query
- Mutation (Write and Get)
- Subscription

### Test-Driven Development

## Cache Strategies

Cache repeatedly access information held in a data store into memory to improve performance. 

#### Cache Aside

Cache-aside is also called as lazy caching, wherein first check item exist in cache. If the item exists in the cache, use that. If the item does not exist in the cache, query the data store, however on the way back you drop the item in the cache.

In cache-aside, application is responsible for reading and writing from the database and the cache doesn't interact with the database at all. Cache is "kept aside" as a faster and more scalable in-memory data store.

#### Read-through & Write-through Cache

In read-through/write-through cache, application treats cache as the main data store and reads data from it and writes data to it. The cache is responsible for reading and writing this data to the database, thereby relieving the application of this responsibility.

- In **read-through cache**, the application always requests data from the cache. If cache has no data, it is responsible for retrieving the data from the DB using an underlying provider plugin. Compared to Cache-Aside, Read-Through moves the responsibility of getting the value from the datastore to the cache provider.
- In **write-through cache**, the cache is updated in real time when the database is updated. So, if a user updates his or her profile, the updated profile is also pushed into the cache. You can think of this as being proactive to avoid unnecessary cache misses. Similar to Read-Through but for writes, Write-Through moves the writing responsibility to the cache provider.

#### Write-Behind

In the Write-Behind scenario, modified cache entries are asynchronously written to the data source.
