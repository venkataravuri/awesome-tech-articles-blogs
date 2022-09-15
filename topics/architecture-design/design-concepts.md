
Event Sourcing
Observabulkty - What your metrics you monitor
12 Factor
Test-Driven Development
CQRS

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

### CAP Theorm

CAP (Consistency, Availability, and Partition tolerance) theorem helps us to make our choice while designing distributed systems. We can incorporate any two of these 3 functionalities into our system, not all of them.
Consistency:

Partition Tolerance:

Tolerating partition means we are agreed to embrace distributed system - our machines are in different networks. There might have some sorts of network outage between different networks in distributed systems, but in that case our system should be operational. If our system does not tolerate network partition, then it is an application with one machine - not a distributed system.

If we choose to implement distributed system, that means, we are tolerating network partition. So, in the presence of P(Partition tolerance), we either choose C(Consistency) or A(Availability).

## Twelve-Factor App

12 Factor App is a set of best practices that guide you to build a great cloud native application.
- In order that an application be deployed in the cloud and enjoy features such as auto scaling, it first needs to be cloud native
- Using methodology, you can make scalable and resilient apps that can be continuously deployed with maximum agility.
- Acts as a acceptance criteria when evaluating whether software is production ready.

https://newrelic.com/blog/best-practices/twelve-factor-app


## Resiliency Patterns

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
