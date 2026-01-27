Theory module, about automata, no labs, no tutorials for the first week, in Lean.

Tutorials are **EXTREMELY** important. Prepare to be stupid.

## Chomsky Hierarchy

A language is a set of words.

A word is a sequence of symbols.

A symbol is an element of an alphabet.

An alphabet is a finite type with a decidable (function -> bool) equality.

### Level 3: Regular languages
Deterministic finite automata (DFAs) can be viewed as programs that only use a finite amount of memory. Regular programs are those that only use a set amount of memory.

Formalism: can be used to identify regular languages. This is a regular expression (can describe patterns for replacement).

NFAs: recognise the same class of language 

### Level 2: context tree
The core of programming languages. 

Formalism: **context-tree grammars**. Formalisation of a language is usually given as this.



Non-deterministic programming languages are not really used as they are harder

DPDAs: 

PDAs: Push-down automata - another word for a stack (stack automata). 

CDLs: Context-free languages

CDFLs:

### Level 1
Turing machines are finite automata with tape. Can read/write from it. It will only use a finite amount of tape. 

Recursively enumerable languages: a language that can be recognised by a Turing machine. A Turing machine is a precise definition of a program. 

Context-sensitive languages stop because of a context 

Context-free: statement goes to x, variable goes to y. Context-sensitive: only if it meets criteria

Decidable language: always has a stopping condition for all inputs.

Halting problem 














