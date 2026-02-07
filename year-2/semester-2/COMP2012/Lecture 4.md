A, B, C are just 3 names (constants) in an alphabet. An alphabet must have a decidable equality (if there is a procedure that can determine, for any two elements, whether they are equal or not, and it always terminates with a definite answer) and be **finite**.

There are two special languages:
- the empty language (for any sigma), which is a predicate that is false. As a finite set, it is `{ }`. 
- epsilon $\epsilon$, the set that just contains the empty word

The language supports some operations: 

- 
- L union the empty set is just L
	- L1 union L2 . L3 is the same as L1 . L3 union L2
- Concatenation
	- If a language is just the empty word, concatenating A with it is just A. 
- Star
	- The operation that makes sequences. Any number of words that make L and concatenate them, makes the star language. 

## Deterministic finite automata

> "Don't switch off, this is easy - Thorsten"

`w ++ a ++ v` where w and v are words over sigma. w can be anything, v can be anything, but there must be an `a`

In the beginning, the machine is in a state 0. It may see an `a`: if so, it goes to `1`. If it gets a `b` or `c`, it stays where it is. 

If `an * bn` where `a` and `m` are natural numbers, where it is defined that $a^3$ is `a a a` 

The type of states is known as q: a type.

In Lean `Fin 2` is `0,1`. It is an alphabet 







