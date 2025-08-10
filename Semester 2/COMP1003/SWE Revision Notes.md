> *These are my revision notes for the Software Engineering (COMP1003) 10-credit module at the University of Nottingham, taught by Dr Horia A. Maior.*

Software engineering is the application of a systematic, disciplined, quantifiable approach to the development, operation and maintenance of all aspects of software production.

It is about teams and people coordinating, planning and understanding how to work on one piece of software.

## Core ideas
Software integrates many features - login, databases, APIs - and (crucially) is ready for real users. These are not scripts cobbled together in a CLI.

The correct approach to developing software varies depending on the product's size, scope and requirements. However, when developing ANY software, there are 4 generic processes:
- **spec**ification - defining what the system should and should not do
- **dev**elopment - making the software
- **val**idation - ensuring that the software meets the user's requirements
- **ev**olution - updating the software to meet new requirements

The final software produced includes the compiled code itself, documentation (how to use it), configuration files, and installer/upgrade functionality, deployed by an installer.

### Challenges
Unplanned IT downtime costs $400bn annually, and is only increasing with increased usage, interconnectedness and adoption of technology.

85% of large software projects over $1m fail. Only 16% of software projects in the UK are successfully completed on time and on budget. In fact, over 31% of all software projects are cancelled before they are completed.

**Bugs have real consequences**
- 3,200 prisoners in the US were released up to 600 days early because of a software glitch
- Poor UI caused an "incoming nuclear bomb" message to appear on the public broadcasting system in Hawaii - the UI was the same for testing vs real event.
- Applications that are updated with new functionality but received poorly by users can risk the collapse of the whole company. (Snapchat share price falling after redesign)

**Why the failures?**
- 57% of software projects that fail are because of a breakdown in communication.
- Poor requirements cause 39% to fail, and 29% are caused by poor testing.

The way software should be built is NOT random and there are dedicated procedures and processes that are used to give software the best chance of success.


60% of software engineering should be planning, designing and building the software. The remainder is testing, delivering and operating it. However, maintaining and evolving it often costs much, much more than creating it initially.

## Models

### Waterfall
A fixed model that starts from the top and moves down only when the current stage has been completed.

- Requirements - *defining what the software should/should not do.* 
- Design - *architecting how the system and software operates.*
- Implementation - *making and testing individual parts of code.*
- Integration - *testing that all the code and the system work together.*
- Maintenance - *the operation and any features/fixes after initial creation.*

### V
This is an extension of the waterfall model. There are still the core four: 
- requirements
- specification
- architectural design
- detailed design 
(and then actual coding). After coding completes, it goes back "up" to a corresponding four: 
- unit testing (detailed design)
- integration testing (architectural design)
- system testing (specification) 
- acceptance testing (requirements).


### Agile
Agile is a more flexible and iterative approach to developing software. It solves the problems of needing fixed, perfect requirements before anything else, and revising/refactoring. New deliverable versions are created with each feature, allowing greater communication with the client and other teams.

However, its disadvantages include: lack of central visibility (less "structure" may mean less coordination), lack of planning and more focus on development, extra skills (e.g. for rapid prototyping) may be required, and lack of documentation - often left to the final stages.


# Creating software
Programs often do not have one version and that's it. There are rolling release schedules, new versions being released with new features, and old versions being updated to fix bugs and errors. This is managed through Git.

## Git
A version control program used to keep a history of everything. The server is the authoritative source, users `clone` from it, work on different copies/`branch`es of the code and `revert`/`merge` changes into the source branch.

We work on the `head`, can revert to a commit with its ID, retrieve a file with its changes from a past commit, etc.
Tags give a name to a commit, useful to mark important versions for others.

# Requirements
The biggest problem is not coding, it is the lack of user involvement creating incomplete requirements. The hardest part is deciding, quantifiably and precisely, what (*and what not*) to build. 

Getting the requirements right can save up to 200x less cost than fixing the same issue in the maintenance stage.


