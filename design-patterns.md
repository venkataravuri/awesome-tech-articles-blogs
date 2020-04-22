Design Patterns - GoF, MVVM

What is Design Pattern?
GoF Patterns
Creational Patterns
Factory Method
Abstract Factory
What is difference between Factory Method and Abstract Factory patterns?
Builder Pattern
Dependency Injection
Prototype
Singleton
Structural Patterns
Adapter Pattern Or Wrapper Or Translator
Composite
Decorator
Facade
Front Controller
Proxy
Bridge
Flyweight
Behavioural Patterns
Chain of responsibility
Command Pattern
Strategy Pattern
Visitor Pattern
Observer or Publish/subscribe
Iterator
Mediator
Memento
State
Interpreter
Template method
MVC, MVP, MVVM
MVC
MVP
MVVM
What is Design Pattern?
A design pattern is a general reusable solution to a commonly occurring problem within a given context.
GoF Patterns
Creational Patterns
Creational patterns abstract the object instantiation process. They hide how objects are created and help make the overall system independent of how its objects are created and composed. 
Class creational patterns focus on the use of inheritance to decide the object to be instantiated. Eg. Factory Method
Object creational patterns focus on the delegation of the instantiation to another object. Eg. Abstract Factory
Factory Method
Define an interface for creating an object, but let subclasses decide which class to instantiate. It uses factory methods to create objects without specifying the exact class of object that will be created. Factory Method lets a class defer instantiation to subclasses.


Abstract Factory
Define an interface or abstract class for creating families of related (or dependent) objects but without specifying their concrete subclasses.


What is difference between Factory Method and Abstract Factory patterns?
Difference between the two is that with the Abstract Factory pattern, a class delegates the responsibility of object instantiation to another object via composition whereas the Factory Method pattern uses inheritance and relies on a subclass to handle the desired object instantiation.
Examples,
I used abstract factory for creating different types of bank accounts such as Checking Account, No Frills Checking, Savings Account, Current Account, Money Market Account
A Loan Factory to create different type of loans such as Home loan (offset, company), Small Business Loan, Personal Loan
Builder Pattern
Separate the construction of a complex object from its representation so that the same construction process can create different representations.

Builder focuses on constructing a complex object step by step. Abstract Factory emphasizes a family of product objects (either simple or complex). Builder returns the product as a final step, but as far as the Abstract Factory is concerned, the product gets returned immediately.

Examples
DOM creation, you have to create plenty of nodes and attributes to get your final object. A factory is used when the factory can easily create the entire object within one method call.
Building an XML document Or using builder for building a HTML table fragments with following methods:
BuildOrderHeaderRow()
BuildLineItemSubHeaderRow()
BuildOrderRow()
BuildLineItemSubRow()
JMock uses builder pattern…

The decorator pattern can be used to extend (decorate) the functionality of a certain object statically, or in some cases at run-time, independently of other instances of the same class, provided some groundwork is done at design time. This is achieved by designing a new decorator class that wraps the original class.
Dependency Injection

Dependency Injection (DI) is a software design pattern that deals with how object/component get hold of their dependencies.

Dependency Injection is a practice where objects are designed in a manner where they receive instances of the objects from other pieces of code, instead of constructing them internally.

Dependency Injection removes the responsibility of direct creation, and management lifespan of object instances upon which a class (consumer class) is dependent. These instances are instead passed to our consumer class, typically as constructor parameters or via property setters.

The management of the dependency object instancing and passing to the consumer class is usually performed by an Inversion of Control (IoC) container

Inversion of control (IoC) is a principle, can be implement using Dependency Injection. Inversion of control pattern Inverts responsibility of managing life cycle of object e.g. creating object, setting there dependency etc from application to framework, which makes writing application even more easy.

Suppose you have an object which in its constructor does something like:
public SomeClass() {
    myObject = Factory.getObject();
}

This can be troublesome when you are looking at mocking myObject but also somehow intercepting the factory call kard. Instead, pass the object in as an argument to the constructor. Now you've moved the problem elsewhere, but testing can become lots easier. Just make a dummy myObject and pass that in. The constructor would now look a bit like:
public SomeClass (MyClass myObject) {
    this.myObject = myObject;
}

It simplifies testing, and improves decoupling.

With IoC frameworks, you can avoid of repeated/boilerplate code that needs to be written if you do on your own.
Prototype
Specify the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.
Singleton
singleton pattern restricts the instantiation of a class to one object, and provide a global point of access to it.
There are multiple ways to create singletons in thread-safe manner in Java.  Since Java 5.0, the easiest way to create a Singleton is the enum type approach.

Lazy initialization
This method uses double-checked locking, which should not be used prior to J2SE 5.0
    
    private static volatile SingletonDemo instance;
    private Singleton() {}

    public static SingletonDemo getInstance() {
        if (instance == null ) {
            synchronized (SingletonDemo.class) {
                if (instance == null) {
                    instance = new SingletonDemo();
                }
            }
        }

        return instance;
    }

