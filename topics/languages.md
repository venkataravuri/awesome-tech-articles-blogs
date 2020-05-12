Java, JUnit
Java
Lambda Expressions
Functional Programming
Difference between Deep Copy And Shallow Copy?
Is it possible to override the main method?
How HashMap works?
How ConcurrentHashMap works?
What is difference between Weak, Soft & Hard references?
What is WeakHashMap?
How Annotations work? You might have used @Override and @Deprecated
What is immutable object? What are the guidelines create one?
What is marker interface? Can you name few marker interfaces?
Why serialisation has no methods?
What is difference between Comparable and Comparator interface?
How does HashSet not allows duplicates?
What is the importance of hashCode() and equals() methods? How they are used in Java?
How Generics implemented in Java ? What is type erasure?
What are different class loaders in Java?
What technique Java Profile employ to get execution details? What is byte code instrumentation?
ConcurrentLinkedQueue
JUnit
setUp() and tearDown() code once for all of my tests?
How Mock injection works?

Java
Lambda Expressions

A Java lambda expression is thus a function which can be created without belonging to any class. A lambda expression can be passed around as if it was an object and executed on demand.

A lambda is just an anonymous function - a function defined with no name.

Lambda expressions in Java is usual written using syntax (argument) -> (body). For example:
(arg1, arg2...) -> { body }
 (type1 arg1, type2 arg2...) -> { body }

Matching Lambdas to Interfaces
A single method interface is also sometimes referred to as a functional interface. Matching a Java lambda expression against a functional interface is divided into these steps:
Does the interface have only one method?
Does the parameters of the lambda expression match the parameters of the single method?
Does the return type of the lambda expression match the return type of the single method?


a Functional Interface is an interface with just one abstract method declared in it.

java.lang.Runnable is an example of a Functional Interface. There is only one method void run() declared in Runnable interface. Similarly ActionListener interface is also a Functional Interface.


@FunctionalInterface
public interface WorkerInterface {
    public void doSomeWork();
 }

list.forEach(n -> System.out.println(n));

Each lambda expression can be implicitly assigned to one of the interface called Functional interface.


int sum = list.stream().map(x -> x*x).reduce((x,y) -> x + y).get();
System.out.println(sum);

.stream() method to convert regular list into a steam.
lambda expression x -> x*x to map() method which applies this to all elements of the stream
This is also a starters example on MapReduce. We used map() to square each element and then reduce() to reduce all elements into single number.

http://viralpatel.net/blogs/lambda-expressions-java-tutorial/

Functional Programming
https://medium.com/javascript-scene/the-two-pillars-of-javascript-pt-2-functional-programming-a63aa53a41a4#.gti2byjtl

Functions are first class citizens in a functional programming language. They exists on their own. You can assign them to a variable and pass them as arguments to other functions

Difference between Deep Copy And Shallow Copy?
http://www.jusfortechies.com/java/core-java/deepcawopy_and_shallowcopy.php

Java is always pass-by-value. The difficult thing can be to understand that Java passes objects as references and those references are passed by value.

http://www.javaworld.com/article/2077424/learn-java/does-java-pass-by-reference-or-pass-by-value.html 

Java copies and passes the reference by value, not the object. Thus, method manipulation will alter the objects, since the references point to the original objects. But since the references are copies, swaps will fail.
   
Is it possible to override the main method?
No,  because main is a static method. A static method can't be overridden in Java.
How HashMap works?
HashMap works on principle of Hashing. A map by definition is : “An object that maps keys to values. 