## Requirements engineering
Developers need to determine the requirements by working with clients that are not software/requirements engineers. 

The software architect's responsibility is to extract information by asking detailed 
questions/clarifications and translating them into clear definitions and program requirements.

These are the fundamentals of the project that sets out its quality and expectations.

### Stakeholder analysis
All the people that will use the software should be identified. This includes:
- primary stakeholders (directly use it)
- secondary stakeholders (use the system but not build specifically for them)
- tertiary stakeholders (sometimes use it but not directly)

> They can be ordered in terms of priority, how important their needs are, etc.

#### Personas
- Personas represent a realistic category of user, such as a publisher, viewer, lecturer etc.
- A stakeholder type may need multiple personas (high-spending gamers, free-to-play gamers, casual gamers).

Personas are useful to make designers think about how their designs will be used, make developers think about what might not be documented, and allows requirements to be prioritised to meet multiple personas' criteria.

Multiple personas can be put in a table to categorise and compare different user needs and to ensure all types of interaction is covered.

##### Use case diagrams

![[Pasted image 20250521164641.png]]

#### User stories
Common, fast and easy to produce in Agile teams.

> As a \<role>, I want \<a goal/desire> so that \<outcome>.

These low-maintenance sentences can be ranked by importance, put along requirements to ensure everything is met, etc.


## Documenting requirements

Requirements and specifications are distinct but can both be defined in terms of functional and non-functional:

- Requirements are high-level goals of the software, often worked on by end-users, stakeholders and developers
- Specifications are lower-level detailed examples as to how requirements will be met, for developers, testers and engineers

- Functional requirements include **what the system must do** so the user can achieve their requirements
	- The specification would be what the software includes - functions to create an account, display and edit profile information, delete the account, upload files, manage files, delete files..
- Non-functional requirements include **technical constraints** on what the user needs to do 
	- Specification would be how the system performs - uptime targets, maximum concurrent users, maximum file sizes, authentication requirements

Functional requirement: a user will need to check and manage their uploaded files
Functional specifications: a user shall be able to see a list of their files; see whether each file is public or private; be able to change the settings of that file; be able to delete the file.


Additionally, non-functional requirements can be broken down into:
- product NF requirements: performance/efficiency metrics, security 
- organisational NF requirements: must communicate with the university's login service
- external NF requirements: accessibility, ethics,

The key to any good set of requirements is about asking the right questions - the design brief given is exactly that - *brief*, not *comprehensive*. One question is not enough: after getting an answer, it should act as a springboard to ask potentially 5-10 more questions. There are different ways this can be done:

- surveys (**quantitative; articulated**): good for majority consensus, bad for detail. 
	- Can be made poorly by being too lengthy or asking leading questions. Can take lots of time vs just reusing an existing, known one like NASA TLX
- interviews/focus groups (**qualitative; articulated**): allow follow up questions in detail following a "to talk about" list.
	- interviewer should be ready to listen and makes interviewee relaxed - this increases involvement
	- allows user to explain, show, draw things.
	- focus groups cover more user examples, different opinions but longer to discuss and may get a "dominant speaker" - conflict
- observations (**qualitative; observable**) - allows you to see whole picture - what people do, didn't realise that was important.
- technology tours - maps out every interaction with each piece of tech in the user's environment
- ethnography - joining the jobs of people who use the software
	- shadowing a doctor instead of being a software engineer.
	- every time something is used - write what it was, where it was used, how etc.
	- allows edge cases to be spotted.
- usage logs (**quantitative; observed**) - automated way of finding bugs or inconsistencies in deployed software.
	- if bug occurs after back button is clicked, then UI needs changing/code fixing

## Requirements models
These represent how something works. They are selective - only portraying important aspects. They can be used beyond requirements too.

### Context diagrams
High-level displays of interrelated systems (so are often non-functional requirements). Can just be simply labelled "system" with a description for each, or more detail e.g. service request to customer system, statuses from instrumentation system, etc.

This also shows the boundaries of the system, how it related, and what do and do not need to be developed.


