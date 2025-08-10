
**Coursework hints** - 17/03/2025
![[Pasted image 20250317140426.png]]


Look at the simple text view which has all functionality for the view - but just as text.

Type erasure: by the runtime, types are removed (at compile time, they are still there). 


The inner class object knows about the outer class objects it is associated with. Unless we add an operation ourselves, the outer class does not know its inner classes.

The inner class HAS A outer class object. `Inner <>—— Outer`

```java
// For all strings in list, their variable name is str and print it.
for ( String str : list ) 
{
	System.out.println( str );
}
```

Each iterable must implement an iterator. The iterator supports hasNext (bool) and next (the next element)

