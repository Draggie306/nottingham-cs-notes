
![](Pasted%20image%2020251110130650.jpg)

160 who have not done anything. 

Task 6: script will auto update javadocs and generate thousands of html lines. 


## Software architecture

Software architecture are the fundamental concepts or properties of a system in its environment, embodied in its elements, relationships and the principles of its design and evolution.

It represents the design decisions related to the system structure and its behaviour.

- High-level system components
	- *These are one or more services that may be used by other components.*
- How the significant are structured and organised
	- Not everything: component has some usable feature 
- Shared understanding of the design process
- Decide what is important or not for the software
- Design decisions the team needs to make

The working, better definition is those of the expert developers’ shared understanding of the system design. AND/OR the decisions that are hard to change, and the constraints we have.  The most important stuff in the software.

The user does not care about the code quality (internal quality), just that it has a good external design with pleasant UI and few defects. However, having a good modular design (internal quality) is good to be able to expand and re-use and build on, to sell to a customer.

Low internal quality = hard to add functionality. 

The architecural goal should be to minimize complexity: the more complex, the harder to maintain. More complex systems are more likely to introduce bugs and security vulnerabilities when being modified or extended.


Non-functional requirements such as:
- storing passwords securely
- should be available for 99.9% of the time excluding scheduled maintenance windows of 1 week notice
- should be compatible with the latest versions of browsers
- codebase should be well-documented and follow coding standards

... are all important to define and document, else a company may lose reputation and money (e.g. recent M&S breach -> passwords should be secure)

![](Pasted%20image%2020251110133427.png)


Example: here, there is no right or wrong solution. Left is slower because of shared database and right is faster, but syncing databases may involve complex logic. It is up to the company.
![](Pasted%20image%2020251110133613.png)

Regular product improvements are required for a long-term product lifecycle. 

The key decisions will require cost-benefit analysis to determine architecture and what to prioritised: compatibility, number of users, reusability, etc…

Trade-off: security versus usability: 
- a layered approach affects usability. Users will have to remember passwords, etc. To avoid this, there must not be too many layers of authentication to access, but enough such that the data itself (e.g. credit card database) is always kept secure. 

### Organising components

Abstraction lets developers focus on elements essential for the system without necessary implementation detail. 

![](Pasted%20image%2020251110134443.png)


### Security architecture

Different technologies are used at different layers, from accessing a database to browser form validation. Protection at lower layers in the system prevent successful attacks at higher layers. If there is only one security component, this is a single point of failure.

### Other architectures


- Layered
- Client-server
- MVC
	- Client-server: model “server” provides all info to the client “conteoller” and “view”
- Multi-tier client-server
	- Clients hit a webserver, which then goes to an application server/database server depending on the request.
- Service-oriented(microservices/component)
	- Client requests a webserver and the server gateway gets any number of internal service.
	- Easier to split dependencies and improve resilience to failure
- Event-driven
- Monolithic



> Coursework: lower level, at a refactoring level “what are the decisions you made for this” - in terms of implementation decisions. 

![](Pasted%20image%2020251110141158.png)

### Debt

- The Minimum Viable Product (MVP) that stuck
	- just kept adding new functionality versus 
-  The Workaround that Stayed
	- a shortcut that was once useful but is now regrettable.
-  Re-inventing the Wheel
	- implementing the same thing multiple times slightly differently instead of having one clear path.
- Architectural Lock-in
- New Context, Old Architecture











