

### Foralls/universal quantifier
When we want to prove a forall, we should use intro (similar to implication).

`intro x` gives us a term inside the 

Naming conventions: big propositions can be introduced with a capital. 


%% ### Existential quantifiers
Use `apply` with the    %%

### Nots
NOT something is just `implies False`, so we can `intro` it. 


### Exists
Very similar to conjunction: we use constructor.


If I have an equality and want to use it:
- Tactic `rw` (rewrite) changes the goal 

Can rewrite an equality at an assumption with:
- Tactic `rw [\left p] at q` 

To prove equality:
- Tactic `rfl` 








