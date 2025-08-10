
### Generics
We want code to work the same way regardless of the type of what is being added to it. This is known as parametric polymorphism

A generic class that is parameterised on a type is written as: `public class Thing<T>`. The type is specified at runtime.

Many OO languages support parametric polymorphism. 

It can only be implemented on a sub-class of a specific type (including any Object).

```java
public class GenericArray<T>
{
	// Any object
}


public class GenericArray2<T extends Animal>
{
	// if someone tries to make an array of Strings, they are not Animals, so it will not compile
	// if someone tries to make array of Tigers, they are, so this *will* compile.
}
```


### Boxing
Problem: on basic data types such as int, char, float, etc., these are not objects. To allow these to be added to generic types that require objects, we change them to be capitalised - Integer wraps an int, Float wraps up a float.

Boxing is the idea of wrapping the data into the box.

If we need to do this, the compiler will usually do this automatically: this is known as **auto-boxing** (into an Object) and unboxing (turning it back to an int). ==**The key is that the parameterised type should be \<Integer>, not \<int>.**== The object is then immutable.

> if we care about efficiency, it may be more efficient to create an array of `int`s not `Integer`s as there is no boxing needed


### Type Erasure
Because types do not exist at runtime, types are “erased” during compilation, so the runtime sees it as a base-class type like an Object.

The real class will not be known at tuntime

We CAN use the class type at compile time