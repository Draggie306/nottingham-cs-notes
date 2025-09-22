
Code doesn’t match class descs:
- We can change whatever we want - class descriptions, code, etc. The aim is to get people talking


**Emergency Changes**
Emergency changes: often problems occur that require immediate changes to the code, deprioritising changes to the documentation. Emergency changes should still be documented.


**Refactoring**
> Refactoring is covered more in module 2013 (Developing Maintainable Software)


Over time, the cost of change gets very high: the client is requiring a lot of change or…


Changes occur during development
- In the waterfall model, change is not handled well. We have to restart from the top to add changes
- In the spiral model, changes can be approved and adapted with every cycle - allowing a faster 


Conclusion
- Code does not end after the delivery point
- There are different types of change - fixing bugs, adaption and new functionality (the latter is the most expensive)



### Agile vs Traditional (Lecture 16)
There are times when it is good to follow traditional methods and times when it is good to use agile development.

**Traditional methods**
Waterfall, V-model
Requirements Tables
Detailed UML/Specs
Integration Testing Phase
Formal User Testing 
Separate skill teams (have dedicated user tests, blackbox/whitebox testing)

**Agile methods**
Spiral/Scrum/Iterative Models
User Stories & Personas
Rapid Prototyping
CI, paired programming
Frequent client interaction at every stage


In 2001, agile really began to take shape. 17 people met at a ski resort to improve software engineering ideas - who had already invented SCRUM, TDD and other parts of Agile. They produced 12 key principles and 4 core values:

==To remember:==
- Individuals and interactions over processes and tools
- Working software over comprehensive documentation 
- Customer collaboration over contract negotiation
- Responding to change over following a plan (vs following the rigid stages in the waterfall model)


How

Traditional, plan-driven processes have a fixed scope but variable time and cost. 
Agile, iterative processes have this the other way round: fixed time and cost, variable scope.

Depending on the developer needs, we can be more or less agile. The overall approach can be agile, with **requirements, design, implementation and testing** all being agile, or perhaps changing design to have a traditional documentation with UML diagrams instead of an agile way.

![[Pasted image 20250324093725.png]]

### Techniques

#### Scrum 
optimised time and delivery

Sprints are fixed time periods to achieve the current plan - like 2-4 weeks. Within the sprint there may be daily scrum stand-up meetings to encourage continuous group communication. 

#### Kanban
> A continuous workflow by visually seeing work and speed of feature delivery

Instead of asking what shall be achieved in the current cycle, it focuses on what should be built next - in order of priority. 

#### Extreme programming (XP)
> Designed to improve team effectiveness, through practices like paired programming and test-driven development, ensuring quick AND working code

New versions may be built everyday (or more often), each passing all the tests before it is released. The general strategy is selecting a user story for a given release, breaking it into tasks and planning how it will be developed, integrated and tested, then released and evaluated.