To store such structure, it uses an inner class Entry:
static class Entry implements Map.Entry{
final K key;
V value;
Entry next;
final int hash;
...//More code goes here}
Here key and value variables are used to store key-value pairs. Whole entry object is stored in an array.?

transient Entry[] table;
The index of array is calculated on basis on hashcode of Key object.
A hash map consists of buckets; objects will be placed in these buckets based on the bucket id. Any number of objects can actually fall into the same bucket based on their hash code / buckets length value. This is called a 'collision'.

HashMap class is roughly equivalent to Hashtable, except that it is unsynchronized and permits nulls.
HashMap is non synchronized whereas Hashtable is synchronized.
Iterator in the HashMap is fail-fast while the enumerator for the Hashtable isn't.
HashMap can be synchronized by  Map m = Collections.synchronizedMap(hashMap);
How ConcurrentHashMap works?
All operations are thread-safe, retrieval operations do not entail locking, and there is not any support for locking the entire table in a way that prevents all access. This class is fully interoperable with Hashtable in programs that rely on its thread safety but not on its synchronization details.
What is difference between Weak, Soft & Hard references?
Weak reference is a reference that does not protect the referenced object from collection by a garbage collector. It is a reference that isn't strong enough to force an object to remain in memory. An object which is only weakly reachable (the strongest references to it are WeakReferences) will be discarded at the next garbage collection cycle, but an object which is softly reachable will generally stick around for a while.
Four types of references in java and they are strong reference, weak reference, soft reference and phantom reference. 
What is WeakHashMap?
WeakHashMap is an implementation of the Map interface that stores only weak references to its keys. Storing only weak references allows a key-value pair to be garbage collected when its key is no longer referenced outside of the WeakHashMap.
How Annotations work? You might have used @Override and @Deprecated
Annotation is Metadata for code. When compiling code with annotations, compiler runs an annotation processor. The annotation processor generally uses the Reflection API to inspect the elements being compiled and may simply run checks on them, modify them, or generate new code to be compiled.
The first main distinction between kinds of annotation is whether 
they're used at compile time and then discarded (like @Override) or 
placed in the compiled class file and available at runtime (like Spring's @Component). 
                                                    "String is read-only and immutable. StringBuffer is used to represent characters that can be modified.
StringBuffer is faster when performing concatenations. This is because when you concatenate a String, you are creating a new object (internally) every time since String is immutable.
StringBuilder is similar to StringBuffer except it is not synchronized.
StringBuffer does not override the Object.equals method, so it is not performing a string comparison.
What is immutable object? What are the guidelines create one?
An object is considered immutable if its state cannot change after it is constructed.
1. Don't provide ""setter"" methods — methods that modify fields or objects referred to by fields.
2. Make all fields final and private .Don't allow subclasses to override methods. The simplest way to do this is to declare the class as final. A more sophisticated approach is to make the constructor private and construct instances in factory methods.If the instance fields include references to mutable objects, don't allow those objects to be changed:
3. Don't provide methods that modify the mutable objects.Don't share references to the mutable objects. Never store
references to external, mutable objects passed to the constructor; if necessary, create copies, and store references to the copies. Similarly,  create copies of your internal mutable objects when necessary to avoid returning the originals in your methods.
 What is marker interface? Can you name few marker interfaces?
The java.io.Serializable interface  and Cloneable are typical marker interfaces.

In Java, a Marker interface is an interface with no methods or fields declaration. In simple words, marker interface is an empty interface. 
Why serialisation has no methods?
The serialization interface has no methods or fields and serves only to identify the semantics of being serializable. Classes that do not implement this interface will not have any of their state serialized or deserialized.
Serializable interface is a marker interface which only notifies JVM that a certain object is set to be serialized. The serialization process happens internally.
What is difference between Comparable and Comparator interface?
Comparable and Comparator interfaces are used to sort collection or array of objects.
Comparable interface is used to provide the natural sorting of objects and we can use it to provide sorting based on single logic. Comparable interface has compareTo(T obj) method which is used by sorting methods.
Comparator interface is used to provide different algorithms for sorting  and we can chose the comparator we want to use to sort the given collection of objects.
 use Comparator interface because Comparable.compareTo(Object o) method implementation can sort based on one field only and we can’t chose the field on which we want to sort the Object.    

Queue allows retrieval of element in First-In-First-Out (FIFO) order
Stack is similar to queue except that it allows elements to be retrieved in Last-In-First-Out (LIFO) order.
Map — an object that maps keys to values. A Map cannot contain duplicate keys; each key can map to at most one value.
Set — a collection that cannot contain duplicate elements.
List — an ordered collection (sometimes called a sequence). Lists can contain duplicate elements.
SortedMap — a Map that maintains its mappings in ascending key order. This is the Map analog of SortedSet. Sorted maps are used for naturally ordered collections of key/value pairs, such as dictionaries and telephone directories.
iterator - An Iterator is an object that enables you to traverse through a collection and to remove elements from the collection selectively, if desired.
How does HashSet not allows duplicates?
When you put an object into a Hashset, it uses the object’s hashcode value to determine where to put the object in the Set. But it also compares the object’s hashcode to the hashcode of all the other objects in the HashSet, and if there’s no matching hashcode, the HashSet assumes  that this new object is not a duplicate.
In other words, if the hashcodes are different, the HashSet assumes there’s no way the objects can be equal! So you must override hashCode() to make sure the objects have the same value. But two objects with the same hashCode() might not  be equal. so if the HashSet finds a matching hashcode for two objects—one you’re inserting and one already in  the set—the HashSet will then call one of the object’s equals() methods  to see if these hashcode-matched objects really are equal.
What is the importance of hashCode() and equals() methods? How they are used in Java?
The java.lang.Object has two methods defined in it. They are:
public boolean equals(Object obj)
public int hashCode(). 

Whenever a.equals(b), then a.hashCode() must be same as b.hashCode(). But two objects with the same hashCode() might not  be equal.
How Generics implemented in Java ? What is type erasure?
A generic type is a reference type that has one or more type parameters.
A generic type is a type with formal type parameters. A parameterized type is an instantiation of a generic type with actual type arguments.

 Example (of a generic type):

    interface Collection<E>  {
      public void add (E x);
      public Iterator<E> iterator();
    }
Example (of a parameterized type): 
Collection<String> coll = new LinkedList<String>();


Generics is implemented using Type erasure, compiler erases all type related information during compile time and no type related information is available during runtime.

For instance, the parameterized type List<String> is translated to type List , which is the so-called raw type .  The same happens for the parameterized type List<Long> ; it also appears as List in the bytecode. 

What are different class loaders in Java?
ClassLoader loads a java class file into java virtual machine. They are be broadly classified into,
Bootstrap class loader loads java’s core classes like java.lang, java.util etc. These are classes that are part of java runtime environment.
Extensions Class Loader JAVA_HOME/jre/lib/ext contains jar packages that are extensions of  standard core java classes. Extensions class loader loads classes from this ext folder. Using the system environment propery java.ext.dirs you can add ‘ext’ folders and jar files to be loaded using extensions class loader.
System Class Loader Java classes that are available in the java classpath are loaded using System class loader.

What technique Java Profile employ to get execution details? What is byte code instrumentation?
Bytecode instrumentation adds additional lines of bytecode before and after specific method calls within a class, and this can be done by intervening with the class loader.

ConcurrentLinkedQueue 
ConcurrentLinkedQueue employs an efficient "wait-free" algorithm algorithm by Maged M. Michael and Michael L. Scott.

An unbounded thread-safe queue based on linked nodes. ConcurrentLinkedQueue is an appropriate choice when many threads will share access to a common collection.

It's good when you may have hundreds or even thousands of threads accessing the queue at the same time.

ConcurrentLinkedQueue is not only non-blocking, but it has the awesome property that the producer does not contend with the consumer. In a single producer / single consumer scenario (SPSC), this really means that there will be no contention to speak of. In a multiple producer / single consumer scenario, the consumer will not contend with the producers.

offer(E e)
poll()

Static Nested Class
A static inner class is a nested class which is a static member of the outer class. It can be accessed without instantiating the outer class, using other static members. Just like static members, a static nested class does not have access to the instance variables and methods of the outer class. The syntax of static nested class is as follows:

class MyOuter {
   static class Nested_Demo{
   }
}
Inner Class (Non-static Nested Classes)

Inner classes are a security mechanism in Java. We know a class cannot be associated with the access modifier private, but if we have the class as a member of other class, then the inner class can be made private. And this is also used to access the private members of a class.

Unlike a class, an inner class can be private and once you declare an inner class private, it cannot be accessed from an object outside the class.
JUnit
JUnit is a open source framework to write and run repeatable tests. JUnit features include:
Assertions for testing expected results
Test fixtures for sharing common test data
Test runners for running tests

Frequent testing gives you confidence that your changes didn't break anything and generally lowers the stress of programming in the dark.

Test fixtures
    private Collection<Object> collection;
 
    @Before
    public void setUp() {
            collection = new ArrayList<Object>();
    }


@Test(expected=IndexOutOfBoundsException.class)

setUp() and tearDown() code once for all of my tests?
    @BeforeClass
    public static void oneTimeSetUp() {
            // one-time initialization code        
    }

Here's an example of how I got my tests working with Spring 3.1, JUnit 4.7, and Mockito 1.9:

FooService.java
public class FooService {
    @Autowired private FooDAO fooDAO;
    public Foo find(Long id) {
            return fooDAO.findById(id);
    }
}

FooDAO.java

public class FooDAO {
    public Foo findById(Long id) {
        /* implementation */
    }
}

FooServiceTest.java

@RunWith(MockitoJUnitRunner.class)
public class FooServiceTest {
    @Mock private FooDAO mockFooDAO;
    @InjectMocks private FooService fooService = new FooService();

    @Test 
public final void findAll() {
            Foo foo = new Foo(1L);
        when(mockFooDAO.findById(foo.getId()).thenReturn(foo);

        Foo found = fooService.findById(foo.getId());
        assertEquals(foo, found);
    }
}

@Mock annotation mocks the concerned object.

@InjectMocks annotation allows to inject into the underlying object the different (and relevant) mocks created by @Mock.
How Mock injection works?
Mockito supports dependency injection by using constructor arguments, setter methods and field injection. The underlying implementation relies on reflection, which means that there is no dependency on the Java EE 6 or Spring annotations as far as Mockito is concerned 

