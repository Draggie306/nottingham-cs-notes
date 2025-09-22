Dr Horia A. Maior - Software Engineering - Based in B floor

# Introduction & Meta
Software engineering work includes:
- writing and understanding user needs and user stories to define and gather requirements
- using Git to source control a project for usability and maintainability - allowing others to understand what your code does
- working with automated testing
- creating merge requests for a manager to accept your code
- having code reviewed and learning from review feedback
- working in teams

This module will be about Agile development and what came before it, as it is the most relevant in the real world in terms of internships, the YII and when graduated.

There are expected readings on Moodle.

Support requests will be submitted as issues in Git. For team support, raise a Git issue, not email and not Teams. Complete the Git self merge conflict (Moodle) to get a good experience of this.

By default, the team grade for CW will be given to each person. However this is checked -> involvement in the team is measured.

> Keep up with all required reading and weekly work
> Take part in the lab weekly (and more)
> Do all the expected reading as this will be examined
> Focus on understanding the implications what is being taught

## Aims
- Teach an overview of the whole SWeng process
- Give you initial practical experience at working in different stages of the process
- Prepare for SWeng group project in Y2
There are various connections with other modules and with interviews


### Schedule
Green ones are team activities with teammates rating other teammates, so they are not assessed but are assessed.

Weekly team assessed exercises

![[Pasted image 20250131161302.png]]

## What is software?
Software is such that it is a big process - e.g. a phone game app with global scoreboard, social media platform, Google Chrome, the whole Universal Credit System for the Government.

In Semester 1, we wrote a series of scripts - a component of software. Software is built for real users and people, not the command line.

Software integrates with many features, other services (login), with potentially a server database, and managing updates.

Chrome integrates multiple functions with a distinct version history on every platform,with new features rolling out on all platforms. They all share data



## Software Engineering Crisis
Nato conference 1968: all saying software was bad or worse, individual approaches to software didn’t scale to software, being unreliable, behind schedule and costly.
Software Engineering was coined to understand the making of software. During the 70s and 80s, people developed new processes to better ’engineer’ software - eventually turning into 

> 16.2% of projects are completed on time and on budget. 31.1% are cancelled before they are completed.

**Poor requirements are the leading cause of project failure.**

- In the U.S., 3,200 prisoners were released early because of a bug.
- In Hawaii, bad UI caused a nuclear emergency message to be sent out to everyone.

”Top 10 Software Engineering mistakes” by Paul Dorsey - is recommended reading

How to organise 100 developers/coordinate/build 1 single piece of software? The selection and way teams build software is NOT random, understanding why different processes are used.

## The Process
Software engineering is concerned with all aspects of software production. It is about the principles and methods for specifying, designing, implementing and maintaining large systems.

Software engineers should adopt a systematic and organised approach, using appropriate tools and techniques depending on the problem. 

The right approach depends on what is being done. There are structured stages for large, government projects.

#### Guaranteed exam question
**Specification** - what the system will be/should do and its development constraints
Development - production of the software system
Validation - checking the software is what the customer wants.
Evaluation - changing code in response to demands



The waterfall model was developed in the 70s - so is tried and tested, fundamental in structured management and planning. Cannot go back up the waterfall model.

The V model extends the waterfall model

Both models need stable and perfect requirements but we cannot always anticipate what we will have to do.


### Agile Models
Spiral - continually go through the 4 stages until the program is completed

Disadvantages include there is a lack of process visibility, meaning poor structure and organisation. It also focuses on creating many iterations and not enough planning. Because of this focus too, there is often not too much documentation and if so, be of poor quality.

60% of software engineering is designing and building the software, but 40% is 


## Extra Reading (#1)
Agile development is a set of principles that guide development flexibly and iteratively, emphasising collaboration to rapidly iterate on designs for continuous delivery of value to customers.


## Git
Alpha testing - mostly internal
Beta testing - more reliable, tested by devs, so some public
Release candidate - building towards public release

> **“Early versions are one of the first”

In groups, we will all be adding, pulling, adding, committing and pushing

