
Optimising Locking
Event Sourcing
CAP theorm
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

### How DDD benefits?




