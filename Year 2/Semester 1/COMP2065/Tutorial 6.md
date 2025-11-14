Nat is a type. Succ of N goes from zero to infnity.

When we want to define a function out of natural numbers, we specify what numbers should be applied to what.

> For Booleans, functions were constructed as being True or False.

```haskell
def double : ℕ → ℕ
| zero => zero
| succ n => succ (succ (double n))
```


To define `isEven`, we use `def isEven : ℕ → Prop`

```haskell
def isEven : ℕ → Prop
| zero => True
-- Successor is dependent: succ of 0 is odd but succ(1) is even.
| succ (zero) => False
-- The succ of succ is the same
| succ (succ n) => isEven n
```

When we want to prove a general fact about booleans, we used cases over a general term.

For natural numbers, we use induction over the term we want inducted.

```haskell
theorem ex02_double_isEven : ∀ n : ℕ, isEven (double n) := by
```

```haskell
  intro n
  induction n with
  -- Want to prove that isEven of double is zero

  -- First, we start from double of zero is zero,
  -- then isEven of zero is true.
  | zero => dsimp [double]
            dsimp[isEven]
```

... and using the previous introductions for nprime:

```haskell
  -- First, use dsimp over double (internal)
  -- this creates a simpler goal.
  | succ n' ih => dsimp[double]
  -- we know that isEven of (succ (succ (something))) is/
  -- the same, so use isEven of it
                  dsimp[isEven]
                  -- finally, use induction hypothesis
                  exact ih
```


## Injectivity

> "if these functions are equal over 2 inputs, then the 2 inputs should be equal to each other."

To prove succ (m) and succ (n) 

Among constructors there is a function, then this function behaves like an injective function. We usually want to change the goal completely when this is the case.

The same statement, but give another proof for it. 

```haskell
example : ∀ m n : ℕ, succ m = succ n → m = n := by
intro m n h
change pred (succ m) = n
rw [h]
-- the result is definitionally true.
rfl
```

The predecessor of the successor of something is always itself. There is no need to prove that either side is equal; Lean itself can go and change it. 

```haskell
theorem ex03_double_comm : ∀ (m n : ℕ), double (m + n) = double (n + m) := by
  intro n m
  -- now prove double of m + n is double of n + m
  -- we can use the lemmas: use commutativity

  rw [add_comm]
```

In coursework, we always have to use `rw` over simple facts about addition and multiplication. In part 2, there is something very useful for Coursework 5.

## Part 2: calc

```haskell
theorem ex04_half_double : ∀ n : ℕ, double n = n + n := by
```

"For all natural numbers, double of natural numbers is = to n + n". Note that this is NOT definitionally equal: double is one funciton and addition is another funtion. BUT, we want to prove that addition of n with itself is = to double n

```haskell
  intro n
  induction n with
  -- always give 0 case first: trivial here
  | zero => rfl -- Can also use dsimp [double]
    | succ n' ih =>
    -- Calc is useful for many calculations at once
    -- here, this is double of n' + 1 + 1, as defined in double function
    -- the "calc" environment is very free: any
    calc double (n' + 1) = double n' + 1 + 1

```


In every line, we want to prove something: after the equal, we give the prove. WE can change to the tactic mode with the "by" keyword.

After this above snippet, we want to use the induction hypothesis:

```haskell
calc double (n' + 1) = double n' + 1 + 1 := by rfl
                      _ = (n' + n') + 1 + 1 := by rw [ih] 
```

Now, Lean is expecting two different types, so we should rewrite it via lemmas:

```haskell
    calc double (n' + 1) = double n' + 1 + 1 := by rfl
                      _ = (n' + n') + 1 + 1 := by rw [ih]
                      _ = n' + (n' + 1) + 1 := by rw [← add_assoc]
                      _ = n' + (1 + n') + 1 := by rw [add_comm n' 1]
```

In many situations, Lean understands where a lemma should be applied, but not in certain other cases. 

Apply a commutativity lemma over a specific term is required. The full proof is thus:

```haskell

theorem ex04_half_double : ∀ n : ℕ, double n = n + n := by
  -- for all natural numbers, double of natural numbers is = to n + n
  -- this is NOT equal: double is one funciton and addition is another funtion
  -- BUT, we want to prove that addition of n with itself is = to double n
  intro n
  induction n with
  -- always give 0 case first: trivial here
  | zero => rfl -- Can also use dsimp [double]
  | succ n' ih =>
    -- Calc is useful for many calculations at once

    -- here, this is double of n' + 1 + 1, as defined in double function
    -- the "calc" environment is very free: any
    calc
    -- Have what we have on the left hand side of the goal
      double (n' + 1) = double n' + 1 + 1 := by rfl
                      _ = (n' + n') + 1 + 1 := by rw [ih]
                      _ = n' + (n' + 1) + 1 := by rw [← add_assoc]
                      _ = n' + (1 + n') + 1 := by rw [add_comm n' 1]
                      _ = (n' + 1) + n' + 1 := by rw [← add_assoc]
                      -- The right hand side finally apply associativity over the whole statement: addition (brackets) is from left, so apply nprime outside of the brackes
                      _ = (n' + 1) + (n' + 1) := by rw [add_assoc]
```


In coursework, intro terms, find the best term for the induction, solve the zero and base case, then solve the rest in the calc environment.

This is not one of the coursework questions but should be used as a lemma to work out the answer to the questions. 

```haskell
theorem ex06_mult_suc_lemma : ∀ n m : Nat , succ n * m = n * m + m := by
```