### Task analysis
Used for breaking down a process into tasks and subtasks.
- Cannot identify processes with different actors/users
- No decision points
- Useful to break down functionally for each use case.


### UML Diagrams
Easy modelling of object-oriented software. Consists of 13 different diagrams and 5 types:

- Behaviour diagrams include use case, activity and sequence diagrams - useful for anything.
- Structure diagrams include class diagrams and state diagrams - useful for specification and documentation.

#### Activity diagrams
Show the workflow of key activities with decisions. Allows parallel work to occur between activities and systems, shows waiting points, with reasons/comments, typically for one use case. 
Diamonds represent decisions, thick bars represent the splitting and joining of parallel activities.

#### Sequence diagrams
Transforms a use case diagram into one that shows the sharing of information between different people and systems and messages between components (e.g. functions).

![[Pasted image 20250522195721.png]]




#### Class diagrams
Models like an E-R diagram the classes and relationships in OO code.

![[Pasted image 20250522195741.png]]

Can also be used for hierarchical inheritance:

![[Pasted image 20250522195842.png]]


#### State diagrams
These give all possible "states" that something can be in, and what actions can change them, such as button presses, when door open/closed, what is displayed, etc.

### Scenarios
These are written text descriptions that document typical and significant user activities. They include a definition of the context (e.g. technology tour), one of the users (e.g. a persona) and a goal (from a user story). A plot (sequence of events) describes how a user achieves the goal in the context.


# Specifications
Specifications are what the software must do to meet a corresponding requirement, not necessarily how it should do it. 
They are looked at by software developers. User requirements are looked at by the client.

They are typically written as one sentence, linked to one requirement, specifying mandatory "shall" and desirable "should", without any jargon. They should be measurable in some form - a metric, UI element visible, etc.

Structured specifications go further than the natural language specifications - specifying additional information like function logic, conditions, side effects, other function calls.

Graphical specifications can be easier to interpret and read, e.g. a sequence diagram is easier to digest than 30 sentences covering each condition.

> Requirements diagrams are higher-level, explaining and linking what systems relate to each other. Specification diagrams are lower-level, can involve function/parameter names and passing between other functions

After the specification has been created, it is common for it to be reviewed by a team of reviewers for errors/inconsistencies. Checks include insuring that specs are:
- Necessary
- Unique
- Complete
- Clear
- Traceable (all link to a requirement; categorised by importance)
- Testable (it must load fast -> must load within 10 seconds)

## Prototypes
These are an example of high level design: quickly envisioning and showing others how specifications work together and how interpretable they are to check if the design is feasible. They are concrete but partial representations or implementations of systems. 

- Low fidelity prototypes are non-functional ways of showing the intended functions, paper mockups of UI elements, sketches of how a website looks, content wireframes. 
- High fidelity prototypes may use software to create something interactive, able to be tried and used, with detail similar to the final product to finalise ideas.
Both help with client approval and are thrown away.

Generally, prototypes are designed to do one of three things: identify the role of the technology, the look and feel of it, and a guide to implement it.

Prototypes can be a waste of time (especially high-fidelity), it might be used as a replacement for documentation (not good) and could be approved by the wrong stakeholders e.g. managers who think it looks nice vs end users who want a specific feature.


# Design and Test Planning
## Low-level design
This is part of the specification often led by a solution architect. It allows enough detail (i.e. with UML diagrams) to be given to the development team to say "build this exactly" not "[make it up as you go along](https://www.youtube.com/watch?v=3Eyx_DhepDg)" - so it usually the final version given to all teams.

It includes architecture design (API use, objects/classes; MVC), interface design (blueprints of the final UI and other components), database design and component design (the class structure in each).

For OO, we can create class description documents: these guide developers by showing the data format and use cases for each variable, and similar for each function with input/output, and how to know the class works as expected.

This also includes various test plans -- similar to the V model: development test plans (unit tests) to make sure each class function works as expected; system/integration test plans to check that components can interact correctly and meets the specification; acceptance test with the client to show it meets the requirements.


