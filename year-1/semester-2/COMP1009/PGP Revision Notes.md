
# Functional Programming - Haskell

### Curried functions
> Named after Haskell Curry, who the language is also named after.

These are functions that takes an input and returns another function as a result. This is commonly used to input multiple arguments; it also allows for some functions to have a partial output if the second argument is not defined.

```haskell
add' :: Int -> (Int -> Int)
add' x y = x + y
```

This can be read as: add-prime takes in a single integer, and returns a function that takes a second integer and outputs the final integer.


### Lambda functions
Lambda functions are somewhat linked to curried functions in that they give a formal meaning to them. This means that the above example can be written as 

```haskell
add = \x -> (\y -> x + y)
```


### Higher-order functions
These are similar to curried functions in that they take in functions as an input and/or returns a function as a result 

### Recursive

Mathematical functions in particular are simpler to write declarative statements about when the functions are defined in terms of themself.

```haskell
factorial :: Int -> Int
factorial 0 = 1
factorial n = n * factorial (n - 1)
```

The three rules of recursive routines apply from other languages: functions must terminate at some point, have a base case, and for all other cases, perform an operation in terms of itself.

We can also define recursive functions in terms of lists:

```haskell
length :: [a] -> Int
length [] = 0 -- base case mapping
length (_:xs) = 1 + length xs -- successor of tail length
```



## Function types
Haskell provides a number of different ways to define and specify the result of functions. Each way is unique in terms of logic, efficiency and ease of use. Programmers may benefit from different definitions depending on their use case: Haskell is a functional programming language; after all, functions are the main characteristic of it. Haskell emphasises clarity, conciseness and correctness; therefore, programmers are given the option to implement  

### Conditional expressions
This is the most obvious way of defining a function, and may be the most familiar compared to other programming languages, such as one-liner if-else statements in Python. It consists of `if <condition> then <result> else <result>`. It may also be nested - multiple more `if`/`else` statements may exist within a parent `else` statement.

```haskell
signum :: Int -> Int
signum n = if n < 0 then 1 else 
			if n > 0 then 0 else -1
```

Note that all `if` keywords MUST also include an `else` keyword. This avoids a hugely ambiguous problem present in other, particularly non-functional programming languages: the dangling else problem. 

```java
if (condition)
	if (anotherCondition)
		doSomething();
else // Which "if" statement does this belong to?
	doSomethingElse();
```

As Haskell emphasises clarity and correctness, this is not a problem.

### Guarded equations

Guarded equations use the guard symbol `|` (meaning "such that") to perhaps more effectively show what a function is designed to do. The signum function above can be changed to:

```haskell
signum :: Int -> Int
signum n | n < 0 = 1
		 | n > 0 = -1
		 | otherwise = 0	
```

Here, `otherwise` is always True -- it is named as such in the prelude.
### Pattern matching
Pattern matching is a more explicit syntax that works well for a set of values that can be predefined, such as booleans.

```haskell
invert :: Bool -> Bool
invert False = True
invert True = False

(&&) :: Bool -> Bool -> Bool
True && a = a
False && _ = False
```

### List Patterns
List patterns are ways of manipulating a list of items. They are built with a series of `:` (construction) operators internally:

```haskell
[1,2,3,4]
-- means:
1:(2:(3:(4:[])))
```

It is common to get the head (first element) and tail (all other elements after) by using `x:xs` expressions.

```haskell
head :: [a] -> a
head (x:_) = x

tail :: a -> [a]
tail (_:xs) = xs
```


### Operator sections
Instead of using infix notation, operator sections can be used to define simple functions, such as the successor function used in discrete mathematics, in a prefix manner. 

For example:
```haskell
successor :: Int -> Int
successor a = a + 1

successor 3
```
can instead be written as:

```haskell
(1+) 3
```

or, for doubling:
```haskell
(*2) 3
```


## List comprehension

We can create new lists from old lists:

```haskell
[x^2 | x <- [1..5]]
-- creates a new list that has the square of all elements 1-5
```

Guards can be used with commas: 

```haskell
[x^2 | x <- [1..5], even x]
-- creates a new list that has the square of all EVEN elements from 1-5
```


## Lazy evaluation
This is a fundamental principle in Haskell. It combines outermost evaluation and the sharing of arguments.

