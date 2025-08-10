## OO
OOP: thinking of a program as interacting objects.

Procedural decomposition: split a problem into sub-tasks, e.g. fu[]()nctions calling other functions.

In OO, we still have these functions and procedures, but we perform these on the objects.

It does make things a lot easier to do - e.g. easily re-use code and adapt it, which makes it easier to debug by localising them. As it makes complex things easier, we can do more with it.

Java checks a lot more than C. Things like checking of array bounds, management of memory lifetime (so no “free()”).

Procedural programming has difficulties: variables can be changed in many different places, can be difficult to ensure the code works reliably. 

OO programming adds things to procedural programs rather than taking away. This is more intuitive for larger, real-world programs by dividing it into interacting objects.

It provides ways to more easily reuse and adapt existing code. We can write less code, use code already debugged and made by someone else, **and produce full software more easily.** There are object types and classes that already exist, so we can just join them together in our own way. Good OO design means designing classes/objects for easy reuse by others.

Even when programming in C, we may still think in an OO way - can do OO in C, with e.g. grouping specific functions in a way they are together, such as in a file, so we know what those may act on. However, it is much easer to do this in a dedivated OO language, and will likely look better and be easier to read than in C.

**An OO language is one that promotes or allows OO programming and design.**
Its features include:
- Objects (and classes)
	- Objects are the key feature - they are a collection of data and functions that work on that data
	- Classes are plans 
- Encapsulation (puts methods and data togerher)
- Data hiding (restricts access to data; only these set of functions can access some data)
- Composition (stronger than aggregation - can make object from another object(s))
- Inheritance (specialisation, reuse generic class but is also able to do *this*, without duplicating code. “take this class and add this”)
- Abstraction (when dealing with one object, don’t care about other ones or how it works)
- Polymorphism (function pointers without function pointer, change behaviour at runtime depending on how it is called, e.g. animal.makeNoise may make a squeak, meow, woof)


## Benefits of OO
It gives us an improved understanding of the program structure. It is more logical, reflecting the real world more accurately, which is especially useful in large programs, giving meaningful decomposition.
Another benefit is the ease of class re-
use, to adapt or extend existing work through classes. There is an ease of change, with modularity meaning that components and systems can be swapped and changed more easily.

Debugging is easer - someone else has debugged existing/imported classes, so we can just “plug things together” rather than working out how all the objects interacts. We can just look at which object there may be an error is and fix that one, and not worry about other ones.

## Java
The Java language has consistently been popular for decades and runs on many devices without recompiling. It is compiled to an intermediate byte code (.class files) which is executed on target devices inside a virtual machine. It can therefore be compiled on one platform and run on any. It’s not just taking the source code cross-platform and compiling it, it’s mostly compiling it and then moving it to another platform, and then it may either run immediately or perform a final “just in time” compilation on this device. **This is a huge benefit.**

Java is also simple - many C developers still code in C and not C++ because C++ adds lots of complexity. 

There are many libraries of reusable classes, which will do most of what you want to do already, reducing developer time. These libraries illustrate good OO design patterns (such as Swing) - prioritising OO design rather than speed unlike in C++. 

This is built on in Year 2 with C++. Java, C, C++ and C# are good for jobs and used in later modules and years.

> This is not a course on Java, but one about the Object Oriented paradigm.
#### The Syntax
Similar to C/C++/C# but without pointers. Can’t do “if (var)”.

Many syntactic similarities e.g. declaring variables, conditionals, loops, functional calls and return values.

> It was made to be similar to C++, as there were many existing developers who knew this language. The differences and changes made were deliberate


## Classes and Objects
An object is the actual thing, that has some allocated memory, that contains some information about the object
Whereas a class is a blueprint/plan/design for the object - it says “ball has an X and Y coordinate, ball has a level of inflatedness”.

*There is a difference between defining what an object is and creating an instance of that in memory.*

> structs in C can be considered simple objects without behaviours.

```c
struct Person
{
		char* name
		int age
}

/* malloc an instance for Person */
```



In Java:
```java
public class Item
{
	String name;
	int id;
}

Item item = new Item();
Item.name = “Jason”;
Item.int_data = 24;
```
Note, no mallocs or frees here.


## More
We can add functions to classes without any data. It may not have functions or data, but it may have either or both.

Everything is labelled with access permisssions - public means anything can access it. Private means only functions **from in that class** can access it.

If data/methods are associated with the class, we do not need an object to use them. If methods are associated with a class (i.e. they do not act on any specific object), they are signified with the keyword **static**. 

public static means:
- public - can be called from outside the class (accessible from anywhere)
- static - not associated with an object
This means - ”I don’t need an object to call this function”

