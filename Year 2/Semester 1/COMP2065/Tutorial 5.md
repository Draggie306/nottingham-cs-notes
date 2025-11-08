Coursework 4: always use cases where something is contradictory. Do not use contradiction 

![[Pasted image 20251107112451.png]]

```
/-
Introduction to Formal Reasoning (Comp 2065)
Tutorial 05: The Booleans
Date: 06 Nov 2025
TA: Aref Mohammadzadeh
You can download tutorial files from moodle `Tutorials -> Aref`.

-/

/-
## Tactics for today:
- `dsimp [_]`  and `dsimp [_] at _`
-  And again, `cases`, this time for `Bool`

-/


--def not : Bool → Bool
-- | true  => false
-- | false => true

-- def and : Bool → Bool → Bool
-- | true, b  => b
-- | false, _ => false

-- def or : Bool → Bool → Bool
-- | true, _  => true
-- | false, b => b

-------------------------------------------------
namespace tuorial05
/-
# Part I : Underestanding Booleans
-/
theorem ex1 : ∀ x : Bool, (x && true) = x := by
-- Generally, in logic, we first hae to understand the statement to prove.
  intro x
  cases x
  -- now two goals: we are doing cases over Bool
  -- as x is in Bool
  -- . dsimp [and] -- goal is now solved, Lean understand False && True by definition is false, and by definition, False and False are equal.
  . rfl -- dsimp is not necessary, Lean is smart to use rfl
  . dsimp [and]


-- Prove or disprove:
def Ex2 := ∀ x : Bool, ∃ y : Bool, (x && y) = false
theorem ex2 :  Ex2 := by
  intro x

  -- we must now use a boolean here, x && what is false? False
  -- very important: for an arbitrary x we should False to prove it

  exists False
  cases x
  . rfl
  . rfl

-- Prove or disprove:
-- there exists a bool such that it is itself, which is = to not of it.. or not of it? false by counterexample

def Ex3 := ∃ x : Bool, (x && x) = (! x || ! x)
theorem ex3 :  ¬ ∃ x : Bool, (x && x) = (! x || ! x)  := by
  intro H
  -- when we have an existential statement in props, best way is to use cases to split it up
  cases H with | intro a ha
  . cases a

  -- this is used when we want to prove something, and sometimes we want to prove false, from which we can prove whatever we want
  -- "ha is a contradictory statement, so from it, you can prove whatever you want"
    . cases ha
    . cases ha



--Prove or disprove:
def Ex4 := (∀ x y z : Bool, (x && (y || z)) = ((x || y) && (x || z)))

theorem ex4 : Ex4 := by
 sorry


theorem ex5 : ¬(∀ x y : Bool, ∃ z : Bool, (x && y) = (x || z)) := by
-- the statement: it is not true that .....
-- therefore there must be a counterexample
  intro H
  have htf := by
    apply H true false
  cases htf with | intro z hz
  dsimp [and , or] at hz
  cases hz



-- for all bools, there is a bool not equal to the firt, and everything else is either equal to the first or second one
-- it is true, but just says bools are complemented: if x is true, we have to choose false.
-- because everything inside type of boolean is either true or false.
theorem ex6 : ∀ x : Bool,  ∃ y : Bool, y ≠ x ∧ (∀ z : Bool, z = x ∨ z = y) := by

/- -- Proof 1:
intro x
cases x
. exists True
. exists False
-/

  intro x
  exists (! x)
  -- prove and with constructor
  constructor
  . cases x
  -- rlf doesn't work as we are trying to prove inequality
    . intro p
      cases p
    . intro q
      cases q

  . intro z
    cases x
    . cases z
      left
      rfl
      right
      rfl
    . cases z
      . right ; rfl
      . left ; rfl



-------------------------------------------
/-
# Part II : From Bool to Prop:
-/

def isTrue : Bool → Prop
| b => b = true
-- sends any boolean to a proposition

theorem ex7 : ∀ b : Bool, isTrue (true || b) := by

  intro b
  dsimp [or, isTrue]

  -- goal is isTrue or b, so use... dsim



-- it is not true that forall false is b
theorem ex8 : ∀ b : Bool, ¬ isTrue (false && b) := by
  intro b
  intro h
  dsimp [and] at h
  cases h -- this works because is true of false 



theorem ex9 : ∀ x : Bool, ∃ y : Bool, (isTrue (x || y) ∧ isTrue (x && y)) ↔ isTrue x := by
sorry



theorem ex10  : ∀ a b : Bool, isTrue (a || b) ↔ isTrue a ∨ isTrue b := by
sorry




-- Challenging question for home:
theorem ex11 (f : Bool → Bool) : isTrue (f true && f false)
                              ↔ (∀ x : Bool, isTrue (f x)) := by

sorry

```