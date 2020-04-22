


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


JVM Tuning
JVM
Explain JVM Memory Model?
Young Generation
Old Generation
Permanent Generation
Java Garbage Collection
Java Garbage Collection Types
Java Garbage Collection Monitoring
Java VisualVM with Visual GC
Tuning
Tuning Heap Size
Tuning Garbage Collection Algorithm
JVM Threads
JVM
JVM translates the Java programming instructions into instructions and commands that run on the local operating system.

A class file contains Java virtual machine instructions (or bytecodes) and a symbol table, as well as other ancillary information.
http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html
Explain JVM Memory Model?

JVM memory is divided into separate parts. At broad level, JVM Heap memory is physically divided into two parts – Young Generation and Old Generation. Permanent Generation or “Perm Gen” contains the application metadata required by the JVM to describe the classes and methods used in the application. Note that Perm Gen is not part of Java Heap memory.
Young Generation
Young generation is the place where all the new objects are created. When young generation is filled, garbage collection is performed. This garbage collection is called Minor GC. Young Generation is divided into three parts – Eden Memory and two Survivor Memory spaces.
Old Generation
Old Generation memory contains the objects that are long lived and survived after many rounds of Minor GC. Usually garbage collection is performed in Old Generation memory when it’s full. Old Generation Garbage Collection is called Major GC and usually takes longer time.
Permanent Generation
Permanent Generation or “Perm Gen” contains the application metadata required by the JVM to describe the classes and methods used in the application. Note that Perm Gen is not part of Java Heap memory.
Method Area -Method Area is part of space in the Perm Gen and used to store class structure (runtime constants and static variables) and code for methods and constructors.
Memory Pool - Memory Pools are created by JVM memory managers to create a pool of immutable objects, if implementation supports it. String Pool is a good example of this kind of memory pool. Memory Pool can belong to Heap or Perm Gen, depending on the JVM memory manager implementation.
Runtime Constant Pool - Runtime constant pool is per-class runtime representation of constant pool in a class. It contains class runtime constants and static methods. Runtime constant pool is the part of method area.
Java Garbage Collection
Java Garbage Collection is the process to identify and remove the unused objects from the memory. Garbage Collector is the program running in the background that looks into all the objects in the memory and find out objects that are not referenced by any part of the program. All these unreferenced objects are deleted and space is reclaimed for allocation to other objects.

One of the basic way of garbage collection involves three steps:
Marking: This is the first step where garbage collector identifies which objects are in use and which ones are not in use.
Normal Deletion: Garbage Collector removes the unused objects and reclaim the free space to be allocated to other objects.
Deletion with Compacting: For better performance, after deleting unused objects, all the survived objects can be moved to be together. This will increase the performance of allocation of memory to newer objects.
Java Garbage Collection Types
There are five types of garbage collection types that we can use in our applications. We just need to use JVM switch to enable the garbage collection strategy for the application. Let’s look at each of them one by one.

Serial GC (-XX:+UseSerialGC): Serial GC uses the simple mark-sweep-compact approach for young and old generations garbage collection i.e Minor and Major GC.    Serial GC is useful in client-machines such as our simple stand alone applications and machines with smaller CPU. It is good for small applications with low memory footprint.

Parallel GC (-XX:+UseParallelGC): Parallel GC is same as Serial GC except that is spawns N threads for young generation garbage collection where N is the number of CPU cores in the system. We can control the number of threads using -XX:ParallelGCThreads=n JVM option.
Parallel Garbage Collector is also called throughput collector because it uses multiple CPUs to speed up the GC performance. Parallel GC uses single thread for Old Generation garbage collection.
Concurrent Mark Sweep (CMS) Collector (-XX:+UseConcMarkSweepGC): CMS Collector is also referred as concurrent low pause collector. It does the garbage collection for Old generation. CMS collector tries to minimize the pauses due to garbage collection by doing most of the garbage collection work concurrently with the application threads.
CMS collector on young generation uses the same algorithm as that of the parallel collector. This garbage collector is suitable for responsive applications where we can’t afford longer pause times. We can limit the number of threads in CMS collector using -XX:ParallelCMSThreads=n JVM option.
G1 Garbage Collector (-XX:+UseG1GC): The Garbage First or G1 garbage collector is available from Java 7 and it’s long term goal is to replace the CMS collector. The G1 collector is a parallel, concurrent, and incrementally compacting low-pause garbage collector.

Garbage First Collector doesn’t work like other collectors and there is no concept of Young and Old generation space. It divides the heap space into multiple equal-sized heap regions. When a garbage collection is invoked, it first collects the region with lesser live data, hence “Garbage First”. 
Java Garbage Collection Monitoring
Use jstat command line tool to monitor the JVM memory and garbage collection activities. It ships with standard JDK. For executing jstat you need to know the process id of the application.
$ jstat -gc 9582 1000
 S0C    S1C    S0U    S1U      EC       EU        OC         OU       PC     PU    YGC     YGCT    FGC    FGCT     GCT
