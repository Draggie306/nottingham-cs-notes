
### Coursework info

Coursework - 43 completed so far, 43 merge requests (merging completion of each version into main from dev). 4 issues had an accompanied merge request.

- Only 6 resolved issues had extra labels/tags
- Only 6 created a milestone for version 

### OO Design Principles

- Inheritance
- Polymorphism
- Encapsulation
- Abstraction

It is required to see a critical understanding of these principles in coursework, and SOLID principles too.

The whole point of developing software is that it is maintainable and can be re-used.  It should be easily adjustable. Design guidelines are SOLID.

- Single responsibility principle: a class should only have one responsible. If it has more than one responsibility, the class should be broken down.
	- Code becomes coupled if classes have more than one responsibility. Modifications risk affecting other parts of the class.
	- Classes with multiple responsibilities need to be split up - into multiple classes to help with re-use, testing, and minimal modifications required.
	- Methods should have one responsibility too, so they only do one thing.
- Open-closed principle: entities (classes, functions) should be open for extension, but closed for modification.
	- The behaviour can be extended (not just fixing bugs but adapt to new requirements) but nobody can make source code changes to it.
	- The idea is the main class is kept in-tact and change subclasses.

![](../../../Pasted%20image%2020251027132322.png)

- Liskov Substitution: subtypes must be substitutable for their base types.
	- Methods that use reference to base classes must be able to use objects of derived classes without knowing it - a way of using inheritance properly.

	- Birds (superclass) may have a fly() method, but not all birds e.g. ostrich (subclass) cannot fly.  
- Interface Segregation Principle: Clients should not be forced to depend upon interfaces they don’t use.
	- If a class wants to implement an interface, it must implement all methods.
	- If an interface has many methods, it must be broken down.	
	- It ensures that each interface has its own responsibility, to be specific, understandable and reusable
	- This is an extension of the single responsibility principle.
	- Instead of an appliance having many features, the features should be specific to e.g. SpeakerAppliance (which inherits and also adds e.g. `playSound()`), LightingAppliance (inherits; has `turnOn()` and `turnOff()`)

> In coursework, always justify why in comments/video

![](../../../Pasted%20image%2020251027133239.png)


- Dependency Inversion Principle: High-level modules should not depend on low-level modules. Both should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions.


![](../../../Pasted%20image%2020251027133656.png)
![](../../../Pasted%20image%2020251027133715.png)


A programmer without code sense can recognise a messy module. A programmer with good code-senes will see options and variations in the mess, and will be able to chose the best variation to plot transformations to make it better.



## Design patterns 

A design pattern provides an abstract description of a design problem and a general arrangements of elements the solves it. It identifies the participating classes and instances, their roles and collaborations, and the distribution of responsibilities. 

They are organised in 2 ways:


- Purpose: what the pattern does.
	- Creational: object creation (factory) - if we want to create many animals in a zoo.
	- Structural: composition of classes and objects.
	- Behavioural: how classes and objects interact and distribute responsibilities.

- Scope: whether it applies to classes or objects
	- Class: relationships between classes and sub-classes, fixed at compile-time
	- Object: deal with object relationships, changeable at runtime

> coursework: state why a design pattern is used in a given place, and why not others, for a particular scenario

















