**A recurrence relation is a recursively-defined function.** The function is some measure of resources used by some algorithm. It is used to classify the function in Big-O terms. A recurrence relation will express the runtime of T(n) size n in terms of its values at other smaller values of n.

### Mergesort

$T(n) = 2\space T(n/2) + b + a n$

- As merge sort splits the array into size of n/2, we use 2 T(n/2). 
- `b` is the cost of performing the split.
- `a n` is the cost of doing the merge


### Examples

Solving: `T(n) = 4 T(n/2)` with `T(1)=1`

- k = 1: `T(2)` = `4 T(1)` is 


## Pattern

1. Start from the base case, use the recurrence to work out many cases. Substitute and work upwards in terms of `n`.
2. Look for a pattern and make a hypothesis for the results.
3. Attempt to prove the hypothesis, using a form on induction.