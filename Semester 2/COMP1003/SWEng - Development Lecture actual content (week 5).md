

## Developing!!!!!!!

Development concerns are in secrtion 2 and 3 in the main books. This includes more than covered in the module, but very good to look at (e.g. security, reliability, distributed/embedded systems). *This module is only about **teamwork***!


Clean Code book: 
Section 1 has inspirational, relevant info
Section2-7 is about development and coding
![[Pasted image 20250228160535.png]]

When joining a company, we may need to adjust our code style to match their style and implementation.

Debugging is social and multifaceted: it may (***will***) be given to other people and understand to solve their other problems, so it needs to be done collaboratively.

### Social development
We are not working alone - an **incorrect** scenario is myself doing the requirements, specifications, design, maintenance, testing, releasing. 

As a developer, we’ll receive a (hopefully complete) brief with class/state diagram and it should be clear what is needing to be built. Then we write code based on the specs, and everything implemented functions as specified. We then test this code and ensure it works, with the team leader reviewing and submitting the code as part of the bigger project.

We need to prove the code is bug-free. To do this in a team environment

For a manager, we need to have similarly implemented code with similar standards that integrates really well together — not like it was made by 20 different people. They need to think about how unifiable and distributable this code is amongst a system. One good way of doing this is having an environment where it is encouraged to talk, share ideas, helping each other, avoid only 1 person understanding what is going on in a system. The ultimate goal is the last peice of code that integrates everything from all the 20 people works well and runs properly. There are many ways this is done and frameworks that goes along with it too.

The integration team is a special team that brings it all together. 


Writing code is not a one-time task: we need to think of all the implications of this when writiing it. 
- Multiple people need to be able to read and understand the code 
- We may have to fix other people’s code
- Coordination between people is needed
- Documentation is very important to allow others (or yourself later) to better understand
- ”Finished”/correct code is judged by other people.

Coding conventions are designed to make coding easier - to read, understand, add code in a team. It makes software that looks uniform & consistent with one naming/coding style, increasing its quality and maintainability.

As 80% of the cost is in maintenance, code conventions improve readability, 

> **Software engineering is not a solo activity. It is a team activity.**

> **Anyone can write code that computers understand. Good programmers make code that humans can understand.**



Linting tests can check for uniformity and check for basic errors such as unreadable code. 
Most code nowadays also has automatic code checking for basic errors before it goes to a human for further review.

- Model driven development
- Feature driven development
	- Is iterative, delivering more and more features with every iteration
- Test driven development
	- Before writing code, we write the tests it must pass. When all tests pass, the implementation is completed.
	- Very good for estimating how long it will take
	- In teams, others write the test for someone else’s code: increases accountability within a team and **facilitates more people to have a shared understanding of the specifications and codebase**. -> risk-free software engineering.
- Comment driven development
	- We comment what and how it will be implemented in English which is then transferred into the code
	- Enforces documentation and teamwork by design - facilitating better design and decides the structure of the code before actually writing the code, providing the reasonings for each function/spec implemented.
	- Easy to revise/refactor comments before implementing.

When writing code in a team, new functions it needs or problems it has arise - we will get back code when finished. Projects need a mechanism to tell other coders about problems in their code. Bug trackers can keep track as to what needs changing and also serve as traceable documentation of testing.

### Debugging
Debugging is the process of locating problems with code and changing the code to fix the problems.

It is an active, social process. It involves communicating with other people about their code.

### Strategies

**Breakpoints:**
Useful to insert and will pause the software so we can check the values of each variable to ensure that everything is as expected. 
We can also create trace tables to ask the IDE to keep track of certain variables in a table to see how they change (we can do this on pen and paper). 
Exception-based breakpoints can be very useful to tell the program to immediately pause when an exception occurs.

Print statements add line that print out the value of a variable - primitive but helpful. 

There are strategies to help us so this: working out where to put a breakpoint can be hard, so we should be systematic:
- Binary search: start in the middle of the code and work out if problem is before/after.
- Code changes (dangerous!) - comment out sections that are unrelated to the program.

Always fix the bug not the symptom. if A calls B, catching it in B fixes the problem but the bug is probably in A.
> The bugs which seem fixed but you don’t fully understand tend to come back worse.


### Important - Rubber Duck Debugging
![[Pasted image 20250303091915.png]]

Can also print out a section of code to review and give many people a chance to look at it, with the author explaining what and why it is doing what it’s doing.

### Paired Coding
One person thinks/checks while the other person codes - taking turn to write functions and change pairs for different tasks.
- Although it may be more expensive initially to write the program with two people, in the long-term, it produces higher-quality, more maintainable code.



## Testing
Open (white) box testing involves having access to the source code and testing it - know how the source is supposed to work and tests test for this.

Closed (black) box testing is where a tester does not know how the code works - running the compiled version. They just know what it is supposed to output for a given input. **No knowledge or access to the codebase.** This is typically the best for release and user acceptance testing.

Automated tests involve large amounts of scripted/coded tests, can also simulate server loads and long-term uptime and stability. It may run as often as the code is compiled/submitted; can be built into Git.

Manual testing is at a higher-level, runs at planned times like the end of a feature implementation and runs when a code version is “ready” or stable.


Test-driven development is when we use the specifications to write tests for some code/function/class and every time the code runs, it runs the test. As more code is developed, the code passes more and more tests. It makes devs think and plan about how the code will be used before it is written - although typical in unit testing, it allows us to see implications for the bigger picture. It also allows us to check if something has broken if we make a change - or if it still passes all the tests.

### JUnit
Allows us to write tests in separate files for java code rather than writing test cases within code. This means that the software is not full of testing code which makes it cleaner and less confusing.

@Test before a function says that it is a test, and we can then write `assertEquals` with the value to test and expected value as parameters. 


The general approach is:
1. Create an empty class with stub methods
2. Write the tests first calling the stub methods
3. Run the test ensuring the tests fail
4. Write code for the first test that is just enough code to pass it
5. Move on when the tests pass.

Good tests have line coverage - every line of code has been tested. 

