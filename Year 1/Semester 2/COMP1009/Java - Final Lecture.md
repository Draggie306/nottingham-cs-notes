There are usually many good ways to solve a problem - small problems have been solved before. 

It is usually better to split a task into multiple classes if it has multiple types of responsibilities. 


Creational patterns are patterns related to the creation of objects, not just `new MyClass()`.

#### Singletons
A singleton object is a single object with 

We keep track of one object created in a static member variable. **The key is that there is no other way of creating an object.**

```java
public class Singleton
{
	static Singleton oneObject = null; // only create when needed
	
	private Singleton() {} // Constuctor is private so nothing outside can create it
	
	static Singleton get()
	{
		if ( oneObject == null )
			oneObject = new Singleton();
		return oneObject;
	}
}
```

![[Pasted image 20250324141914.png]]


#### Factory
A factory is an object which makes other objects.

We firstly create a factory object, which then makes other objects.

We do not care what the factory object is. Instead it returns objects of a different class.

It is useful to hide the actual classes that are used, so implementations deal with the factory call as if they are from the base class.

It also allows side effects of the creation method, e.g. allowing us to keep track of the number of objects creared.

![[Pasted image 20250324144238.png]]


Data hiding
It is common practice to not access daa directly. Methods are made public so that can be called and manipulate the data

