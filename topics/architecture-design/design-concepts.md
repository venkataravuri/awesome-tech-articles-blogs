
Optimising Locking
Event Sourcing
CAP theorm
Domain Driven Design
Observabulkty - What your metrics you monitor
12 Factor
Test-Driven Development
CQRS

### Domain Driven Design

Source: https://medium.com/inato/an-introduction-to-domain-driven-design-386754392465

Three concepts that make most of what Domain-Driven Design is.
- Separating the concerns into layers - Isolating the domain: the layered architecture
- Modeling the Domain
- Managing the life-cycle of Domain objects

1. Isolating the domain: the layered architecture

Domain-Driven Design focuses on domain modeling, and separating the model (or business logic) from the implementation details (e.g. which database we use).

The recommended architecture is made of 4 layers.

User Interface (or Presentation Layer)
Application Layer
This layer is kept thin. It does not contain business rules or knowledge, but only coordinates tasks and delegates work to collaborations of domain objects in the next layer down.

Domain Layer (or Model Layer)
Responsible for representing concepts of the business, information about the business situation, and business rules.

State that reflects the business situation is controlled and used here, even though the technical details of storing it are delegated to the infrastructure.

Infrastructure Layer
Provides generic technical capabilities that support the higher layers: message sending for the application, persistence for the domain, drawing widgets for the UI, and so on. The infrastructure layer may also support the pattern of interactions between the four layers through an architectural framework.

