
## Tutorial 1: 

To prove a formula in MCS1:
- write all assumptions at the top
- write goal at the bottom
- use tactics/rules to combine assumptions until they reached the goal, "proving" it

Lean is slightly different; in IFR:
- start with the goal: an object in Lean.
- use tactics to break down the goal, which, in process, gives assumptions to work with
- finally, all subgoals will be one of the assumptions

3 logical connectives: conj, disj, implication.

- To prove a conjunction: we must prove both left and right. In Lean, we construct a conjunction object. This is `constructor` in Lean: splits it into 2 subgoals.
- To prove a disjunction: just prove one side. In Lean: we choose which one - `left` or `right`. 
- To say A implies B, we can write down `intro` with a name with the assumption, e.g. variable name `a` (or anything) becomes the left side to prove the other side.

For a conjunction, we use **constructor** and **cases**.
```
constructor

cases assump with
| intro p q => assumption
```
This gets 2 new assumptions

For a disjunction, we can also use proof by cases: the case of the left and the right. There are two ways to prove it.
```
cases assump with
| inl lhs => -- FOr the left hand side
| inr rhs  => -- FOr the right hand side
```

For an assumption:

- we call `apply` with the assumption to get the new proof goal.
- we then `assumption` or `apply`



### `example : P → P → P := by`

Intro means assuming the **left**. This is the top of the evaluative tree. (To determine the top of the tree, just write `intro`)

It is equivalent to `P → (P → P)`. To start, we need the first logical conjunction, `→`


```
/-

	→          (P → P → ...)
   /  \
  P    →
	  / \
	 P   P    (Must be evaluated first)

-/	
```


Answer:
```
example : P → (P → P) := by

	intro p
	intro p2
	apply p
```

We can use `exact p`, `apply p` or `assumption`. Generally `exact` is faster 

### example : `P → Q → Q ∧ P := by`

Conjunction binds stronger than implication

```
/-

	→          (P → P → ...)
   /  \
  P    Q
	  / \
	 P   P    (Must be evaluated first)

-/	
```