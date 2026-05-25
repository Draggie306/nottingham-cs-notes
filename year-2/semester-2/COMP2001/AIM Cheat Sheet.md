# Artificial Intelligence Methods - All Notes

## 1. Introduction and Key Terms 
 
A number of related elements that, together, perform an activity, function or task is a **system.** These systems can be closed (independent from the environment they interact with) or open (interact with their environment). 

These systems can be compared based on their **effectiveness** (to what extent goals are achieved) and **efficiency** (how well the inputs & resources are used to achieve an output; such as speed/memory usage).

Problems - the high-level, abstract question or optimisation issue - can be solved based on searching for **paths to goals** (like in a graph; BFS, DFS, A* algorithm), or for **searching for solutions** themselves through optimisation. 

To search for solutions, a candidate solution is needed. These can be represented/encoded as e.g. a path through a tree, or in binary. The effectiveness of a solution can be represented with an objective function. Generally, optimisation attempts to minimise or maximise this value. 

### Optima

For any solution space (the set of all possible solutions), there may be a local and global optimum.

- The **global optimum** is better than all other solutions in the space.
- A **local optimum** is better than all other solutions in a given **neighbourhood**. A neighbourhood is a solution that can be reached by applying an operator or heuristic.

For example, defining N as ±δ:

![](../../../Images/Pasted%20image%2020260520143833.png)

### Search spaces

The search space may be **continuous** or **discrete**. 
- Continuous search spaces involve curves, a range of values between numbers, etc. For example, the best orientation to place a wind turbine
- Discrete search spaces have a series of specific variables. For example, a series of backpacks with fixed capacities need to carry as many items with specific weights as possible. (Knapsack problem)


NP-complete problems have a yes/no answer. Solutions of NP-hard problems grow exponentially with instance size. **Most real-world problems are both NP-complete and NP-hard**. Combinatorial optimisation problems require finding the optimal solution from a finite solution set - is both NP-complete ("is \[representation\] the best solution") and NP-hard (by definition).

Search methods can be either **exact** or **inexact**.

- Exact (exhaustive/systematic) methods systematically traverse the search space and are guaranteed to eventually find the optimum. Dynamic programming (COMP2054) is an example. 
- Inexact (approximate/local-search) methods are not guaranteed to find the optimum. They use heuristics to sample the search space and attempt to move in a better direction over time.

There are also many search paradigms:

- **Deterministic** search (typically exhaustive) will always give reproducible answers.
- Single-point search uses a trajectory
- Multi-point search uses a population of solutions at once
- **Stochastic** algorithms use an element of randomness to traverse - and may not give the same result.
- Local search only performs a search refinement in a given neighbourhood. 

Solutions can be complete - used by perturbative heuristics, or partial - used by constructive heuristics.



### Heuristic methods

Heuristics are problem-dependent search methods that try to find "good enough" solutions in a reasonable time and computational period. Optimality is not guaranteed.

Heuristic methods are necessary: solving the TSP with 81 cities gives 5.8 x 10^120 possible combinations, which would take too long. 


## 2. Searching and Hill Climbing

### Solution Representation 

When searching, each solution for a specific problem must be encoded. A representation should have a degree of:

- completeness - it can represent all solutions to the problem
- connexity - if there is a path between a candidate solution and all other candidate solutions in the search space
- efficiency - if it is fast and easy to change the representation and encoding

This can be done in multiple ways:

- binary representation - each bit represents each of the $n$ variables being True or False. Useful when each variable is a Boolean decision. The search space is $2^n$.
- permutation representation - each permutation has an index to represent the order to travel in. Search space is $N!$
- integer encoding - each entity (item) in the representation corresponds to a choice, e.g. type of material 
- value encoding - each entity is given a real value, such as a floating point number, direction, DNA sequence, etc. 


### Moving between solutions

Where each bit represents a Boolean value, we can flip a bit with the bit-flip operator. This has a hamming distance of 1: the difference between two bit strings of equal length: `HD(00110, 00111) = 1`.  For a string of length $n$, the neighbourhood size is $n$ (as we can reach all solutions by applying it once), and the hamming distance is always 1.