## Test plans
A test plan document has a testing process (description of how the test takes place), spec traceability (talked about earlier), tested items (list of e.g. classes that are to be tested), schedule, recording procedures, hardware/software requirements, test constraints. 

Before coding, we should design and create test cases, running the test until the code we wrote afterwards passes.
*Each test case should have what is being tested, the inputs, expected outputs, and steps needed to carry it out.*

Validation and defect testing should be used to give it all possible types of correct/incorrect data and show that it remains correct and does not break.

# Implementation

When working in a team, 1 solid piece of software should be produced that doesn't look like it was built by 20 different people. Everyone should be collaborating, helping and talking to each other, and will have to prove that it all works together. Other people will look at your code, you will have to fix others' code, documenting code will be with multiple people, other people will judge whether you have finished.

## Clean code
Coding conventions are used to standardise the code -- this includes where brackets should go, comments placed, files named in a way, variables named in a certain way, or even Javadoc syntax used. They improve readability, allowing new engineers to take over, new contributors to understand it. 80+% of the cost of software is in the maintenance phase so even small decisions on variable naming can have significant cost savings.

Linting can be configured to do this, in addition to pointing out basic errors like unused variables/unreachable code.

Code should be clean: no duplications, functions that do one thing but well, be simple and direct, and self-explanatory.

Strategies
- Test-driven development: write the passing/valid tests before the code is written; in a team, write tests for someone else's code. Tests run every time code is changed; open-box.
	- Very beneficial: code made to the bigger picture as it implements specifications and requirements
- Comment-driven development: write the comments to be populated with code first - separating the logic from the code. Comments can be refactored easier than code, they also are enforce documentation so facilitate better design and team collaboration.

## Debugging
Is the process of locating issues and changing the program to fix them. Especially hard if the bug is highly conditional or in large codebases.

New functions or problems with existing functions may be found: there needs to be a way to keep track of things that need fixing. Coders who write some code will often get it back to fix a bug/add a feature.

Bug trackers like Jira or bugzilla can be used for any project, especially if code needs to be finished without fully testing for bug-free behaviour. Generally, bug reports should have a high level description, reproducing steps (minimal reproducible example), expected behaviours, screenshots if it helps, and a test case.

### Debugging methods
If there is an exception, the call stack shows the line number. It is harder if the code works fine but produces the wrong result.

- Breakpoints - pauses execution; see step by step changes to see program flow, inspect variables
- Trace tables - see when variable changes occur and to what value new value
- Print statements - useful for loops and conditionals, sees how far code is executed before an error
- Rubber duck debugging: explain what you think it is doing then read the code. Often will find a mismatch
- Fagan inspections - group code inspection, everyone explains the code to each other.
- Paired programming - a social activity: take it in turns to think and check, while the other codes. Improves problem solving, built-in review process, immediate bug reporting, multiple authorship, knowing code is readable as it is being written, does not take longer when accounting for testing and debugging.

Important to fix bugs: often come back work if think are fixed but not fully understood.

## Tests
Tests should be written every line, condition, function etc. This is called code coverage.

### System/release tests
These are tests of the full system to find errors between components' interactions and to ensure subsystems work together to meet the full specifications AND non-functional requirements.

Compared to integration testing:
- it uses a separate team to test
- the objective is to test if specifications are met for external use
- uses closed-box testing on built executables
- is usually validation testing

Can be hard to automate.

There are 3 major strategies for this: performance-driven, high-level spec-driven and scenario-driven.

This is where performance/stress tests can be made

### Acceptance testing
A formal test with the customer with real data supplied by them, and then payment is made.

The client should be shown all the ways the tests pass, ideally with their real data, in the actual environment of use. Usually there will be some failures of the client identifies an issue, so these are negotiated, resulting in either an accepted or rejected system (if so, more acceptance tests will follow).

### Additional tests
In the maintenance stage, we may have specified "support for X months" - problems may emerge from the working environment with real use with real users. To mitigate these, we can use:

