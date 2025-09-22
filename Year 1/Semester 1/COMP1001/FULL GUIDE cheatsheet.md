

## Sets
A set is an unsorted/unordered collections of items, with no quantities. Don’t care about the quantities - only concept is what is/is not in a set. The item can be anything.

> An item is a member, or is not a member, of a set, independent of how many times it is. 

Can list (enumerate) items, and determine if it is or is not in the set (True/False).

There is NO ORDER or any other concepts. 

If a series has an order, or has quantity (multiple - i.e. shop inventory) then it is NOT a set.

### Standard set notation
Standard set notation, called set-builder notation, is used in many programming algorithms and maths to identify what is listed inside the set:

It is denoted with its contents inside curly brackets {} 
- { 1, 3, 5, 7 }

As quantity does not matter, maths says the following are equivalent:
- { 1, 1, 1, 1, 1, 1, 7, 5, 3 }

To determine if the element to the left of the operator is in the set to the right, we use the set membership operator.



## Set theory

Sets are denoted by `{}`, with numbers inside e.g. `{a, b, c}`. Also can be `{ {a}, {b, c} }`.

The set of all real numbers is R.


### Subsets ⊆
A ⊂ B: *strictly* all elements in A are also in B; not all elements of B are in A
A ⊆ B: all elements of A are also in B.

A ∈ {b, c} means "is A a member of set containing b and c?" *False*.


**For example:**
If the set A = `{ a }`
and B = `{ 1, 2, { a } }`
The set `{a}` is in B
The set `{a}` is NOT a subset of B
`a` is not in `B`
A is also NOT a subset 

### Union ⋃
A ⋃ B is the **set of all elements** in A, B, or them both.

### Intersection ⋂
A ⋂ B is the set of all elements **in only both** A and B.

### Not-in
Represented by a `\`, this is the set that contains **all elements in A, remove those in B** if A `\` B.
This is also known as **set minus**.

### Empty-Sets 
The empty set is **not a member** (∈) of every other set, but is a *subset* (⊆/⊂) of the set. It's a `∅`

### Partitions 
A partition is a set of sets where each element of the original set is in only one of the new sets.

A larger set `{a, b, c, d, e}` can be partitioned any way so that its subsets contain the superset's values e.g. `{ {a, b, c}, {d, e} }`



### Power Sets
Power set: `|p(A)|`. The formula is 2$|A|^$ (to the power of)

The powerset of `A`, `P(A)` (or 2^A^), is the set consisting of the subsets of A. 
- e.g. `P({a, b}) = {∅, {a}, {b}, {a, b}}`.



## Venn and Euler Diagrams

### Venn
Overlapping (circles) with each other set that show set memberships depending on their relevant area/category.

Each possible overlap must be shown - cna get tricky with over 3 

### Euler
The same as Venn diagrams, but one that does not require that every overlap be shown. 

More easy to show set relationship. “There is no element in A that is in C, but there can be one in B”. It can also show that “Every element in B must be in A, but every element in A may not necessarily be in B”.

When in an exam, show the Euler diagram clearly by demonstrating that it does not overlap/empty overlaps can be removed.

- ℕ is the Set of natural numbers (1, 2, 3, 4, 5, 6…)
- ∈ means ”is in”

## Set membership and subsets
Subsets are sets that completely belong to another set


A strict subset is a set that must have at least one element in the original (e.g. A) that is not in the subset (e.g. B). A is strictly contained in B, but it cannot be equal. This is ⊂.

⊆ represents a subset; A can be equal or a strict subset of b.

## Intersection and union

The intersection is the set of elements that is of the place where the two overlap. This is the things in one AND the things in the other one.

The union is the set of elements in *either* two+ sets.

Others
The state of being implied with implication is equivalent to subsets. If A implies B, everything in B is a subset of A.

“not” in set theory requires a concept of relativity. Instead of enumerating everything that exists that is not in the set, we use **relative difference** (/set difference/set minus)

> A \\ B refers to the set of elements in A that are not in B

> “U” refers to “universe”, i.e. every number in the set. U \\ A means every number in the whole set that is not in subset A.


# Predicate Logic

**Proposition**: a statement that can be determined to be either True/False based only on things explicitly given in the statement.

**Predicate**: a proposition that has a parameter, something that depends on something else, in the proposition. *Usually a free variable*


### Implication (⇒)

A *implies* B is always True *unless* True implies False.
- A => B
- False implies anything will always be True.

A ⇒ B is equivalent to ¬A ∨ B.

¬P => R   *is equivalent to*   ¬(¬P) ∨ R
### If and only if (⇔)
Similar to equivalent.

Let P be False and let Q be True;
P ⇔ Q evaluates to False.
If we let P be True, do both P and Q have the same truth values?

P = T; Q = T.
Thus, P ⇔ T = True.

Let P = F and Q = F:
P ⇔ T = True (again).

### Tautology
A statement or mathematical expression that always evaluates to False. An example is `A ∨ ¬A`.
### Contradiction
A statement or mathematical expression that always evaluates to False. This could be `A ∧ ¬A`.

### Entailment
Whenever A is True, B must also be True

## Modus Ponens
Knowing P is True, knowing P implies R, this entails R (is True).

## Quantifiers

∀ = "forall". **Universal** Quantification: true for all.  
- Counterexample: a value when P(x) is False / any value for x that is False.
- The statement holds logically true for every possible value in the set.

∃ = "there exists". **Exist**ential Quantification: there exists one (EXISTential), at least one, element that is True.
- This is known as a **witness**.
- The statement holds logically true for at least one value in the set. 

> Universal quantification and existential quantification are opposites, in terms of de Morgan’s.

∀will always be True regardless of what the predicate is if it is applied to the empty set. ∀ s ∈ empty set (P (s) )

This is called a **Vacuous truth**: a statement which is true because you are working over the empty set, automatically true because there are no elements. 

When dealing with predicates, if we look for an element in X where X is an empty set, it must be True, as we cannot prove there is a counterexample, meaning it is True.
# Proofs

We write all premises down that are to the left of the operator on the top of the page, and the one to the right at the bottom of the page.

A *flag* is like a temporary premise 


# Axioms



## AA5 - mathematical induction for predicates

> **φ(0) ∧ ∀k(φ(k) ⇒ φ(k+1)) ⇒ ∀n(φ(n))**

This means:
- If something is true for the first natural number (0) and true for k+1 whenever it's true for k, then it must be true for all natural numbers.
This is used to prove a statement is true for all natural numbers N.