Static functions act as global functions - they are not associated with an object.

All top-level classes must also be public.

Eclipse may say to fix an error, we can use static functions. *This is not good OO practice*. Do not make all the functions or variables static - even though this may be used in all the examples.

## Lecture 2
Think about C without pointers

In Java, **all executable code must be in a class**. Functions are defined in classes, i.e. the implementation is in the file defining the class.

Functions are defined inside classes, that usually act on objects.

> An object is usually a set of data - and a set of operations that can be used on the object.

In Java, the main method array format is slightly different to C:

```c
(char* argv[])
```
becomes…
```java
(String[] args)
```

### Naming conventions
Class names should be in ThisTypeOfCase.
When names have multiple words, capitalise the first letterOfSubsequentWords.
Be consistent with braces \{ } - doesn’t matter if on new line or not (easier if it is for debug).


### The data types
int, float, boolean, double, long, char, etc. All the same as C.

However, a char type is of 2 bytes due to using Unicode vs ASCII.
A byte type is a single-byte value.

To create an object, we should use new() -  it is equivalent to malloc and initialisation of the object.

Assigning one object reference to another

#### Strings
Strings are built in to the language. With classes, we cannot simply do +, so they built it into the language for concatenation (think Python).🐍 


When we concatenate strings, be careful, as addition works from left to right.

![[Pasted image 20250203143448.png]]


#### Command line arguments
In C, we can work out what the program name was in argv\[0]. However, in Java, as we are running as a class, we do not have this, so the immediate first argv will be the actual first command line argument, **and NOT the file/executable name!**! There is also no argc.

To get the length of an array in Java, we can use `args.length`. 

### Memory and syntax
Java has no stack objects, but has stack objects with the flexibility of heap objects.  They act as heap objects with the tidiness and syntax of the stack object. They get automatically get cleared and freed. 


## Lecture 3

### Object-oriented design
OO systems are viewed as compositions of domain-specific object abstractions, rather than global data and functions. The class/object literally represents a “think” in the domain of the program.

An object is a domain concept that has:
- state - its 
- behaviour - methods
- identity - a unique identifier, e.g a memory location

Objects also intercommunicate, such as by sending messages to each other. This can be done in two ways:
- synchronous - interacting in realtime, expecting a response, waiting until it the conversation finished
- asynchronous - leave a message/email, and at some point it will be responded to but can do something else when waiting for the response. “set some data to something that something else will look at later”

### Objects and classes

getters and setters: these are very simple classes that can get/set the values of the data of an object.
> These should not be “static” variables as they will not reference any object, which is required when setting/gerring values of a specific object.

Procedural decomposition splits the porgram into a number of procedures and functions that group operations, howecer, having fewer things interacting means 



### Class libraries
Java classes exist for most of what we want to do - we can use them by creating instances (objects) and then calling our methods on the objects.

We do not need to know how “PGPText” or “PGPFile” classes work in order to use them - e.g. we just need to know how to use “.open()” - we **act on an object**. This is abstriction.

Aggregation and composition is an easy way to use existing code without needing to copy and paste - to create a class that contain another class (this is a HAS-A relationship: so that objects of a class have one of the aggregated/composed objects inside it). Objects which use the container don’t need to know 

## Inheritance & (sub-type) polymorphism
> Subclassing/`extends` in java.

Most design patterns in OO use inheritance due to it being malleable and usable everywhere!

If all animals (class) can breathe, and a tiger (another class) is an animal, then everything one can do with the animal must also be able to be performed on the tiger.    


```Java
public class Animal
{
	public String getName()
	{
		return “I am an animal”;	
	}

	public String getNoise()
	{
		return “Unknown noise”;
	}
}
```

To add a type (subclass) of an animal, we can use an IS-A relationship using the `extends` keyword.

```java
public class Bear extends Animal
{
	@override
	public String getName()
	{
		return “I am a bear”;
	}

	@override
	public String getNoise()
	{
		return “grrrrr”;
	}
}
```

```Java
…

Animal animal = new Animal();

Animal bear = new Bear();

// printing out bear.getNoise() will print “grrrrr’

```


A new class that extends another automatically gets/inherits everything from the parent class.

The `@override` tells the compiler that this override for a function that is in the base class - and is useful for ensuring there are no typos.

If we change a function we have a new version, if we don’t change the function, we still have a function.


The original class is the superclass/base class. The new extending class is the subclass/derived class. As soon as it extends, it will inherit the functions in the superclass — but the good thing is that the original piece of code can be modified/change a few functions without needing to copy and paste code.

When we call a function on the Animal type reference, the same function on the subclass of the Animal class is called. 

This is runtime polymorphism - the compiler does not do this, but the program looks this up at runtime and decides which function - there is one extra function lookup that must occur.