When git pull/pushing, Git will compare and see if there are any differences between local and server copy. This means there is an official, remote source and a local, working copy. 

- It keeps a history to allow people to roll back to an existing state, making it hard to lose files. 
- It is designed to stop multiple people overwriting changes accidentally - e.g. will say when someone else has changed the same file and asks how to integrate these changes vs. overwriting them.
- It lets us work on different copies, or branches, so we can work independently of the same version.

When accessing a file, we see the current view called the **head** - the most recent version. It stores a copy of all the history and files in a hidden .git folder. It is all in a history tree - so can be searched and new branches added.

`git checkout <hash>` - revert all the files to given view in time

### Tagging
Instead of referring to a commit as a hash we can refer to it with a tag e.g. “v1” by setting it.

### Gitignore
`.gitignore` - tells Git which files and file types to ignore, e.g. private keys, passwords, local data about local repo that should not be synced with the server.

### Milestones
Git also can track milestones of the 


# Requirements

- Why requirements are so important
- What requirements engineering is
- Intro to Requirements Elicitation stage
- Initial methods for identifying requirement areas

### Why requirements are so important
40% of projects fail as a result of poor requirements - incomplete requirements with a lack of user involvement are at the top of causes of project failure. The biggest problem is understanding the requirements of the project.

To understand what to code, we need to understand what humans want to have built.
The hardest part of building software is deciding precisely what to build.

Fixing a problem in the requirements stage can give a £20-200 reduction versus in the maintenance stage.

> The critical thing is to spend time figuring the software out properly - right at the start

In order to build software, it’s not about being able to make good code, but that it does what it needs to do and it solves problems. Stakeholders could be customers, users, people funding the project. 

We need to be able to determine the requirements by working with clients: users are not software engineers or requirement engineers, describing how things work and what they want according to them. It is our job to decode and clarify/elaborate on points so that we know exactly what we want - translating vague statements into a series of clear definitions and requirements that the program needs.

Requirements are the foundation of the project. They define the level of quality needed, decision making, the basis for tracking progress. Things unspoken during this stage are the things that will be problems later in the development cycle.

For example, a brief of a few pages by the government that companies bidded on did not include 


### Requirements engineering & elicitation
Requirements engineering has developed as much as software engineering itself over the course of software development.

Requirements elicitation

The first stage is determining all the people that will use the system and who the users are. This can be classed from a mixture of focus groups, interviews, observations etc.
- Primary stakeholders - directly affected e.g. students, staff
- Secondary stakeholders - use the system but not for them e.g. 
- Tertiary stakeholders - sometimes interact/are affected by it but not directly, e.g. some staff

Personas represent a real type of user from our stakeholders - a realistic but fictional representation. We can easily describe/invent a typical stakeholder in each category. *Once identified the stakeholders, we should create personas for each category.* We can put multiple personas in a table which allows us to spotand compare differnet user need. We can also use pen/paper/whiteboard; the process of designing it is not important, just how they are handled and used.

### Use case diagrams
We need to elaborate on the tasks that each stakeholder will do - th emost comonnom method for this is a “use case” diagram - a simple, visual way to see the key tasks that identified users will perform. People are called “actors”. For instance, a medical receptionist will need to regiter/unregister patient, view personal info, records, etc. 

We can have multiple stakeholders acting in boxes, linked to other actors. There is no official “rule” of how to do this. *This shows that some use cases are interconnected, giving us a better  view of the overall system needed.*

## Requirements gathering (lecture 4)

#### User stories
User stories are not the same as use case diagrams. They are a popular way of gathering requirements so that people easily use and understand them. 

A user story connects who is doing a task with what they need to do and, importantly, *why* it matters they do it. It’s very popular in Agile models

**It is a single sentence to represent a single requirement.** 

> As a \<role>, I want \<goal/desire> so that \<outcome>.
- “as a user, I want to be able to see all the details I have stored about me in my account”
- “ as a user, I want to get a notification 20 minutes before the delivery driver arrives so that I can prepare and be there to get it”

