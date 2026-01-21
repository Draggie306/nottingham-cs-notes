
Learning objectives:
- Think critically about legacy code in DevOps context
- Assess when code needs refactoring by identifying “code smell”
- Understand the concept of refactoring and refactor small sections for maintainability
- Understand and apply coding principles to legacy and new code: Cupid, DRY, SOLID, KISS
- Understand and apply design patterns to legacy and new code


Refactoring: changing sections of code to make it better

To make the code better quality, we think of:
- modularity: can the code be divided into modular form?
- reusability: can the same (module/function) code be re-used?
	- Login systems will be largely the same
- analysability: can it be analysed easily?
	- Is it easy to read and understand
- changeability: is it easy to change
- modification stability: will it affect other code?
- testability: is it easy to test?
- compliance: does it work in different OS/versions/browsers?
	- Can isolate different environments

Corrective maintenance: fixing bugs and errors in the system.
> The coursework contains some bugs

Adaptive maintenance: changes in the environment - adapting to new versions/changes in the environment

Perfective + preventive maintenance: updated stakeholder requirements - ways to increase quality and prevent future issues
> Coursework contains some new features


## Legacy code

> Coursework: is in Swing, but needs to be updated to JavaFX. It is not intentionally bad. First thing to do: develop tests, so that additions or refactoring doesn’t change anything

Legacy code is traditionally defined as old code, built with outdated (but still used) technology, and is difficult to modify or replace because of the design and tech stack.

The pragmatic definition is simply maybe without tests, where any change is inherently risky, and we cannot be certain that changing has not broken existing functionality.

Generally, they lack tests, are documented poorly, use outdated tech (langs/frameworks now unsupported). The architecture is “big ball of mud”: hard to separate changes from other code in a poor, tight structure. Only one person (perhaps no longer in the company) understands how it works. It is also fragile: one tiny change results in a “snowball” in bugs in unrelated parts.

> Coursework: clean bugs up, make the tests, break it down, then do the additions

Legacy systems contain proprietary configurations and frameworks which could cause issues with automation tests, which might not be compatible with CI/CD in DevOps.

Developing tests of a working system is crucial for coursework - as soon as bugs have been fixed.

> When refactoring coursework: creating fake objects (as the code may interact with a database/API that can’t be tested easily)



## Refactoring

It looks easy but quickly becomes challenging.

> Coursework: evidence for writing tests before making the changes.

“Any fool can write code that a computer can understand. Good programmers can write code that humans can understand” – Martin Fowler

Refactoring is the process of changing software, not to alter the external behaviour but to improve its internal structure incrementally. It minimises the chanve of introducing bugs, improving its design after it has been written.

It does not optimise code to make it run faster, comparing the tradeoff between clarity and performance — it makes code more sensical and robust, allowing it to be modified. SOLID principles are applied.

> Basics AND beyond the slides are required for higher marks. Books recommendations on Moodle

“The majority of the cost of software is incurred after the software has been first deployed. Thinking about my experience of modifying code, I see that I spend much more time reading the existing code than I do writing new code. If I want to make my code cheap, therefore, I should make it easy to read”

### Refactoring roadmap

Quick wins:
- Remove dead code
- Remove duplicates
- Improve identifier names
- Reduce method sizes

Divide and conquer:
- Split code into components
- Improve encapsulation (everything part of a class)
- Reduce coupling 

Inject quality:
- Ensure all components are covered with tests
- Improve internal design of compoenents


**The test scaffold should be made before the code is touched.** This means an existing or new test scaffold will be made. After every change (not after every refactored feature), it should be changed

#### Mock objects
Simulated versions of a genuine object, configured to replicate the real behaviour between APIs, databases, etc. These are simulated versions of a genuine object. This allows it to be replicable, isolated and its interactions be verified.


### Mendi Mustafa Talk


- Bitrise CI/CD
- GitHub AI 
- 30% of code is AI generated, gemini code assist


Incredible developer - wanted to do things his way (incredibly knowledgable) but awful to work with as a team. 

Cross-platform: good for prototyping - unified codebase. However, for specialist features: libraries may not be official, difficult to implement etc.

For some companies: development focus is on stability and new features, with no time for workshops 

Enforced in github: cannot merge into dev branch before being approved by a human.


## Code Smells

Code smells are categories of issues that may lead to deeper problems over time.

Technical debt compounds over time - developers waste time and it compounds without anyone eliminating it. They are not bugs - there is no flaw, no error in execution and do not need immediate fixing for the functionality. They may lead to them due to indication of poor design. 

### Lab 3
3 tasks, VERY LONG. This is designed to replicate the coursework  