Similarly, a random move operator replaces a value with another from a specific alphabet alphabet `Σ`. Where `Σ={3,5,7,9}` and `X=5559` with one replacement we can create `9559`. This has a neighbourhood size of `(k-1) n`, as each value in the solution can be changed to each of the others in the alphabet. The hamming distance is also 1.

For adjacent swap, that swaps two adjacent values in the representation, its neighbourhood size is `n-1` as there are always 1 fewer adjacent pairs than values. Its hamming distance is 2.

Pairwise exchange swaps two different (randomly-selected) entries in the representation.  This has the neighbourhood size `(n (n-1) )/ 2` Rationale:
- pick one from `n` vales
- pick another from all other values (so `n-1` values left) 
- giving `n(n-1)` distinct pairs
- halve it, as e.g. swapping positions `(3, 1)` is the same as `(1, 3)`
The hamming distance is also 2.

### Hill Climbing
Hill climbing is a local search technique that moves in the best direction compared to an objective solution, to find the lowest/highest point in the search landscape. It attempts to balance **exploration** and **exploitation**: going to many values within a search space, and exploring/refining its guesses in a good-looking region, respectively. Going over 

First-improvement hill climbing goes over all bits in the current solution, then performs a heuristic on it. If the resulting objective value is better than the current best, the heuristic is accepted. Best-improvement goes over all values sequentially, performing the same evaluation, but only keeps the change that resulted in the best objective value. Davis's bit hill climbing is similar to best-improvement in that it iterates over all values in the solution representation, applying the heuristic operator, but does not just keep the "best" - it keeps all changes based on the move acceptance criteria. As best-improvement (steepest descent) only accepts one move even if changing all bits result in improvements, Davis's bit is more efficient. 

Hill climbing can be made with a variety of move acceptance criteria, such as strictly improving (MUST BE better than the current solution) or just non-worsening (better OR equal to the current solution).

These algorithms are very easy to implement (only needing a solution representation, evaluation function, and "neighbourhood" definition) but suffer from getting stuck in local optima/valley (if exploration is not balanced), and can get stuck on a plateau if all states in the neighbourhood result in the same evaluation value.  Further, there are no optimality guarantees, being an exact method, and cannot see/know the global optimum value so only has the starting value as a point of comparison. Although these can be mitigated with e.g. Random Restart heuristics, there will still be no guarantee - to help resolve some challenges, we use **metaheuristics** (see below).


## 3. Metaheuristics

Metaheuristics are high-level, problem-independent frameworks to provide strategies for developing optimisation algorithms. 

There are 3 types: **local search** metaheuristics are single-point, trajectory methods that improve a single solution over time; **population-based** that evolve a set of solutions, and **constructive** metaheuristics that create new solutions starting from nothing or a partial solution.


### Metaheuristic components

There are three additional components for a metaheuristic, in addition to those of a standard heuristic:

- a way to escape local optima
- a termination condition - how to know when to stop searching 
- multiple move operators - metaheuristics can use several whereas heuristics may only use one

These components/parameters can be made in two ways:
- **Parameter control**: happens online (whilst the metaheuristic is running), as a response to changes in the search space state.
- **Parameter tuning**: happens offline, defining the initial settings for optimisation.


#### Local search metaheuristic template
Generally, local search metaheuristics do the following:

- Initialise a solution
- While termination conditions are **not** satisfied:
	- Move to a neighbouring solution (possibly based on **memory**)
	- Decide whether to accept this move or revert it

### Escaping local optima

Depending on the search landscape, we may get stuck on local optima quickly. Applying hill climbing in a local optimum will do nothing - there are no better solutions in the local neighbourhood. To resolve this, there are no guarantees, but we can attempt to:

- Change the current solution when a local optima is detected:
	- **move to a random solution** in the neighbourhood
	- **re-initialise the whole solution**