They are consice, clear and require little maintenance. They cn be transformed into a clear checklist and broken down into chunks that can be visualised more easily - and the work in a small team can be divided amongst the team. We can also rank them for importance and e.g. if we want to have some implemented first, we can swap some to be at the top of the “to-do list”.

However, it’s difficult to use in very big projects and doing this can lose detail and formality. It also does not discuss the context of the projects or tasks to be done.

### Requirements vs specifications
Requirements define, at a broad and high level, what the system must do, with user needs and capabilities defined. It is written for stakeholders.

Specifications define how the system will meet the requirements - they act as a blueprint for their implementation. They are detailed and precise, designed for developers, testers and software engineers.


### Functional vs non-functional requirements
**Functional requirements define what the system must do** (tasks, features etc. from a user perspective) - we may visualise this on a use case diagram. They include the functions the user needs to achieve and functions the software will include (such as allowing login, account creation)

**Non-functional requirements describe technical capabilities and constraints** and not come from users - e.g. 100k should be able to login at the same time, videos should autopay, all major file types should be supported. Security/scalability are frequently used examples.

### Elicited requirements to formal requirements
Now that we have some initial requirements, how can we formally write this up in a document and create system models?

The key to every good requirements set is to ask the right questions during the investigation phase. E.g. we want to login, but how does it behave if the wrong password is entered? When we have misleading/unsure/missing information will need to be clarified.

For every question. 
- We can ask further 5-10 questions to the users for each requirement.

Surveys are an opportunity to gather many data points about a question - e.g. for global/majority perspective on a system or topic, a survey is a great way of doing it. Quantitative data, visualisations etc. can be performed, it is **good to get the majority view**, but not very good to understand the reasons **why**, and the voice of **minorities and potential edge cases may get lost**. 

For real details and the freedom to ask follow-up questions, we can create a focus group and interview, that frees responses from the shackles of a mere survey.

> Crap in, crap out - when designing requirements & specifications, need to be careful when designing them. When making a game, use already-existing questions, not make our own if there is a proven, already-existing thing out there.

Observations and logging can be used. Observations fill gaps that are not visible and allows us to see the things people didn’t say. 

**Technology tours** - map every interaction with every piece of tech in the room (or virtual area). 

Ethnography is joining the jobs for which people use the software - e.g. shadowing a doctor or medical crew instead of being a software engineer. Every time used a tablet - write down what they used, where they used it. This is great to find the edge cases that we may not even think about. 

Usage logs can also be used. This is an automated way of finding bugs or inconveniences and we can observe certain behaviours - for example, if many users press the back button after clicking a previous one, this may indicate a mistake or error in UI which could be improved.

**The key here is having a plan about how we validate requirements before validating them. 

### Requirements models
are a representation of how something works. They are selective representation to portray an important aspect — we should specify why we picked that diagram and what that allows us to see, as opposed to another section/model.

Requirements models are not just for requirements — they can also be used to specify things.

These models are very good to visualise them in an easy way to interpret, allowing us to take them to stakeholders and get even more feedback.



**In summary, these models are designed to:**
1) describe the requirements for a system
2) during the design process, to describe the system to engineers implementing the system
3) after implementation to document they system’s structure and operation

#### Context Diagrams
When gathering requirements, we may identify many other systems interconnect and interact with ours. These diagrams show (at a very high level) the input and output of these. The system that is being built is at the centre of the diagram.

Additionally, they define the boundaries of the system and what should not be developed, to focus development and not waste resources.

They are part of the nonfunctional requirements - being simple or detailed, or showing parts of a multi-part system.

![[Pasted image 20250210092531.png]]


#### Hierarchical task analysis
This is great for identifying subtasks (recursively). The overall task can have many subtasks and then 


### UML Diagrams
**This is very important in the degree and in industry.** Unified Modeling Language is based on 3 popular approaches to creating models that got ”unified” in 1990.

#### Behaviour diagrams (for requirements, specifications and documentation)
- Use case diagrams
- Activity diagrams
	- Rounded rectangles represent actions, diamonds represent decisions.
	- Bars represent the start or end of concurrent activites
	- Circles denote the start and end of the program
