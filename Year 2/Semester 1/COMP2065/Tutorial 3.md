

## Quantifiers

How to PROVE them (when they are in the goal):
- `∀ x, P x`: Use `intro x`. This gives an arbitrary `x : A` and a new goal `P x`.
- `∃ x, P x`: Use `exists x` to provide the witness
              and get the goal `P x` immediately.

How to USE them (when they are hypotheses):
- `h : ∀ x, P x`: Use `apply h`. Or, create a specific copy by `have`.
- `h : ∃ x, P x`: Use `cases h with | intro x hx => ...`. This gives you
                  a *specific* element `x` and a hypothesis `hx : P x`.








### Foralls/universal quantifier
When we want to prove a forall, we should use intro (similar to implication).

`intro x` gives us a term inside the forall.

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

The `rw` tactic uses equality.
- `rw [h]`: If `h : x = y`, changes `x` to `y` in the goal.
- `rw [← h]`: If `h : x = y`, changes `y` to `x` in the goal.
- `rw [h] at p` : If `h : x = y`, changes `x` to `y` in the assumption `p`.

The `rfl` tactic proves any goal of the form `t = t`.

**Whenever we have (notequals), it can be rewritten and applied:**
`a ≠ a3` is equivalent to `(a = a3) -> False`





