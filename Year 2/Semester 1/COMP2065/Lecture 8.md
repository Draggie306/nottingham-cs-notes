
## Equality
All animals are equal but some are more equal than others. Pigs can fly and are more equal.

The tactic `efl` is used to prove equality. 

If we know two things are equal, then they can be rewritten with `rw` . 


### Love
Is love an equivalent relation?
- Most people love themselves, but some don't. It is not equivalent

Is it symmetric?
- No, as A loves B but B might not love A. *Unrequited...*

```haskell
axiom People : Type
axiom Loves : People → People → Prop

def P1 : Prop :=
	∀ x : People, ∃ x : People, Loves x y ∧ x ≠ y
	
-- forall people, there exists a person such that x loves y and x is not y.

```

### Equivalence 2
3 ≤ 4 but 4 ≰ 3

Less than or equal to is not an equivalent relation. 