- Sequence diagrams
	- Complex 

#### Structure diagrams of code (more for specifications and documentation)
- Class diagrams
	- Specifies the classes in OO code that actis like an entity relaitonship diagram
	- A class hierarchy diagram shows how inheritance work - as we go down each layer, there will be more specific code/attributes for that specific 
- State diagrams


Producing basic diagrams is 40% of the way there. Producing good diagrams is 70% of the way there.


### Requirements validation

If we know what we are documenting and why, then this is good.

There is an IEEE standard 860-1998 that outlines the recommended practice and specification for software requirements (SRS).

It states the purpose of the software, the scope (things that will be defined AND things that will not be), constraints (legal, performance), amongst other things. Key points, inputs/outputs, functions that users must do, etc., are all included. It is very important to keep - it will not be destroyed at the end, it will be retained during maintenance stage to look back and understand what was going on, and can be used as a framework to build on it, and more. It is important to have unique identifiers, a structure, and more so that multiple teams can use it and collaborate.

Organisations are likely have their own templates for such a document.

Translation from anecdotal user wishes, needs and issues into a formal document is difficult, so this framework is a good idea. 
Requirements should be **uniquely identifiable**, **cross-referenced** to previous related documents, and **formatted** in a way that readability is maximised. Such a document is usually a big set of (nested) lists with diagrams accompanying them, with the lists categorised into importance/risk/etc.
At the end, this document is useful to tick boxes for each list with “acceptance testing - the ideal scenario to show to the people who a team is working is that it works as intended.

For the next stages of development and how the software evolves, this document becomes the foundation.

A table can simply be made:
![[Pasted image 20250214162250.png]]
> note: don’t just stop at “importance” - can do risk too e.g. is there going to be a legal issue with adding a feature.

These documents are looked at by customers, managers, developers (so diagrams could be used to explain how things link and the operations between them), testers, maintainers. Therefore, d**o not make any assumptions** as to who will read it and **tailor the document to what groups of users will be using it**. Customers especially need a simple overview.

> If you and the client are not on the same page during requirements, how will you be during the acceptance testing stage? Ensure that everything the client wants is in that document.

The process of checking that requirements actually define the system that the customer actually wants

#### The cycle
1. Requirements discovery
2. Requirements classification and organisation
3. Requirements prioritisation and negotiation
4. Requirements specification

As we progress, assumptions will reduce, name things that haven’t been named. The ultimate goal in the requirements validation cycle is to save as much time, money (and sanity) as possible.

This is also known as the spiral model — it takes a while and comes very late to see coding and implementing things in it.


### Validation
At some point, the decision as to what exactly needs to be built needs to be taken. If this is for a customer, we especially need to have everyone agreeing to exactly - e.g. the customer may say “after you have built these exact 10 things, then I will pay“. 


**Internal**
The requirements will be presented to the boss and colleagues, financial projections, developers. Getting the right people in the room to explain things…. [todo]

useful as there is a shared understanding and better able to e.g. ask developer how long X will take. 


**External**
This is with a client - essentially a review of requirements. 


Conflicts may happen - e.g. 2 requirements saying contradicting things. This will require involvement with the client, giving them (cost) options in the external validation stage.

> All questions and steps involved in the negotiation phase will too need to be documented.

### Identifying objects from a system description
When we have a system description, we can work out many of the objects with each noun in the description.

### Exam Questions
- Using no more than 4 bullet points, explain the difference between requirements and specifications
- Knowing why UML diagrams are useful and what for.
	- Identify 1 type of UML diagram in the module and explain how it can be used differently for requirements and specifications.
- Explain personas
- How scenarios are useful beyond the requirements stage
	- think about req, spec, other stages are used further down the line
	- e.g. new feature 5 years later, a scenario is useful to understand why it is implemented the way it was originally


## Lab 2 Feedback
![[Pasted image 20250217091812.png]]

- See evidence that git pushed, involved in discussions, raised issues, commented, etc.

Create requirements, document assumptions well so that we can go back and ask the client for clarification.

