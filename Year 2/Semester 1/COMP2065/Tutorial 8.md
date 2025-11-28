


## Definitions

```haskell
-- 1. Append (++)
-- If the first list is nil, the output is just the second list
def append : List A → List A → List A
| [],    bs => bs
-- Head is a, and tail is the rest....
| a::as, bs => a :: (append as bs) -- Recursively do it until the first is nil!
```

Equivalence: 
- `[1,2,3] = 1::[2,3]`
- `rev [2,3] = rev 2::[3]`


## Excercices
### Duplicate


```haskell
-- EXERCISE 1: Definition
-- Define duplicate. duplicate replicates each item in a list twice
-- #eval duplicate [1,2,3] should give [1,1,2,2,3,3]
def duplicate : List A → List A
-- constructors of the type list
| [] => [] -- duplicate of nothing is nothing

| a :: as => a :: a :: duplicate (as)

#eval duplicate [1,2,3] -- RESULT: [1, 1, 2, 2, 3, 3, 4, 4]
```


We can solve facts about lists using induction over lists.



### Inductions


```haskell
example : ∀ as : List A, ∀ a : A, a :: as = [] ++ a :: as := by
-- Doable by reflexivity: identity of nil is the same as after it
  intro as a
  rfl

example : ∀ as : List A, ∀ a : A, a :: as = a :: ([] ++ as) := by
  intro as a
  rfl
  -- These are provable without induction, so they should not
  -- require "redundant" induction operations to prove them

example : ∀ as : List A, ∀ a : A, a :: as = (a :: []) ++ as := by
  intro as a
  rfl

example : ∀ as : List A, ∀ a : A, a :: as = a :: as ++ [] := by
  intro as a
  -- 1. Think about brackets: append has more priority
  -- rfl : the elements are not definitionally equal

  -- We do not have the equality that "as append nil == as",
  -- so use the simp on the lemma app_nil_or
  simp only [app_nil_r]
```