```haskell
infinity = 1 : infinity

infinity
1 : infinity
1 : (1 : infinity)
1 : (1 : (1 : infinity))
```

Here, innermost evaluation will keep executing. The lazy evaluative statement will terminate after one step if the `head infinity` statement is used.

# Object-Oriented Programming - Java

## OO Design
OO systems are compositions of domain-specific object abstractions. 

An object has **state** (data), **behaviour** (methods) and **identity** (unique identifier).
Objects can communicate with each other synchronously (method calls) or asynchronously ("leaving a message").

### Decomposition
Reduces how much has to be considered at the same time. Fewer, interacting things (functions/objects) makes problems simpler to reason about. In OO, these are performed on objects.

## Java Basics
No global functions; all code and functions in classes. Functions are stored in memory and usually act on objects.

The `static` keyword means there is no object associated with the function. 
The `public` keyword means the variable/function is accessible outside the class.

Instead of `malloc()`, we effectively use `new Object`. Auto destroyed and free'd when no reference exists. The reference is the variable name, and a method is acted on it with `.`.
### Data types
int, float, boolean, double, long, char (2 byte number) and more (`byte` is a single-byte val).

String literals are String objects, so no `new` is needed. They are immutable.


### Clarifications
Class methods: static functions in the class - acts on the class, not the object (no `this`).

Instance methods: non-static functions.

Attributes: not typically static

`for ( String s : array )` - for each String (s) in the `array`

### Constructors
These are methods called automatically when an object is created. 

They are non-static functions with no return type and with the same name as the class. The default constructor does not have any parameters.
Parameters can be passed into constructors providing there is a constructor that expects that parameter. `new MyClass("Hello")`. A default constructor will be created automatically that does nothing if not specified.

Setters and getters are used to read/change an object's values (typically private).

`this` is the current object reference. It can typically be omitted, but useful when the object requires being specified.

### Static members
Functions and data not associated with an object, like `main`. 

`satic int count = 0;` could be defined and in the constructor, `count++;` called. The count of all elements created by the constructor is then shared across all objects.

### Generics
A generic has a \<type> added to the end of the name to say what type it works on, such as \<String>. When we parameterise a class on a generic type, it means that only the generic code that works with that type will be accepted and returned. Easier to understand, maintain, and enforce type safety at compile time.

Both `ArrayList<String>` and `ArrayList<Integer>` 

### Auto boxing
When an object is needed, the data type e.g. `int` is wrapped up into e.g. `Integer` (and the other way) automatically as needed. Generics do not work on primitives

## Aggregation
Aggregation and composition are important concepts: classes can be reused to create other classes.

- Aggregation: items have a lifetime of their own beyond the container they are in or part of (e.g. an Array inside the ArrayList will be there after ArrayList is destroyed)
- Composition: items only last as long as their containing item (the container typically creates the item, manages visibility, destroys alongside itself)

### Abstraction
Hiding all but the information the user needs to simplify usage. The knowledge of the implementation of classes is not needed to be able to use them. The `protected` scope does this.


## Inheritance, virtual functions
Inheritance (sub-type polymorphism) is an ==**IS-A**== relationship. A car is a vehicle, a motorbike is a vehicle. These classes are all specialisations of the vehicle class. Therefore, we can use `extends` to show this:
```public class Car extends Vehicle``` -> The `Car` (subclass) inherits all methods of `Animal` (superclass).

### Types of polymorphism

