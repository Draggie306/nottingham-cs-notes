
### Recap
In OO, we:
- identify the objects we need, understand the class library when using one.
- create the objects - using existing or new classes
- customise/extend the objects to add functionalities

### Swing behaviour
When we use the swing library, the process creates a new thread when `setVisible()` is called. DO not do anything with the UI objects we have created, e.g. `GUIFrame()` after we have called `setVisible()`. By design, Swing is not thread-safe.

> Given X threads, the program can do X things at once.
> Problems will arise when two threads do something on the same thing.


> Constructors: public function with no return type, have the same name as the class.

When a class extends another class, the new class has all the base class’s methods and attributes by default. 

To refer to the current object being created in a constructor, we can use `this`.

If our constructor has the `super.`, we can call the original version of base class.

We cannot default values in parameters by doing e.g. `=0` so instead Java allows us to call another constructor with default values instead. 




JPanel is a container. there can be many panels that contain panels, buttons, labels etc. Because it is a container, it needs to know how to lay out its components. 

`panel3.setLayout( new FlowLayout() )`

There are a variety of layout managers:
- FlowLayout()
- BorderLayout()
	- This divides the panel into a north, south (highest priority), east, west (2nd most priority) and centre 
- GridLayout()
	- 






We can call another constructor from the same class if it 

Eclipse: ctrl+shift+o to 