What makes a good set of user stories: **one for every combination of actors and use cases** - e.g. if there are 3 types of users, then at least one use case for each of these. If multiple use cases & actors, ‘just’ 6 stories may not be enough.

We can use labels to define user stories as a requirement, and make a diagram with a link to connect these together. **This allows integration across diagrams.**




## Extra Reading (#2)

> "AI can’t create software, only code"
# Specifications
The main stages are specification, development, then verification (and evolution, going back to specification).
### What are specifications?
Define what the system should do (functionalities, limitations) from a user perspective.
“as a user I want to be able to see my results and feedback”. 

Specifications are detailed descriptions of the software systems functions, services and operational constraints. They define exactly and precisely WHAT is to be implemented - not HOW this will happen - to meet user requirements.

**In short, it translates what the software must actually do to meet the requirements.**

> There is no technical thinking like how to design the system.

For one requirement, there can be many specifications - thinking about different scenarios, edge cases to meet the requirement.

Specifications involve developers, engineers, architects and **no users** who look at them, therefore, the language used when writing them is much different. 

The typical format is a table (tabular data), with unique identifiers for each specification (e.g. building prototype to meet specification id 72) that includes what it is for (a description).

Natural language can be inuitive and universal, so is good to have many stakeholders understanding it - but can be vague and ambiguous.

Structured specificiations are a template that forces us to think about everything the company deems important. They can be used to specify additional information, e.g. code logic, I/O, how functions may work, rationale and explanation behind that specification, conditions, and relations to/side effects on other functions.

### How specifications differ from requirements
Requirements: high level as to what people do.
Specifications: how the system functions 

### What makes a good specification?
Specifications should be:
- complete
- correct - need to build the right things 
- necessary - must be needed
- unique - define one thing
- concise and clean

All specifications must be traced to the user requirements. For each specification, the corresponding user requirement should also be stated. 

#### Testability
It is important to verify that it was built correctly - so we need to know that the specification has been clearly achieved, for example “app should load quickly” should become “app should load within 10 seconds”.

In summary, specifications:
- define everything that meeds to be built - ensuring nothing is being missed
- are good for a checklist of things to achieve
- are hard to understand the overall idea/the holistic view
- are often full of conflicting specifications
- are bad for conveying the overall idea *(having 3/4 pages of specs is difficult to understand)*

### Who refers to specifications?
#### Reviews
Everyone on the internal team should have had a look, ensuring all the specifications are correct, necessary and important, then it can be given to external teams.

## Prototyping
**A prototype is a concrete but partial representation or implementation of a system.** They are a type of high-level design that help us develop specifications and early versions of the specs and system functionality.

Prototyping is where a version of the system or part of the system developed quickly to check the customer’s requirements and the feasibility of some design decision.

> We may have choices, showing what we do/don’t want. We can break coding conventions as the prototypes will be thrown away afterwards.


Prototypes are:
- a way of envisioning how specifications work and fit together *(as opposed to pages of tables of specs)*
- a way of testing the consistency of specifications
- useful to represent/visualise a subsystem of the overall design



### Types of prototypes
There are different types of prototypes - categorised broadly into **low-fidelity & high-fidelity**
- low fidelity: pen and paper, cheap to 
- high: mockups, developed subsystems/particular functionalities

#### Low fidelity
Non-functional, high-level or general model that is linked but nothing close to the functional product - just useful to show what it may look like and work, how the customers may feel about it.

In software, this involves pen and paper sketching to create different parts of the system - still, we get a good overview as to what the product will do. It focuses on the underlying ideas and key functionality, creating many possible ideas and helps communicate and get confirmation from the client. It minimises committment to any design as it is very early on.

For web design, we can use wireframing:
![[Pasted image 20250221163714.png]]

#### High fidelity
A functional, working thing with high functionality that people can try and use it but not the final product.

It can take hours or days to implement, but provide a very close view, look & feel to the final product, allowing us to fine-tune a strong design and finalise these ideas, helping the client confirm that the design is what exactly is wanted.