#### Alpha/beta tests
Alpha tests are small-scale but involve real users and real tasks.
Beta tests are where the software is fully released but for a limited number of people, with feedback. Often used as marketing and when cost of fixing problems is low.

## CI and Deployment
Branches are often used to have multiple versions of the software at the same time. There are a range of methods for this:

- no branches - small teams, no need for "isolation"
- for release - new branch for the next release with new features, then after the feature is added, it goes back into the main source tree
- for maintenance - to maintain an old version with maintenance changes - not related to production builds and never merged back.
- for feature - development branch has a new feature which is then merged back into the main after the feature has been completed - also allows parallelism
- for team - sub-groups can work without making breaking changes, working to reach to different milestones

### CI/CD
All code changes get built automatically, producing complete software. When there is a new commit, if the build pipeline is successful, then the submission can be accepted. 

This supports test-driven design (all new submissions must also pass all tests), identifies bugs quickly, and automates integration testing.

Build configurations and scripts are pushed to a build server which then pulls all new commits.

Continuous delivery refers to then having code available in "staging" and then "production" servers - Google tests Chrome changes on a subset of real users before it is applied to all users.

# Evolution/Maintenance
The most important/longest aspect of software development. 

It involves correcting errors that were not found, updating the implementation for newer platforms and enhancing the services with new requirements.

Good, large-scale software may be used for 30 years with changing markets and technology. Customers would rather update their current software than to move/transfer to a new system. Plus, building new software is risky, takes a while and can be more expensive. There are 3 types of change:
- fault repairs - for coding errors (cheap; no redesign)
- environmental adaptation (updates for a new OS; not expensive + little redesign)
- functionality additions (to meet business changes; very expensive + redesign)

Much more money is spent on functionality changes than anything else.

Developers move on to newer projects, juniors given hard tasks, age of the software and poor development practices with limited docs contribute to costly repairs.

When changes need to be made, start by working out how much change is required and how much it will cost. 
Emergency changes such as downtime may require immediate maintenance - deprioritising the updating of specification and documentation so that the code no longer corresponds with the documents.

To mitigate these long-term costs spiralling out of control, refactoring can be used. This is a way to look at code and improve it by removing duplicates or similar lines, breaking down functions into multiple distinct parts and removing code that will not be needed in the future. New features risk adding "spaghetti code" and adding/adjusting all other code in the program, which gets more and more expensive and less "worth it".

With agile workflows, changes during development can occur as the customer is involved throughout the development process, such as seeing prototypes. This way, change becomes part of the development process as a whole.

# Agile vs Traditional
Agile methods like Spiral, Scrum, and iterative models prioritise different skills and are used differently compared to more traditional methods like Waterfall and the V model. For instance, user stories and personas are prioritised over long lists of requirements tables and detailed UML specifications. Prototypes are made rapidly, every cycle of the spiral model can adapt to new requirements, putting the client at the centre. Traditional models focus on dedicated phases for integration and user tests but Agile models prioritise test-driven development with CI/CD pipelines and paired programming.

From the 1990s, there was concern with the traditional models - particularly the waterfall model - as it heavily prioritises top-down approaches with fixed working on each section of development.

Agile really came together in 2001 which combined Scrum, TDD and rapid software development. A collection of people came together to agree that methodologies can be adaptable to the situation to avoid unnecessary bureaucracy. 

Individuals and interactions > processes and tools
Working software > comprehensive documentation
Customer collaboration > contract negotiation
Responding to change > following a plan
## Agile Manifesto

**Individuals and interactions** over processes and tools  
**Working software** over comprehensive documentation  
**Customer collaboration** over contract negotiation  
**Responding to change** over following a plan



## Agile methods

Scrum is about time and delivery.
- 2-4 week sprints, managed by a scrum master, to complete a sprint backlog and make a shippable product
- Daily scrum stand-up meeting
- Product backlog gets cleared as it gets added to sprints and then developed
Kanban is about speed of delivering features
- Kanban board organises work by priority
- Allows new features and changes made at any time
- Anyone can work on anything and no particular role
Extreme programming is about the effectiveness of the team.
- Versions built more than daily, increments delivered every 2 weeks, builds must pass all tests and released immediately.