A table of functions - if extends, it will add/remove/change functions in this table.

### Polymorphism
There are three main types of polymorphism.
- Parametric polymorphism - code works with multiple types or runs regardless of types. E.g. function can run with an int, float, double, etc.
- Ad-hoc polymorphism - function overloading. The idea is having multiple functions with the same name, but with different parameters. The function that will be called is the one that takes in the appropriate parameters, for instance two ints, two strings, etc.
- Sub-type polymorphism - sub-classing


## Scoping
### Packages
Packages are groups of similar classes within a single directory.

If a class in the same package as another class, there is high privilege going to it - known as package-level access.

> `animal.Animal` - get the `Animal` class from the package (directory) `animal`.

We could import `animal.Fish`, `animal.bear` individually, OR we can use `import animal.*;`. Packages are ***import***ant.

### Access Specifiers
There is a hierarchy of accessed specifiers.

The idea as we can limit the access depending on the interface we want to be able to be accessed. 

It is standard that we keep the access priviliges the same if we extend in a subclass. HOWEVER, if we need to change the access specifier, it can be less privileged but not more privileged. BUT, private functions in a subclass can be changed to any access specifier as the original ones are effectively not in scope at all, so it is effectively is completely a new function.
#### private
- Only this class - no subclasses - can access this
- “hidden the implementation details” - not the functions that should be called or accessed
#### package (default)
- Anything in this class and this package - but no subclasses - can access this
- This is not really a thing in any other language
#### protected
- Anything in this class, this package and any subclasses can access this
- Usually a good idea to have this - but only subclasses - so slightly annoying that anything in the package can access which can be an issue. It is also why typically there are lots of different packages - to allow subclasses 
#### public
- Anything can access this

So far:
![[Pasted image 20250220110525.png]]


### Class Diagrams 
We can use diagrams to represent the relationships between classes. This allows us to better understand the structure of a program.

Each class has a rectangle, with 3 sections. 
- The top is short - the name of the class. 
- The second section is all the members or attributes in the class
- The bottom section contains all the methods/functions of the class.
	From this, we can just look at a class and see all its functions and data.

Then, we can join a line for each relationship:
- To show that something that links 
- Aggregation: the side of the side with the diamond in the line contains one of the other side. (Something else may also)
- Composition: If the diamond is solid, then it shows a “has a” relationship that is integral to the relationship.
- Is-A/type of: triangle that is always on a base class/superclass side of the relationship. For example Animal <|—— Bear.

> **The diamond always goes on the container, and triangle on the base class, end.**

![[Pasted image 20250220111334.png]]
PGPText has a list that is essential to it, so it is composition. The strings added to the ArrayList could just be literal strings, so exist outside the array list.


All classes are subclasses of class “Object”. It always extends based on inheritance and the very base class that is hidden is always Object which has a few functions like toString or getHash of it.

## Exceptions
When we call a function, we cannot guarantee it will not end in an unusual way.


Functions can be declared with `throws Exception`. Exceptions exist, they are real, and they can be dangerous to the program.

Functions will suddenly end when an exception is thrown, and if there is no handling of this exception, it is passed back to the caller. 

If a function can raise exceptions then we must:
- Catch the exception in the function
- Label the function so that is clear that it raises an exceptions.
Therefore, we are essentially forced to catch anything thrown.

> Runtime exceptions do not require the function to be labelled so do not use it.

Not handling all exceptions will risk terminating the program.

```java

try {
	doSomething ( i );
}
catch ( InterruptException e )
{
	System.out.println( “Interrupted: “ + e.getMessage() );
}
catch ( Exception ) // wildcard for any
{
	System.out.println( “okay” )
}
```

Any Throwable object can be thrown, not just an Exception objet.
Throwable has two subclasses:
- Exception
- Error - don’t use this unless there is a very bad error that cannot be recovered from.

#### Danger of RuntimeExceptions
RuntimeExceptions happen because something common happens, instead of ‘exception’al circumstances. It covers things that are not predictable or are common, such as IndexOutOfBoundsException. As these are subclasses and inherit, there is no explicit labels required.

Therefore, when we need to throw an Exception, don’t use a RuntimeException and instead use an Exception (or subclass of). 

![[Pasted image 20250220114101.png]]

Exceptions from a constructor (`new()`)stop the creation of a new object and allow us to handle an error, since they do not return a value


### PGPFile
If false is returned, then this is a wrapper for an exception, on both read/writing from lines will return False if there was an exception thrown.

We set br = null to tell the system that it no idlonger refers to a valid object - as the JVM manages running memory.

> `system.gc();` encourages garbage collection but not guaranteed.