ex

```haskell
/-

    Lecture 4

-/


variable {P Q R : Prop}

example : True := by
  constructor

-- P ∧ True =

-- There is no way to prove false
-- ex Falso quod libet : from False everything follows

theorem efq : False → P := by

  intro pcf -- pigs can fly
  cases pcf


example : ¬ (P ∧ ¬ P) := by
  intro pnp
  cases pnp with
  | intro p np =>
    apply np
    exact p



-- Cut (have) : a stepping stone from one side to the other; an intermediate step

theorem double_or : R ∨ R → R := by
  intro rr
  cases rr with
  | inl r =>
    assumption
  | inr r =>
    assumption

example : ( P → Q ∨ Q) → P → Q := by
  intro h p
  apply double_or

  -- q or q is the conclusion of h, so apply it
  apply h
  assumption



-- Cut the proof without naming another
example : ( P → Q ∨ Q) → P → Q := by
  intro h p


  -- If we need an external lemma, we can either give it a new name above or use it in the middle of the proof
  have qq : Q ∨ Q := by -- have to prove the stepping stone before using it
    apply h
    assumption


  cases qq with
  | inl q =>
    assumption
  | inr q =>
    assumption




-- de Morgan rules

theorem dm1 : ¬ (P ∨ Q) ↔ (¬ P) ∧ (¬ Q) := by

  constructor
  . intro npq
    constructor
    . intro p
      apply npq
      left
      assumption
    . intro q
      apply npq
      right
      assumption

  . intro npnq
    intro pq
    cases npnq with
    | intro np nq =>
      cases pq with
        | inl p =>
          apply np
          assumption
        | inr q =>
          apply nq
          assumption


-- if you negate a conj, the conj flips and becomes disj

theorem dm2 : ¬ (P ∧ Q) ↔ (¬ P) ∨ (¬ Q) := by
  constructor

  . intro npq
    right
    intro q
    apply npq
    constructor

    sorry

    -- .


  . intro npnq pq
    cases pq with
    | intro p q =>
      cases npnq with
        | inl np =>
          apply np
          assumption
        | inr nq =>
          apply nq
          assumption

```