- Parametric polymorphism: code that works regardless of types. This is [generics](#generics) in Java. This is what FP means by polymorphic functions.
- Ad-hoc polymorphism: overloading functions, same function name but different parameters and parameter types. Caller will 
- Sub-type polymorphism: inheritance (the typical OO polymorphism).

### Access privileges
- Private - **only** this class.
- Package (default) - this class **and package** can access it.
- Protected - anything in this class, package **AND SUBCLASS**.
- Public - anything

### Class diagrams

- Association: something uses something else \[xxx]------\[yyy]
- Aggregation: something HAS A thing that stays after container; \[container]<>------\[contents]
- Composition; something HAS A thing integral to it/IS PART OF; black diamond \[x]◆---\[y]
- Is-A/type of/inherits: x IS A y; \[y]<|-----\[x]
	- Triangle points at base class

![[Pasted image 20250517164715.png]]

### Exceptions 
If an exception occurs, the function will end unless the thrown exception is caught. It should be caught in the function or the function labelled as `throws Exception` and caught by the caller.

They are used to report errors and must be caught with 
```java
try { 
	someFunc();
} catch (InterruptedException e) { 
	somethingHere();
} catch (Exception e) { 
	somethingHereAgain();
}
```


A Throwable object can be thrown. These include `Exception` and `Error`. `Error`s should not be caught and should never occur, Therefore, many subclasses inherit from `RuntimeException` (no throwing needed for these) which inherit from `Exception` which inherit from `Throwable`. IS-A relationship here.


## Design patterns

### Strategy
Used to delegate some responsibility from one class to another.
- Each responsibility has an associated interface that implements a set of functions.
- The strategy objects can implement the functionality in different ways.
- The main object (the context) has an object reference to the interface, which points to ONE implementer object (the strategy). 
- Whenever the context needs to perform a certain functionality, it asks the strategy to do it instead of itself.


### Observer
Used to allow other objects to get notified about something happening to the subject that is not essential for the subject to function.
- Each event to notify about has an interface that calls a related function to handle the notification
- The object being notified implements this interface in different ways with different fucntion implementations
- The observer registers the object with the subject; the subject has a list of objects to notify.
- When the subject needs to notify them, it treats the list of objects as the interface type and runs `notify()` on each.


### Singleton
A singleton only allows one instance of a class. We create the object in a static method and make the constructor private to never manually create an object of the class.
To get the object, we use a static getter to see if the singleton is null and if so, create it, else return the singleton object. This means that repeated requests will give the same object back.

```java
public class Singleton()
{
	static Singleton newSingleton;

	private Singleton() {};

	static Singleton get() {
		if (newSingleton == null) {
			newSingleton = new Singleton();
		}
		return newSignleton();
	}
}
```

### Factories
These are objects that create other objects.
They are useful as it allows the user/caller to treat the new objects as base class objects with hiding the actual class implementation, and allows side effects: things like counting the number of objects created, as object constructors always go through the factory.


### Iterators and iterables

Denoted with `implements Iterable<T>`. *This required a change to the language.*

```java
Iterator<Integer> it = array.iterator();
while (it.hasNext())
	System.out.println(it.next());

// can be written as:

for ( Integer i : arr )
	System.out.println( i );
```

- The container to iterate over is iterable (uses the iterable interface).
- The object that does the iteration is the iterator (that implements the `hasNext()` and `next()` functions).

## Collection classes, generics

When we use `class GenArray<T>`, the `T` is a type variable placeholder that will be filled with the real reference type when an instance of it is created. If specified as String, calling it later with Integer will not work. 

### Type erasure
Generics are implemented using type erasure. The type exists at compile time but not runtime. At runtime it sees it as Object. All `T` references are `Object`.  

It allows us to *not* manually require casting, allows us to specify the type going in and out of it, and permits the reusing of the same code.

Type safety is checked at compile time

```java
public class Wrapper<T>  
{  
    public T data;  
    public Wrapper( T value ) { data = value; }  
    // Other functions included here  
}  
  
Wrapper<String> wrappedString = new Wrapper<String>("Hello");
```

## Other key Java features

`final` keyword is like constants: their value cannot be changed once initialised. Likewise, methods cannot be changed in subclasses, making them faster as the jvm does not need to determine which version to run. And classes can be final to not be extended. 


### Anonymous classes
The name of the class is only used when creating the object, nowhere else.

When we `return new Iterator<T> () { ...` -- the curly brackets mean a new subclass with the given implementation will be created. This is useful as we do not have to create a new class (potentially somewhere different in the codebase) and call it if we only need a single object somewhere in the code.


### Lambdas
These are simpler syntax for anonymous classes ONLY when it subclasses **an interface with a single method**.
They use the `-> ` operator. 

	`button.addActionListener( e -> label.setText("Lambda")`
The compiler knows addActionListener expects an ActionListener object, which has a single method `actionPerformed()` and that this has a single parameter. We just tell it what `actionPerformed()` does -- here, it's setting text.