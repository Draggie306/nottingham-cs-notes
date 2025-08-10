### Patterns
Patterns allow us to identify ways in which a problem can be solved. We can identify the problem and look at how people have solved it in the past - results in much less thinking and working out. Some patterns are better than others, and usually the best solutions are the most common and widely-used ones.

> “has a “ - composition - X black diamond Y

The strategy pattern allows the objects’ behaviour to be changed at runtime. The strategies should be interchangeable - in this context, the code to use it should be the same regardless of the layout manager used


### Abstract classes and methods
A method without an implementation.

When we declare a function ==`public abstract String getName();`==, for example `Animal.getName()`, we **have to label the class as abstract**. And because of this, we cannot then instantiate the class with `class.new()` as a bit would be missing.

The idea is that we can use it to say that ”all objects in this class have this function but the superclass does not”.

#### Interfaces
Sometimes we may not need any implementations. We can use an **interface** instead - the assumption is that the classes that implement the interface must implement all functions (or be abstract). **The subclass MUST implement ALL functions**.

A subclass implements interfaces but extends a class: a class can only extend one class but can implement many interfaces.

```java
public interface Animal()
{
	String getName(); // no need to make it public or labelled abstract
	String makeNoise();
}
// An interface has no data
```

If classes have all abstract methods it is better to make it an interface as more things can be done with them.

> An interface can extend (make bigger) another interface as we are not *implement*ing it.
### JButton

The Swing library uses the Observer Pattern which uses the ActionListener interface which we write the implementation of the `actionPerformed()` function.

We need to run `button.addActionListener(this)`



We can use a random number generator with `static Random rand  = new Random() and rand.nextInt(upper_bound)`






