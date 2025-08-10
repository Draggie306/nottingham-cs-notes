**Recap**
THere is a standard way of having iterator objects in Java. The iterator implements the iterator interface: as it does this, we know OurIterator is treated as an Iterator — it must support `hasNext()` and `next()`

**Anonymous Classes**
An anonymous class is one where the class is only used in one place. There is no need to put it into a class, and there is no point having 

```java
// these brackets mean that a new nameless subclass will be created with the below data.
return new Iterator<T>() 
{
	int index = 0;

	@Override
	public boolean hasNext()
	{
		// ...
	}
}
```

When we see `{` after the `()`, this means “create a new subclass of the class with the following implementation”.

> This used to be the most common way of implementing GUIs.

In summary, an anonymous class is an inner class without a name. Instead of extending/implementing a class/interface, we can name the base class and give the implementation of the changes.


### **Lambda expressions**
In Java, lambdas are a simpler implementation for an anonymous class when it subclasses an **interface** with **only one method**.


> ==Arrow operator `->` means lambda expression==

```Java
button2.addActionListener (
	e -> label.setText(“text”)
);

// Actionlistener is an interface with only one method: actionPerformed. It takes in an ActionEvent 
```

The lambda name knows it has to have a type in that subclass, so there is no point writing it out.

To have multiple parameters, the lambda can be defined as `(x,y)->x+y`

**Variable capture**
Lambdas can capture any variable that is effectively “final” - its value cannot be changed later on. As long as the variable in the function does not change it can be captured in the 


![[Pasted image 20250319105007.png]]
