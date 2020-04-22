


What are good object-oriented design techniques?
Program to an 'interface', not an 'implementation'
Favor 'object composition' over 'class inheritance'.
open closed principle - software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification
What is difference between Abstraction & Encapsulation?
Abstraction is hiding away the implementation details.
Abstraction is implemented in Java using interface and abstract class.

Encapsulation wraps data and methods into a single unit. It is most often achieved through information hiding, which is the process of hiding properties and behaviours of an object and allowing outside access only as appropriate.
Encapsulation is implemented using four types of access level modifiers: public, protected, no modifier and private.

What is Polymorphism?
Polymorphism is briefly described as "one interface, many implementations." Polymorphism is a characteristic of being able to assign a different meaning or usage to something in different contexts - specifically, to allow an entity such as a variable, a function, or an object to have more than one form.

Inheritance, Overloading and Overriding are used to achieve Polymorphism in java. 

Polymorphism manifests itself in three distinct forms in Java:
Method overloading
Method overriding through inheritance
Method overriding through the Java interface

Compile time polymorphism is method overloading.

Runtime time polymorphism is done using inheritance and interface.

What is difference between Aggregation & Composition?
Aggregation is also known as”HAS-A” relationship.  Aggregation can be understood as “whole to its parts” relationship.
Composition is a special form of Aggregation where the part cannot exist without the whole. Composition is a strong Association. Composition relationship is represented like aggregation with one difference that the diamond shape is filled.
What restrictions are placed on method overriding?
Overridden methods must have the same name, argument list, and return type. The overriding method may not limit the access of the method it overrides.
What is the difference between inner class and nested class?
When a class is defined within a scope of another class, then it becomes inner class. If the access modifier of the inner class is static, then it becomes nested class.
Can there be an abstract class with no abstract  methods in it?
Yes,  there can be an abstract class without abstract methods.
What are the differences between Interface and Abstract class?
Abstract Class: An  abstract class can provide complete, default code and/or just the details that  have to be overridden. In  case of abstract class, a class may extend only one abstract class.
An  abstract class can have non-abstract methods.
An  abstract class can have instance variables.
An  abstract class can have any visibility: public, private, protected.
Interfaces: An interface  cannot provide any code at all, just the signature.
A  Class may implement several interfaces.
All  methods of an Interface are abstract.
An Interface cannot have instance variables. Interfaces may have member variables, but these are implicitly public, static, and final



-------------
Functional Reactive Programming, Event-Driven Programming
Reactive Programming
Why we need to go Reactive?
What are characteristics of Reactive Applications?
What you mean by built  “Resilient Systems”?
Functional Reactive Programing
Functional
Reactive
What are Reactive Streams?
Why Stream Processing?
Backpressure (Reactive Pull)
Reactive Extensions -  RxJava
References
How is reactive programming different than event-driven programming?
Event-Driven Server Architecture
How async process works in Camel?
Reactive Programming















Why we need to go Reactive?
Performance demand is always increasing
Rise of Microservices - Distributed systems - Multiple integration points
What are characteristics of Reactive Applications?
Responsive
Resilient
Embrace Failure
Independent things will fail independently
Elastic (Scalable)
Asynchronous / Message-Driven
Free up resources with Async operation & Non-blocking I/O
What you mean by built  “Resilient Systems”?
In a distributed environment, failure of any given service is inevitable. To be resilient they should be, 
Inherently capable to cope with failure, latency and outages of dependencies. Embrace Failure.
recover quickly from difficulties
Should be Fault-tolerant and does fault isolation

Resilient Application Development with Microservices. In microservices architectures, applications are split into highly decoupled, simple, distributed services that communicate with each other over lightweight communication mechanisms like message queues and HTTP APIs.

Hystrix is a library designed to control the interactions between these distributed services providing greater tolerance of latency and failure. Hystrix does this by isolating points of access between the services, stopping cascading failures across them, and providing fallback options, all of which improve the system's overall resiliency.

Elasticity and recovery parts of resilience still need more than just moving to microservices architectures in development to be fulfilled.

Resilient Deployment with Containers on Cluster Infrastructures

Elasticity and recovery, though partly having to be built into the services, are more of a job for deployment, management, and scaling of said microservices systems - and don’t forget to keep them highly available. This is where containers and cluster infrastructures come into play.


Functional Reactive Programing
Functional
It’s declarative, stateless, side-effects free and immutable
‘First Class’ Functions - Pass functions into function
Declarative Programming - Compose methods together to create higher abstraction
Immutable Data - We don’t change data, we project (select) it into new formats
Reactive
Reactive programming combines concurrency and event-based and asynchronous systems.
Reactive programming is programming with asynchronous data streams.
Reactive programming is turning everything into an asynchronous data stream and programming with asynchronous data streams.
What are Reactive Streams?
Stream based Functional Programming
Why Stream Processing?
Scaling business logic
Processing real-time data (fast data)
Batch processing of large datasets (big data)
Monitoring, analytics, complex event processing, etc
Backpressure (Reactive Pull)
Flow control options
Need a way to signal when a subscriber is able to process the data
Effectively push-based (dynamic pull/push)
“Push” behaviour when consumer is faster
“Pull” behaviour when produces is faster
Switches automatically between these
Can only mitigate Hot Streams

Fast publisher responsibilities
Not generate elements, if it is able to control their production rate
Buffer element in bounded manner until more demain is signalled
Drop elements until more demand is signalled
Tear down the stream if unable to apply any of the above strategies


throttle
sample
window
buffer
drop

Reactive Extensions -  RxJava
Observer Pattern (not Pull) based Iterators
An Observable is like Promise++
An Observable pushes items to Subscribers
Subscribers receive and operate on emitted data
Observables and Subscribers operate on Schedulars

Key operations,
filter
map
reduce
groupBy
flatMap

RxJava NOT supports back-pressure
References
http://www.slideshare.net/moldovaictsummit2016/reactive-streams-61623963
http://www.slideshare.net/StevePember/an-introduction-to-reactive-application-reactive-streams-and-options-for-jvm

How is reactive programming different than event-driven programming?
http://stackoverflow.com/questions/34495117/how-is-reactive-programming-different-than-event-driven-programming
Event-Driven Server Architecture
A good write up on Event-Driven Server Architecture,
http://berb.github.io/diploma-thesis/community/042_serverarch.html#event
How async process works in Camel?
http://camel.apache.org/asynchronous-processing.html
