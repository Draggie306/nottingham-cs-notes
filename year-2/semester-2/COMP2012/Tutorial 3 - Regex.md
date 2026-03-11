

To have a regular expression for the word ab, we can build it by taking the regular expression of each character, one by one: ab.

In Lean we do `append (sym a) (sym b)`.

To have either a or be, we use the + symbol:
- `plus (sym a) (sym b)`

To take any string of `a`s and `b`s:
- `star (plus (sym a) (sym b))`

To have `a` followed by either `b` or `c`:
- `append (sym a) (plus (sym b) (sym c))`

For zero or more repetitions of `ab`:
- `star (append (sym a) (sym b))`


### Converting regex to NFAs


To have an NFA:

![Screenshot_2026-02-17-09-28-03-09_92460851df6f172a4592fca41cc2d2e6.jpg](Screenshot_2026-02-17-09-28-03-09_92460851df6f172a4592fca41cc2d2e6.jpg)

`b a*` -> `append (sym b) (star a)`

Defining a plus of two NFAs can be done by having an epsilon transition from the end state of one NFA to the start state of the next NFA.

To get the star of any NFAs, **everything that transitions to an accepting state should also transition to the starting state of the next NFA**. The original accepting state becomes no longer an accepting state. 

%%We take the union of the states first.%%



















