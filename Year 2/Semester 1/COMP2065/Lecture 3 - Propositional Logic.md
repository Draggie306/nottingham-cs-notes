

```ts

-- intro: assumes the left 

variable (P Q R : Prop)

-- ↔ is defined as P -> Q and Q -> P

-- Proving a conjunction:
example : P → Q → P ∧ Q := by
  intro p q -- introduction for conjunction

  -- Constructor makes 2 goals: left and right
  constructor -- Shortcut for "and,intro"
  
  . assumption -- left state
  . assumption -- right state

example : P ∧ Q → P := by
  intro pq
  cases pq with

  -- the below has nothing to do with the above intro
  | intro p q =>
    assumption

-- A curry theorem
-- P → Q → R
-- is the same as:
-- P ∧ Q → R

-- Brackets are optional here. When written using a tree, ↔ is at the top.
theorem curry : (P → Q → R) ↔ (P ∧ Q → R) := by
  constructor -- Is needed to prove both directions

  . intro pqr
    intro pq

    cases pq with
    | intro p q =>
      apply pqr
      . assumption
      . assumption
    

    -- . cases pq with
    --   | intro p q → 
    --     assumption
    
    -- -- have to prove the other side:
    -- . cases pq with
    --   | intro p q => 
    --     assumption
    
  . intro pqr p q
    apply pqr 
    constructor 
    . assumption
    . assumption 


-- Proving disjunction P ∨ Q : the sun shines OR we go to the zoo
-- There are 2 ways to prove: left, right
example : P → P ∨ Q := by
  intro P
  left
  assumption

example : (P → R) → (Q → R)  → P ∨ Q → R := by
  -- means: if sun shines then children happy, if zoo then children happy, then if the sun shines OR go to the zoo THEN happy
  intro pr qr pq

  -- Apply is a bad idea here
  -- There are 2 cases:
  cases pq with
  | inl p => 
    -- we know P and want R
    apply pr
    assumption

  | inr q => 
    -- we know Q but want R
    apply qr
    assumption

-- what is left:

```