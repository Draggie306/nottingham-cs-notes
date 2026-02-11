
A **metaheuristic** is a **high-level**, **problem-independent** framework, providing strategies for developing heuristic optimisation algorithms.

Metaheuristics are slightly higher-level, compared to previous components of heuristic search with low-level and hill-climbing heuristics.

### Classification and examples of metaheuristics
- Local search *single-point, trajectory methods that impove a single solution over time.*
	- Simulated Annealing (next week's lab - to implememt)
	- Guided Local Search
	- Iterated Local Search
- Population-based - *evolve a set of solutions over time*.
	- Genetic Algorithm
- Constructive - *where we start from no/partial solution, to derive a complete solution*.


### Components
The basic components of heuristic searches are still used:
- Solution representation
- Initialisation method
- Neighbourhood function
- A cost/evaluation function (helps evaluate the quality, guiding the search to a local or (hopefully) global optima)

We also need:
- Way to escape local optima
- Termination condition (when do we know we have found a solution? need to define something to stop it)
- Multiple move operators (previously - a single way e.g. hill climbing; metaheuristics can use multiple)

### Escaping local optima

We can very quickly get stuck on local optima depending on the search landscape. The heuristics show there is no guarantee it will find the global optimum, instead, the function hopes it will improve.

- Applying a hill climbing heuristic in a local optimum will not change the result. To escape, we can either **move to a random solution**, or **generate a random solution**. 
- We can also **change the objective function** that evaluates a solution, or use **different neighbourhood operators** - allowing us to find different solutions.

- Another option is to maintain a memory to prohibit certain moves, such as Tabu Search.
- We can also change the way to accept certain moves. Sometimes, we can get stuck on some regions, so accepting regions can escape some regions

No mechanism is guaranteed to escape effectively from all local optima.

### Termination criteria 
We can choose to stop searching depending on many factors:
- Iteration-based: stop after 1000 iterations, returning the best found of these.
- Moves: from one to the next may not be the same as 
- Objective function changes: some make the result worse, so revert this.
- CPU time: everyone has different CPUs so the result will be different depending on the hardware.

Others can look at the search progress. As we are moving to new regions, we may be able to detect if we are at the end of the search.
- Number of iterations since the solution was improved. (if at the best solution, escape, and find another solution that is "better". This can go on repeatedly, so limit this based on time since last optimum)
- Evidence that we are at the optimum (difficult as there is no guarantees; however, for some e.g. minimum satisfiability, if the result is 0, it is the best possible.)
- No feasible solution within a fixed limit.

### Feasibility of solutions
Not all solutions are feasible - they do not satisfy the constraints. For example, the 0/1 Knapsack problem 


To deal with infeasibility, we can penalise constraint violations by including them in the objective function:
- We can set a fixed penalty for any infeasible solution to make them more unlikely they are searched.
- We can also set a penalty value based on the level of infeasibility: if we exceed the knapsack capacity slightly, we apply a small penalty, but a larger penalty for large violations
- We can add a term to the objective function such that the cost of a solution with any violation is worse than that of the worst feasible solution, so it is never searched. 

## Iterated local search

We perturb the solution (could be better/worse than current), then immediately improve it with hill climbing. We keep repeating it until the termination criteria are met, returning the best one. 

If the **perturbation strength** (CRUCIAL) is too high (e.g. 10 bits vs 1 bit), then we may jump over something the local optimum, into somewhere entirely different. Generally, for all search landcapes, we want to stay in regions that are "close" to the same region (unless we are stuck). Likewise, if the strengh is too small, we may end up back in a valley of a local optimum.

![[../../../Images/Pasted image 20260210164334.png]]

To improve this, we can have acceptance criteria, or memory for restarts (to replace the current solution with a perturbed solution).

#### Creating an ILS algorithm
To create an ILS algorithm, we need to choose each of the following
- Generating an initial solution - *random initialisation*
- Perturbation - *random bit flip*
- Hill climbing - *Steepest Descent Hill Climbing with 1-bit-flip neighbourhood*
- Move acceptance - *non-worsening moves only*

```

(1) (0) (1) (1) (1) (1)

012345
111100

```


For long computational budgets, the strategy to initialise a solution does not matter (reconsider for low budgets). The local search should also be fast and effective - steepest descent is much slower than Davis's bit. Ideally, when choosing the pertubation operator, we do not want the local search to undo the perturbation bit - as this may cause a cycle, with hill climbing reverting the pertubation depending on its strength, so they should be unrelated.

Advanced methods ma change the perturbation strength during the search or use memory to replace the current solution if it is determined to be stuck in a wider, locally-optimal space

