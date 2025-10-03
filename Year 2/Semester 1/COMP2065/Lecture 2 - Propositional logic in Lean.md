Mathematicians are interested in making sure their proofs are correct.

Propositional logic: how to combine propositions. A proposition is an unambiguous statement that may want to be proved.


```lean
  
-- Telling Lean that each variable is a proposition

variable {P Q R : Prop}

  

-- P = the sun shines

-- Q = we go to the zoo

-- R = the kids are happy

  

-- Propositional connectors
#check P

#check P ∧ Q -- \and
#check P ∨ Q -- \or
#check P → Q -- \implies
#check True -- it sometimes rains in England
#check Flase -- pigs can fly

#check ¬ P -- ¬
#check P ↔ Q -- \iff; logically equivalent; imply each other
```


Tautology is a statement containing propositional variables that is true for any assignment of propositions. Tautology does not tell us about anything, just that it is True.


To prove an implication: you assume the left and prove the right. In Lean, we use intro
