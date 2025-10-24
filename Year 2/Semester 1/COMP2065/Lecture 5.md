**Intuitionalistic logic is logic of evidence.**

Trying to prove `¬ (P ∧ Q) → (¬ P) ∨ (¬ Q)`
P = I like dogs
Q = I like dogs

If I don't have dogs and cats,
then I don't have dogs or I don't have cats

**Classical logic: logic of truth.**

```haskell
open Classical

#check em -- every proposition is either True or False
-- exclude the middle

-- if you negate a conj, the conj flips and becomes disj

theorem dm2 : ¬ (P ∧ Q) ↔ (¬ P) ∨ (¬ Q) := by

  constructor
  . intro npq
  -- Classical unlocks the power of truth tables
    have pnp : P ∨ ¬ P := by 
    -- Have means to add something to the assumption 
    
      apply em
    cases pnp with
    | inl p => -- no cats
      right
      intro p
      apply npq
      constructor
      . assumption
      . assumption
```


```haskell
/-

Alternative to em:
- proof by contradiction: assume not P and show it's false:

¬ P → False → P
¬ ¬ P → P

"Reductio ad absurdum"

-/

theorem byContradiction : ¬ ¬ P → P := by
  intro nnp -- want to prove not not P
  have pnp : P ∨ ¬ P := by
    apply em
  cases pnp with
    | inl p =>
      assumption -- easy to prove as it is an assumption
    | inr np =>
      -- from false everything follows.
      have pcf : False := by -- pigs can fly.
        apply nnp
        assumption

      cases pcf

-- for any proof of false

#check Classical.byContradiction

-- em → byContradiction
-- byContradiction → em
-- ?!?!

--  ¬ ¬( P ∨ ¬ P )
-- should be called principle of omissions: exclude the middle

theorem nnem : ¬ ¬ ( P ∨ ¬ P ) := by
  intro npnp
  apply npnp  -- the only conveyor of falsehood

  right -- if left =, we will be stuck
  intro p
  apply npnp

  left -- now, we know P
  assumption

theorem em : P ∨ ¬ P := by
  apply Classical.byContradiction
  apply nnem


-- L∃∀N

/-

False = Gold

P = philosopher's stone

King asks for P or ¬ P
"either give me the philosopher's stone OR give a way to turn the philosopher's stone into gold"

The magician has the ability to time travel
-/



/-
Logic poker:

P:
provable intuitionalistically - then prove it
provable clasically
unprovable


-- 2 points: right answer
-- 1 point: if you prove clasically but it can be done intuitionalistically

Have to explore all possible proofs:
- implication `intro` - then think about possibilities
- "sometimes you just have to guess" - "poker" element


Why do we want to avoid classical logic (em, byContradiction):

1. philosophical
Mathematics is a construct. Hence, it is not a statement about the real world; it's a story.
Therefore it is not known if it is true or false.
Rejection of Plato's cave story

2. pragmatic
Avoiding em means we stay constructive. If there exists a number, then we need to know the number.
"Are there 2 rational numbers x y, such that x^y is rational"

"can prove something exists but cannot show what i is"

-/
```








