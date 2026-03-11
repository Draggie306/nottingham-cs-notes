q
Classical logic is:
- when it can be proved (in addition to all principals and tactics)
- with the law of the excluded middle:
- ∀ proposition P,

A proposition is definitely classical is definitely classical if it uses one of the principles:
- the law of the excluded middle

How to prove that something is not provable?



```haskell
/-
Introduction to Formal Reasoning (Comp 2065)
Tutorial 02: Propositional logic-part2
Date: 16 Oct 2025
TA: Aref Mohammadzadeh
You can download tutorial files from moodle `Tutorials -> Aref`.
-/

-------------------------------------------------
--section1:

/-
This week we have four goals:

1. Understand what it means when we say a proposition P can be proved in:

     - Constructive Logic
     - Classical Logic

2. Prove more constructive propositions using the `have` tactic.

3. Prove some classical propositions and understand
   why they cannot be proved constructively.

4. How to prove that a proposition is not provable.
   Can Lean help us for this?
-/

variable {P Q R S : Prop}
open Classical




--Constructive or Classical?
theorem ex1 : (P → ¬ Q) → (Q → ¬P) := by
sorry


-- Double Negation Introduction:
theorem ex2_doubleNegIntro : P → ¬¬P := by
  -- COnstructive: just needs intro and apply
  intro p
  -- goal is not not p: not p implies false
  intro notp
  apply notp
  assumption


-- Double Negation Elimination:
theorem ex3_doubleNegElim : ¬¬P → P := by
  -- not constructive: double negation, implication
  -- apply Classical.byContradiction
  -- ask Lean what it is
  -- #check Classical.byContradiction
  intro nnp
  cases em P with
  | inl p =>
    assumption
  | inr np =>
    have false: False := by
      apply nnp
      assumption
    cases false


-- Is this classical or constructive?
theorem ex4 : (P → Q) ∨ (Q → P) := by
  cases em P with
  | inl p =>
    right
    intro q
    assumption


  | inr np =>
    left
    -- use p imp Q using assimp q
    intro p
    -- now I have P and not P
    -- to prove Q, have false
    have False: False := by
      apply np
      assumption
    cases False



-- what about this one?
theorem ex5 : (P → Q → P) → P → Q := by
  intro pqp -- outermost operation
  intro p

  -- i have p imp q imp q and i have p, but want Q
  -- the trick: lean can help find the counterexample
  --

  have qp : Q → P := by apply pqp p
  -- we just know that if it rains then the ground is wet, just know the ground is wet, cannot say it rained
  -- how to get a counterexamples: we can just use:
  -- we have P in the list of assumptions, let's assume it is true, and assume Q is false
  take p : True
  sorry.

--ex
theorem ex6 : (P → Q) → ¬¬P → ¬¬Q := by
sorry

--ex
theorem ex7 : ¬ (P → ¬P) ↔ ¬¬P := by
sorry




----------------------------------------------
-- section2
-- Double negation elimination and the law of excluded middle are
-- equivalent to each other.

theorem ex8 : (P ∨ ¬P) → (¬¬P → P) := by
sorry


-- Question: Is there any constructive proof for (¬¬P → P) → (P ∨ ¬P)?
-- Can you prove the following proposition?
-- theorem ex9' : (¬¬P → P) → (P ∨ ¬P)  := by


-- However, you can do this one:
theorem ex9 : (¬¬P → P) → ¬¬ (P ∨ ¬P)  := by
sorry



-- So what it means when we say LEM and DNE are equivalent?
-- Think about it first, but you can find the answer in the solution.


--------------------------
-- The following classically valid proposition is called Peirce's law.
-- It can be proved that it is equivalent to the law of excluded middle,
-- Therefore it is not constructive.
theorem ex10 : ((P → Q) → P) → P := by
sorry

-------------------------

```




- To **prove** True, we just use `constructor` (because `True` is just `\and`).  We can't use True.

- To use assumption: the goal needs to be the same as one of the assumptions.
- `have` can be used to take existing assumptions and create new assumptions. 

- If the goal matches the right hand side of an existing implication assumption, you can just apply it.

- To prove an or (i.e. there's a `Q \or P`goal and we already have a `Q`), we use `left`/`right`

  have qp : Q → P := by 

![IMG_20251009_165557.jpg](IMG_20251009_165557.jpg)


- Cases on False kills it.

When there is a contradiction, the below boilerplate can instantly "solve" it as being false.

```haskell
have pcf : False := by 
	apply nnp
	assumption

cases pcf
```







