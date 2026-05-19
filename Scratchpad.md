


Level 3: 

- regular languages, including finite (state) automata.
- production rules: a -> a; a -> aB OR a -> Ba (right vs left recursive), a -> empty.
- L = { a^n | n > 0}
-  examples include the language of empty words, any number of as followed by any number of bs.

2: 
- context-free languages; non-deterministic pushdown automata
- formalism: G = (V, E, R, S)
- L = { a ++ n | n >= 1 } , or L = {a^n b^n | n > 0}
- Language example: balanced parentheses


1: 
- context-sensitive languages; linear bounded non-deterministic Turing Machines
- formalism: a -> b where it is satisfied that |a| <= |b|
- L = { a^n b^n c^n | n > 0}
- Language example: anbncn

0:
- recursively enumerable languages; Turing machines
- L = { T | T halts }