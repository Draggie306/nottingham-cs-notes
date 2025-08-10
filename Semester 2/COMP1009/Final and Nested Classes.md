
## CW Recaps
Create 1 view, model and controller. once all 3 are created, each is initialised in turn, with each object receiving the other two object reference to enable intercommunication


## Keyword: final
Means the function is unchangeable/immutable. Variables can be final -> they cannot be changed, they are a constant.

A function made final means it cannot be overridden - a subclass cannot have a new implementation of that function - cannot be extended. *A benefit of this is a speed gain as there is no need to check the version to run.*


![[Pasted image 20250310141428.png]]

**Strategy pattern**
- One class has multiple responsibilities. Wants the ability to mix and mach responsibility
- For each responsibility, there is one **(and only one)** object reference associated with it that performs the functionality - **otherwise it will not work.**
> This delegates work to another class. The calling function does not know/care how it executes.
- For layout managers, it does not care what type of layout manager it is and how it is implemented. The interface method can be called, without caring how it is implemented, and we just know it does something relevant (implementing all the functions from the interface).

> ==**Note: this below differentiation is important for exam**==

**Observer pattern**
- There does not need to be strictly one “parent” - zero or more.
- Has a list of observers to tell and once an event happens, tell everything in the list (that wants to know)
- Doesn’t need something for the functionality, but it can notify objects that are interested in it.


## Nested Classes

Classes can be defined inside classes, which is sometimes useful when a class is only used by the surrounding class

Static means not associated with an object.

```java
public class Outer
{
	public static class NestedStatic
	{
		public void foo() {}
	}

	// Is associated with a specific object of the outer class
	public class InnerClass
	{
		public void ...
	}
}
```

From this, in a main class, we can:
```java
public static void Main(String[] args)
{
	Outer.InnerClass ob3 = ob1.new InnerClass();
}
```

> We almost always create an object from the outer class from the method we are in


Class defined in class

If class inside is static, it does not have a specific object (and cannot do `this`)


Use mousePressed() in the coursework to verify against if the mouse has change positions 