## Software quality
Quality assurance is about planning for high quality goals and everyone to reach them.

The quality assurance team is the one that:
- plans for quality
	- writing a Project Quality Plan that includes standards and procedures such as requirements docs, specification docs and documentation guidelines
- defines the company's standards and procedures
	- this includes the programming style, document structure of requirements and specifications, the process that new versions/branches are made and how tests are recorded.
	- there are many ISO standards (ISO 9000)
- checks that projects conform to these standards. Typically it is a separate division than the developer team.
	- ensure that the software is measurable
	

Quality inspections can occur  at every stage - inspecting code can fix 60+% of bugs and 90% of defects. Documentation is produced about the review, focusing on finding problems or incompleteness, missing steps and conformity to specs and requirements and the agreed standards. A review leader, recorder, reader and reviewer are present.

There are lots of problems - criticising who built it, performance anxiety, too much focusing on every problem

In agile, there are:
- retrospectives: after each sprint, reflects on progress, thinking about optimisations and good/bad parts of the sprint
- postmortems: after the project has been delivered, look for root causes of difficulties to prepare for the next time.

### Measuring quality
It is difficult to measure code quality. Subjective measures of quality can be inferred from quantified metrics:

- actual lines of code
- Fog index (how readable comments are)
- length of identifiers (longer variables = more descriptive)
- fan-in/fan-out (number of functions that call other; if fan in is high 1 function controls lots of output, if fan out is high then complexity is high)
- depth of nested statements (more nested = more complex = higher bugs)
- number of faults after delivery
- number of days per person of coding.


## Risk management
To reduce risks of software, there are generally 3 categories:
- Hazard **avoidance** - *mitigating vulnerability* - ensuring the risk is as low as possible, none if possible. These are actions taken to reduce the risk happening
- Hazard detection and removal (**minimisation**) - *mitigating the event* - allowing the system to recover/gracefully handle the event - reducing impact of it on people if it happens
- Damage limitation (**contingency**) - *mitigating loss* - sometimes failure is inevitable, but we can reduce its damage scope - what will happen if it happens

What the system should do in the event of a failure, or for any risk, should be documented with a description and the failure type in the non-functional requirements. Commonly, metrics like "six nines availability" should be achieved. "Shall-nots" are also common requirements and specifications.

There is risk to the project as a whole too: a project manager should anticipate possible problems for the project, not just the software, including contingency plans, hardware unavailability, or even external factors like a competitor product being launched.

## Scheduling
All activities in projects must be measurable (produce a requirement/code/database) so progress can be estimated - commonly with milestones in Git.

This can be done with a range of methods like PERT (dependencies), Critical Path Method (risk analysis) and Gantt charts (measuring time per task).

- PERT chart show dependencies and parallel tasks e.g. A -> B means B cannot be done if A is not done. Multiple branches from A to B *AND* C mean that B and C can be worked on concurrently.
- The critical path method is a PERT chart but with the longest path (worst case) identified. This helps analyse cost and budgets - it is the *bottleneck* route which anything added to will slow down the whole project.
- A Gantt chart is a horizontal bar chart with milestones as diamonds, X axis as duration and each activity a separate row. 
- At each milestone, the plan can be updated and reviewed to check for slippage or re-planning
- A staff allocation chart is just a row with each developer on with the task they will be working on for a certain number of weeks

In Agile, reviews and planning is built in to each sprint, such as with burndown charts that track the sprint's targets.

Costs can be estimated e.g. with COCOMO II, for each sprint. The cost of the project can be determined naively by e.g. costing each sprint; buying more sprints = more functionality but higher cost. Generally, pricing is really hard and depends on volatility of the requirements, developer cost, etc. It is up to the project manager to decide the cost: they know the team the best.