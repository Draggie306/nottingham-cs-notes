


## Coding Principles and Design Patterns in industry

### DRY - Don’t Repeat Yourself
Particular logic is only used once: each piece should have a single unambiguous and authoritative use in the system.

Issue: sometimes it is necessary to repeat yourself, but this generally minimises coupling.

### CUPID - ”joyful” coding

- Composable - plays well with other systems
	- Easy to use, gets used, and used.
	- Small surface area with a special task - less to learn/go wrong/less conflict.
	- Intention-revealing name and purpose: easy to discover and evaluate
	- Minimal dependencies
> When we write coursework, we should not just say there is no dependency, but also show and explain it.
- Unix philosophy - does one and only thing well. Clean, transparent
	- If a piece of code does not change the current output, then consider if it is needed. Does it do something useful for you/system/product? 
	- Composable: output from the program becomes the input to another: `cat | grep | sed | sort | uniq`
- Predictable - does what you expect
	- Behaves as expected, passing all tests even when there are no tests.
	- Deterministic, so it does the same thing every time.
- Idiomatic - feels natural
	- Uses language idioms, standard features, frameworks, etc.
	- If the task doesn’t need to use super complex and crazy techniques then don’t use it. Don’t add or change the coding or design standards
- Domain-based in language and structure
	- Uses the language of the domain. Some apps are suited to one particular language, tool or use case
	- Codes for the solution and not the framework 


CUPID can be applied to critically evaluate code.
> Coursework: use it


### Keep It Super Simple
Keep it simple, stupid!

- Identify core objectives
- Focus on essentials
- Simplify design and workflow
- Prioritise clarity and understandability 
- Iterate and refine
	- Continuously review and refine solutions to simplify it further.
- More lines of code = more room for errors or mistakes. Take it out if it is not needed.



## Design Patterns

> It is not expected to use every single design pattern.

- Structural
- Behavioural
- Creational

> Coursework: factory patterns can be applied in the coursework. Have an obstacle which defaults to an enemy, but can create another?

### Builder pattern

- Product, builder, concrete builder, director, client

A builder interface is implemented by different types 

> Coursework: observer pattern can be applied to the game.


Strategy pattern: the strategy of doing events is different (e.g. human vs computer player).

> Singleton 






