- Change the search landscape and state:
	- **change the objective function** to prioritise something else
	- **use different neighbourhood operators** to find somewhere else to go
- **Keep a (short-term) memory to prohibit certain moves** - forcing the search to go in a worsening direction in the hopes a better one will be found afterwards (as seen in Tabu Search with a Tabu List)
- **Change the move acceptance criteria** from being strictly improving to non-worsening

### Termination criteria 

To know when to stop searching, or e.g. re-initialise the solution to explore more, we can terminate based on numbers of iterations elapsed, how many non-improving moves occurred, or even CPU time. We can also look at iterations since last improving solution, or evidence of being at the optimum - see below to understand more.

### Solution (in)feasibility 

A problem may have millions of possible combinations of solutions, but most of these could be **infeasible**. For example, exceeding the capacity of a bag with hundreds of things you can put in the bag (0/1 Knapsack problem).

There are generally two ways to deal with infeasibility: **repairing** and **penalising**.

- Infeasible solutions can be **repaired** into feasible ones. For example, we can remove an item from the bag until it matches the bag's capacity.
- **Penalising** can be used by considering this in the objective function evaluation. A penalty value can be applied **uniformly** or to the extent that the solution is infeasible. For example, exceeding the bag's capacity a lot makes the objective value significantly worse. This can be extended by e.g. making infeasible solutions worse than any possible feasible solution.

### Iterated local search

ILS is a good example about balancing exploration and exploitation, by visiting a sequence of optimal solutions. 

It does the same as the template above, but moving to a new neighbouring solution is based on performing **both a perturbation operation and then a hill-climbing operation**. These are controlled by a perturbation strength and also a depth of search. 
- **Perturbation strength** - exploration - increases the neighbourhood size: too large lose the good properties of local optima or jump over an optimum into somewhere different, whilst too weak may not be able to escape valleys in the search landscape.
	- *Generally, it is best to stay in regions close to the initial region, unless the search is stuck.*
- **Depth of search (hill climbing)** attempts to immediately improve upon the mutation by refining it. For example, if the search is perturbed onto a valley side, the hill-climbing operation will move it closer to the valley floor (for minimisation).

![Pasted image 20260210164334|339](../../../Images/Pasted%20image%2020260210164334.png)


The local search must be fast and effective; as this will be carried out several times during the search, choosing something like Davis's bit is much faster than steepest descent. The choice of perturbation should also be such that it is not easily undone by the local search - if the perturbation attempts to go up a hill, and hill climbing wants to go down, nothing happens. **Parameter control methods** from earlier can also be used to adapt perturbation strength if the state is determined to be stuck in a local optima.


### Tabu search 

This search method keeps a memory list of prohibited moved to avoid cycles. 

It contains a **forbidding strategy** to determine which moves to forbid, a **freeing strategy** (tenure) to remove (old) moves from the tabu list, and a **short-term strategy** to balance these.

Over a series of neighbourhood solutions, find the best one, and check if it is not in the tabu list. If it is, then choose the next-best one until one is available. Then, replace the current solution with it.

An example is below. Starting from `x0`, the search moves to `x2`. Crucially, after moving here, `x0` is added to the tabu list. This means that, despite `x0` having a better objective value than `x2`, it cannot be moved back to. As the only other element `x3` is in the neighbourhood, the search is forced to move in a worsening direction - but still closer to the global optimum. 

![](../../../Images/Pasted%20image%2020260525231502.png)


It is important to find a good value for tabu tenure (how long a search is on the tabu list before being freed). Small values will result in the same cycling, but high values mean the search becomes very restricted and loses the optima. An **aspiration level** can be defined to accept tabu moves, if a move meets this level. 


### Statistical Testing

- Comparing two algorithms with matched data: one-tailed Wilcoxon Signed-Rank Test.
- Comparing two algorithms with **unmatched** data: Mann-Whitney U Test
- 


## 4. Move Acceptance


## 5. Evolutionary Algorithms


## 6. Hyperheuristics


## 7. (Bonus) Fuzzy Systems