Eager initialization
    private static final Singleton INSTANCE = new Singleton();
    private Singleton() {}

    public static Singleton getInstance() {
        return INSTANCE;
    }

Static block initialization
Initialization-on-demand holder idiom
The enum way
public enum Singleton {
        INSTANCE;
        public void execute (String arg) {
            // Perform operation here
        }
}

Structural Patterns
These concern class and object composition. They use inheritance to compose interfaces and define ways to compose objects to obtain new functionality.
Adapter Pattern Or Wrapper Or Translator

Convert the interface of a class into another interface clients expect. The enterprise integration pattern equivalent is the translator.

The adapter contains an instance of the class it wraps. In this situation, the adapter makes calls to the instance of the wrapped object.


Composite
Compose objects into tree structures to represent part-whole hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.
Decorator
Attach additional responsibilities to an object dynamically without subclassing. Decorators provide a flexible alternative to subclassing for extending functionality.

Add responsibilities to individual objects, not to an entire class.
This is achieved by designing a new decorator class that wraps the original class.

http://www.silversoft.net/docs/dp/lowres/pat4dfso.htm

Facade
Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.

Front Controller
The pattern relates to the design of Web applications. It provides a centralized entry point for handling requests.
Proxy
Provide a surrogate or placeholder for another object to control access to it.
Bridge
Decouple an abstraction from its implementation allowing two can vary independently.

http://thecafetechno.com/tutorials/design-patterns/bridge-pattern-in-java-with-sample-code-to-download/
http://www.cs.sjsu.edu/~pearce/modules/patterns/platform/bridge/index.htm
Flyweight
Use sharing to support large numbers of similar objects efficiently.

Behavioural Patterns
Concerned with communication between objects.
Chain of responsibility
Delegates commands to a chain of processing objects. Avoid coupling the sender of a request to its receiver by giving more than one object a chance to handle the request. Chain the receiving objects and pass the request along the chain until an object handles it.


Examples
servlet filters
pipes
Command Pattern
Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

Four terms always associated with the command pattern are command, receiver, invoker and client.


Struts Action Servlet
Do & Un-Do in Text Editor MS-Word
Stock Trade: The client creates some orders for buying and selling stocks (ConcreteCommands). Then the orders are sent to the agent (Invoker).The agent takes the orders and place them to the StockTrade system (Receiver). The agent keeps an internal queue with the order to be placed. Let's assume that the StockTrade system is closed each Monday, but the agent accepts orders, and queue them to be processed later on.
http://www.oodesign.com/command-pattern.html
Strategy Pattern
Define a family of algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

According to the strategy pattern, the behaviors of a class should not be inherited. Instead they should be encapsulated using interfaces.

Strategy allows one of a family of algorithms to be selected on-the-fly at runtime.

KokaWhere did you used this pattern?
Appenders, Layouts, and Filters in Log4Net and Log4j
Layout Managers in UI toolkits
Data compression
Visitor Pattern
Represent an operation to be performed on the elements of an object structure. Visitor lets you define a new operation without changing the classes of the elements on which it operates.

A practical result of this separation is the ability to add new operations to existing object structures without modifying those structures.


Pattern can be used,
Shopping cart with different price calculations (weight of fruit * per kg price) + (no of books * price * discount)
entity validation
Calculation of fees & commissions

http://www.journaldev.com/1769/visitor-design-pattern-in-java-example-tutorial

Observer or Publish/subscribe
Define a one-to-many dependency between objects where a state change in one object results in all its dependents being notified and updated automatically.
Iterator
Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.
Mediator
Define an object that encapsulates how a set of objects interact. Mediator promotes loose coupling by keeping objects from referring to each other explicitly, and it lets you vary their interaction independently.
Memento
Without violating encapsulation, capture and externalize an object's internal state allowing the object to be restored to this state later.
State
Allow an object to alter its behavior when its internal state changes. The object will appear to change its class.
Interpreter
Given a language, define a representation for its grammar along with an interpreter that uses the representation to interpret sentences in the language.
Template method
Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.
MVC, MVP, MVVM
MVC
Traditional MVC is where there is a
    Model: Acts as the model for data
    View : Deals with the view to the user which can be the UI
    Controller: Controls the interaction between Model and View, where view calls the controller to update model. View can call multiple controllers if needed.
MVP
Similar to traditional MVC but Controller is replaced by Presenter. But the Presenter, unlike Controller is responsible for changing the view as well. The view usually does not call the presenter.
MVVM
The difference here is the presence of ViewModel, a specialization of the Presentation Model. It is kind of an implementation of Observer Design Pattern, where changes in the model is represented in the view as well, by the VM. Eg: If a slider is changed, not only the model is updated but the data which may be a text, that is displayed in the view is updated as well. So there is a two-way data binding.


