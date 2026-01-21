### Coursework 2c and 2d info
Courseworks 2c and 2d: set up to do the UI and controller at same time with matching functionality. Ordered in how Jason recommends how to do it.

Controller: rules
Model: data
View: what it looks like
These are all interfaces; abstract classes without implementations for the functions


ReversiController extends base class SimpleController but with the implementations and rule checking added.

Do not put data e.g. who’s turn it is in the view.

Build whole controller first *then* test it. 

TestYourController is more useful than TestYourGUIView

- an important thing is also that TestYourController checks feedback messages in the returned string 