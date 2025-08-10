Tradeoffs - amount of stuff decide to display is important
Some used other tools outside of Visual Paradigm

**It is important to:**
- Have links to reasoning included in the markdown file
- Have links to previous requirements



## Object Oriented Design and Test Planning
In the V model, we are almost in the development/coding phase but we are not quite there yet.

Briefly:
> Low-level designs are there to guide developers
> These diagrams, documents etc. are the final outputs of the Spec phase - are handed to devs
> Planning testing is a part of the specification phase

Component specification is produced in this phase.

For implementing Low Level Design , we need to have enough detail to give to the development team to say to them, “here, build this” — *not “design this software as you go”*.

This design stage is often led by a Solution Architect - UML is key, as a visual documentation of how the system will interact. THere may also need to be database design. 

All of these together will be used for future reference from developers, testers, and other external stakeholders like management.

Architecture design
- Internal structure of the system, bits of code that need implementing (objects/classes/APIs)
- Like MVC architecture
- Shows how system components are designed internally at a high level.

Interface design
- Detailed blueprints of the user interface - not just ideas, but input validation too
- Also how other programs will have to interface with other programs - e.g. API to access server.
- …

Database design
- developers will assume they can request from the database in their code, as specified.
- Other types of database can be specified.


![[Pasted image 20250224092452.png]]

Class description documents add detail to classes, guiding developers and acts as a “v1” of documentation.
For each variable, the data format is specified.


Accepting, release and development testing - are all different types. 
> Be sure to know which testing category each tests in.
### Test plans
Test plans determine when the software that has been built is “done”.

**Test plans** define what counts as finished, and how each stage back up the other side of the V model is tested — when, where, by who, etc.
- Developers use these to test code before delivering it, ensuring each individual module functions as expected.
- Managers use these to estimate how long it will take, with what workload, and schedule it according yo budget.
- Clients also use this as evidence of proper software engineering and that everything has been tested to expectations

#### Development testing
Verifies each class/module functions correctly independently.
Defines who will do it, with what data (invalid/valid/borderline), on which platform (mobile, tablet, desktop)


#### System/integration test plans
Proves that the software meets the specifications.
It tests interactions bettween different components, ensuring data flows between different modules correctly and interfaces correctly

#### Acceptance tests
Ensures the software meets the user requirements, that the software actually meets the requirements.


The overall document has a testing process - a description of the approach take

**Each test case needs:**
- a statement of what is being tested
- specifications of the inputs to the test
- what the specified output from the system is (e.g. if date picker, should the program either crash or handle a string integer of an integer)
- specify the steps needed to carry out the test - NOT JUST “run with the test data” but also it may require other functions to be called first.


#### Types of testing
- **Validation testing** are tests to show that the software produces the correct answer when all types of correct data are given as input.
- **Defect testing** are tests that show that the system does not break unexpectedly when given incorrect data.
> Writing tests for validation testing only is a common mistake.
