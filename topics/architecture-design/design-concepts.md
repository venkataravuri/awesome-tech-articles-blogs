
# Modern System Design Concepts 

### Cloud Native Applications

Cloud native apps are designed and built to exploit scale, elasticity, resiliency, and flexibility provided by in public, private, and hybrid clouds.

Usually designed as self contained services or microservices, packed as containers for portability, deployed to immutable infrastructure.

Microservices are the core of cloud native application architecture

Cloud native microservices communicate with each other via APIs and use event-driven architecture, which makes them loosely coupled, serves to enhance the overall performance of each application.

Adheres to 12-factor principles

## Twelve-Factor App

12 Factor App is a set of best practices that guide you to build a great cloud native application.
- In order that an application be deployed in the cloud and enjoy features such as auto scaling, it first needs to be cloud native
- Using methodology, you can make scalable and resilient apps that can be continuously deployed with maximum agility.
- Acts as a acceptance criteria when evaluating whether software is production ready.

https://newrelic.com/blog/best-practices/twelve-factor-app

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

### Event Sourcing & CQRS

### Resiliency Patterns

Resiliency Aspects applied in following order:

Retry ( CircuitBreaker ( RateLimiter ( TimeLimiter ( Bulkhead ( Function ) ) ) ) )

Retry is applied at the end (if needed).

The execution order:
1. supplier, then decorate in order with resilience:
2. RateLimiter (prevent a call if rate-limit exceeded)
3. TimeLimiter (time-out a call)
4. CircuitBreaker (fail-fast)
5. Retry (retry on exceptions)
6. Fallback (fallback as last resort)

A suitable reference order is for example auto-configured in the Spring-Boot extension. See the official Guides, Getting started with resilience4j-spring-boot2 about Aspect order

### Circuit Breaker

A technique to avoid cascading failures in an interdependent microservices environment, where dependent service has outage or degraded performance. 

Circuit Breaker framework monitors communications for failures. Once the failures reach a certain threshold, the circuit breaker trips, and all further calls to the circuit breaker return with an error or with some alternative service or default message

It make sure system is responsive & resilient and threads are not waiting for an unresponsive call. 

The circuit breaker has three distinct states: Closed, Open, and Half-Open:
* Closed – remains in the closed state and all calls pass through to the services. When the number of failures exceeds a predetermined threshold the breaker trips, and it goes into the Open state.
* Open – The circuit breaker returns an error for calls without executing the function.
* Half-Open – After a timeout period, the circuit switches to a half-open state to test if the underlying problem still exists. If a single call fails in this half-open state, the breaker is once again tripped. If it succeeds, the circuit breaker resets back to the normal, closed state. 

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

### BFF Patterns

https://blog.bitsrc.io/bff-pattern-backend-for-frontend-an-introduction-e4fa965128bf

### Microfrontends

https://medium.com/bb-tutorials-and-thoughts/7-different-ways-to-implement-micro-frontends-with-react-907b5e262230

### GraphQL

GraphQL, I see it as query language for API

https://www.slideshare.net/nburk/react-graphql?qid=e496f1f4-ad5f-43fa-9b8b-e74762825f3e&v=&b=&from_search=5


3 operation types:
- Query
- Mutation (Write and Get)
- Subscription

Test-Driven Development
