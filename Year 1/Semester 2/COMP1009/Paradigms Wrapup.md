Simple programs are often 1-2 lines but can do lots.

> Once type correct, it works first time. This is even true for professional developers in industry.


Functional programming focuses on **what we want to compute, rather than how**.

filtering even, map square over even, sum all remaining
> `sum . map (^2) . filter even`

Pure and impure code can be separated with:
`Int -> Bool` vs `Int -> IO Bool`
A pure maths function vs maths function *but also interact with something outside*.

Functions are first-classed citizens. 
`map :: (a -> b) -> [a] -> [b]`


Equational reasoning about programs:
`map f . map g` = `map (f . g)`
(f compose g)


### Drawbacks: 
- Can be difficult to reason about the efficiency of programs; it can be clear to see mathematically but not what they do in terms of how they interact. 
	- In C, it is clear how it interacts with memory, but not what it mathematically means.
- Limited tool support for developers
	- Java programs may be developed by large programs with testing
- Requires ability to think abstractly
	- Only once thought about it, then we type


# Java

![[Pasted image 20250326102225.png]]


If object that is contained is removed when container is removed, it is composition. If it does have another object reference, then it is aggregation.

Generics (parametric polymorphism): built on inheritance. Class parameterised on another class

Design patterns are the key for modern OO programming. “we need a generic solution for this” - 6 covered in the module, very common globally.

Key features and concepts to know
![[Pasted image 20250326102800.png]]
Also: explain design pattern (from diagram X)


Java simplifies and removes many things compared to other OO languages like C++ especially memory management. GC is a good thing - no need to worry about memory leaks, accessing memory after freeing, as this is built-in.
> *Smart pointers are used in C++ that can do this automatically - objects that act as pointers*.

The benefits of OO are only really seen in larger programs - and reuse things instead of building them from scratch. We can make a powerful program quickly with reliability with Java or OO langs. There is a lot we can do with classes that already exist.

In FP, we tend to use recursion vs iteration as data is usually immutable.
In Java, we do not want to do this since each recurse creates a new stack frame.

### Comparison
FP - deliberately limits you by removing functionality that would break a mathematically provable function. This means the runtime and compiler can assume and do lots more, such as managing evaluation order (thinking declaratively, lazy evaluation, handling deep recursion without stack overflow)


OOP - make the data private but the tool that can change it public. Code can also be reused (but modified)

## Exam Info
First question: Haskell - essay question. To spend an hour on.

Second question: Java:
- lots of multiple choice question. 
- Fill in gaps
- Explain this concept
- Write code



Make sure it ticks all boxes, use testyour

- Bored and want extra? 2 extra lab exercises (concurrency)
- Have a good break, don’t work too hard

