
We will use Swing - an old library - as it illustrates OO design patterns

> To identify objects given a system description, look at the nouns, whilst operations and what is should to can be identified with verbs.

Libraries are sets of classes that work together. It is useful to understand what classes are available.

> “What I care about is what the program done, not what is stored”

There are similarities and big differences with ER diagrams and the OO implementation. In OO class fiagrams, we care about what is done and what is doing it, including objects and operations.

We may group projects differently, creating new objects to do some behaviour (even if they have no data) or split objects that have different behaviours.

A class library provides a set of classes for use, designed to be reusable. It is as generic and configurable as possible for reuse in another program. They tend to be designed to be configured to what we want to do.

Many jobs in a specific area require knowledge of a specific class library (and knowing where to search for to look at).



## Swing
The top-level window is likely a JFrame, with an automatic close button, minimise button, maximise, frame, with options for resizability etc. *It is really configurable.* 
> Swing allows us to change how things are drawn, e.g. changing to use X as a background colour.

The controls and components have a range of objects like JButton, JLabel, JTextField, JListBox - all of which are very configurable.

Other useful classes include the font to draw the text with and layout managers to refine ow it appears.
- We do not want to create a layout for every possible resolution, platform etc., so layout managers can be used to design each one

When working with the frame, work with the content pane of the frame and not the frame - *if we add menus, toolbars etc., then it becomes more difficult.*



![[Pasted image 20250224144750.png]]