1024.0 1024.0  0.0    0.0    8192.0   7933.3   42108.0    23401.3   20480.0 19990.9    157    0.274  40      1.381    1.654
1024.0 1024.0  0.0    0.0    8192.0   8026.5   42108.0    23401.3   20480.0 19990.9    157    0.274  40      1.381    1.654
1024.0 1024.0  0.0    0.0    8192.0   8030.0   42108.0    23401.3   20480.0 19990.9    157    0.274  40      1.381    1.654
1024.0 1024.0  0.0    0.0    8192.0   8122.2   42108.0    23401.3   20480.0 19990.9    157    0.274  40      1.381    1.654
1024.0 1024.0  0.0    0.0    8192.0   8171.2   42108.0    23401.3   20480.0 19990.9    157    0.274  40      1.381    1.654
1024.0 1024.0  48.7   0.0    8192.0   106.7    42108.0    23401.3   20480.0 19990.9    158    0.275  40      1.381    1.656
1024.0 1024.0  48.7   0.0    8192.0   145.8    42108.0    23401.3   20480.0 19990.9    158    0.275  40      1.381    1.656

The last argument for jstat is the time interval between each output, so it will print memory and garbage collection data every 1 second.

Let’s go through each of the columns one by one.
S0C and S1C: This column shows the current size of the Survivor0 and Survivor1 areas in KB.
S0U and S1U: This column shows the current usage of the Survivor0 and Survivor1 areas in KB. Notice that one of the survivor areas are empty all the time.
EC and EU: These columns show the current size and usage of Eden space in KB. Note that EU size is increasing and as soon as it crosses the EC, Minor GC is called and EU size is decreased.
OC and OU: These columns show the current size and current usage of Old generation in KB.
PC and PU: These columns show the current size and current usage of Perm Gen in KB.
YGC and YGCT: YGC column displays the number of GC event occurred in young generation. YGCT column displays the accumulated time for GC operations for Young generation. Notice that both of them are increased in the same row where EU value is dropped because of minor GC.
FGC and FGCT: FGC column displays the number of Full GC event occurred. FGCT column displays the accumulated time for Full GC operations. Notice that Full GC time is too high when compared to young generation GC timings.
GCT: This column displays the total accumulated time for GC operations. Notice that it’s sum of YGCT and FGCT column values.

The advantage of jstat is that it can be executed in remote servers too where we don’t have GUI. Notice that sum of S0C, S1C and EC is 10m as specified through -Xmn10m JVM option.
Java VisualVM with Visual GC
If you want to see memory and GC operations in GUI, then you can use jvisualvm tool. Java VisualVM is also part of JDK, so you don’t need to download it separately. VisualVM-Visual-GC-Plugin
Tuning
Tuning Heap Size
Java provides a lot of memory switches that we can use to set the memory sizes and their ratios. Some of the commonly used memory switches are:
VM Switch
VM Switch Description
-Xms
For setting the initial heap size when JVM starts
-Xmx
For setting the maximum heap size.
-Xmn
For setting the size of the Young Generation, rest of the space goes for Old Generation.
-XX:SurvivorRatio
For providing ratio of Eden space and Survivor Space, for example if Young Generation size is 10m and VM switch is -XX:SurvivorRatio=2 then 5m will be reserved for Eden Space and 2.5m each for both the Survivor spaces. The default value is 8.
-XX:NewRatio
For providing ratio of old/new generation sizes. The default value is 2.
-XX:PermGen
For setting the initial size of the Permanent Generation memory
-XX:MaxPermGen
For setting the maximum size of Perm Gen

Tuning Garbage Collection Algorithm
Garbage collection is expensive. Generational garbage collectors have the JVM  memory divided into several spaces.
Eden space: All objects are placed here when first created
Survivor spaces: One or more regions where objects mature
Tenured space: Where long lived objects are stored
Permanent generation: This area is only used by the JVM itself to hold metadata, such as data structures for classes, methods, interned strings

Java Garbage Collection Tuning should be the last option you should use for increasing the throughput of your application and only when you see drop in performance because of longer GC timings causing application timeout.

If you see java.lang.OutOfMemoryError: PermGen space errors in logs, then try to monitor and increase the Perm Gen memory space using -XX:PermGen and -XX:MaxPermGen JVM options. You might also try using -XX:+CMSClassUnloadingEnabled and check how it’s performing with CMS Garbage collector.

If you are see a lot of Full GC operations, then you should try increasing Old generation memory space.

Overall garbage collection tuning takes a lot of effort and time and there is no hard and fast rule for that. You would need to try different options and compare them to find out the best one suitable for your application.


JVM Threads
 green threads are threads that are scheduled by a virtual machine (VM) instead of natively by the underlying operating system. Green threads emulate multithreaded environments without relying on any native OS capabilities,

On a multi-core processor, native thread implementations can automatically assign work to multiple processors, whereas green thread implementations normally cannot. Green threads can be started much faster on some VMs.
Green threads significantly outperform Linux native threads on thread activation and synchronization.
Linux native threads have slightly better performance on I/O and context switching operations.
