
## OO
OOP: thinking of a program as interacting objects.

Procedural decomposition: split a problem into sub-tasks, e.g. functions calling other functions.

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

> These should not be “static” variables as they will not reference any object, which is required when setting/getting values of a specific object.

(If defined the same class, we can still edit the private/protected value directly!)

Procedural decomposition splits the porgram into a number of procedures and functions that group operations, howecer, having fewer things interacting means 

### Identifying objects from a system description
When we have a system description, we can work out many of the objects with each noun in the description.

### Class libraries
Java classes exist for most of what we want to do - we can use them by creating instances (objects) and then calling our methods on the objects.

We do not need to know how “PGPText” or “PGPFile” classes work in order to use them - e.g. we just need to know how to use “.open()” - we **act on an object**. This is abstriction.

# Live Coding

- Don’t click moduleinfo.java (if forget, then delete this file)
- Tick public static void main

In Java, we do not connect object files in the same way as C. At runtime, the relevant class files are loaded into memory if requested and then executed.

- `javac *.java` - compile all Java files from the command line directly.

Packages:
When creating a new package, it creates a new directory then places a file in that directory. The first line of the code in this file in the new dir is `package <folderName>`.

> All import does in Java is tell the current script where the package is, if it is outside of the current package.

Breakpoints will only work if the program is running in debug mode and not normally. *It can be useful to remove breakpoints especially if it is a huge file, before leaving/switching what file we are editing.*

`break;`: exit while loop

When we use `new()`, we get an object reference back that stores the object we just created. They are automatically destroyed when there is no reference to them.

Method/member function - a function that is a member of a class, i.e. defined within the function.
Class methods - a static function in a class, acting on a class instead of a specific object.
Instance methods are non static functions, acting on a specific object.

### Constructors
Constructors are something we make but we do not call it manually - it is called by default when creating an object.

A constrictor is a function in a class that is static, and has no return type, with the same name as the function.

```Java
class MyClass {
	public MyClass{ // Default constructor
		text = “some text”;
	}

	public MyClass ( String message ) { // This will be called if called with string as an argument
		text = message;
	}
}
```


If inside a non-static function, there is an implicit object reference: `this`. It refers to the current object.

Static members do not have this `this` object reference and is assocated with the class.

### Abstraction
We can use the functions without knowing exactly how they work. We don’t need to know the details or complexity


### Imports and packages
The code that we write will not be in packages for simplicity. 

All standard classes are in packages, and we usually need to say which package the class you want to use it from. The array list is in a package called `java.util.ArrayList` so we can use it with `java.util.ArrayList = new java.util.ArrayList<String>’`. 
Or we can just `import java.util.ArrayList;` to tell the compiler that every `ArrayList` is from this library.

![[Pasted image 20250212104045.png]]


### Aggregation/composition
If the lifetime of the things inside lasts/is indepent of the thing it contains, it is aggregation. “the container has a”

