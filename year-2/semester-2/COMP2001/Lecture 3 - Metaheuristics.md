# Lecture 3 - Metaheuristics


A **metaheuristic** is a **high-level**, **problem-independent** framework that provides strategies to develop heuristic optimisation algorithms.

Metaheuristics are slightly higher-level compared to previous components of heuristic search with low-level and hill-climbing heuristics.

### Classification and examples of metaheuristics
- **Local search** metaheuristics are *single-point, trajectory methods that improve a single solution over time.*
	- Simulated Annealing (next week's lab - to implement)
	- Guided Local Search
	- Iterated Local Search
- Population-based metaheuristics *evolve a set of solutions over time*.
	- Genetic Algorithms
- Constructive - *where we start from no/partial solution, deriving a complete solution*.


### Components
The basic components of heuristic searches are still used:
- A solution representation - how it is encoded
- An initialisation method
- Neighbourhood function
- A cost/evaluation function (helps evaluate the quality, guiding the search to a local or (hopefully) global optima)

We also need:
- Way to escape local optima
- Termination condition (when do we know we have found a solution? need to define something to stop it)
- Multiple move operators (previously - a single way e.g. hill climbing; metaheuristics can use multiple)

### Escaping local optima

We can very quickly get stuck on local optima depending on the search landscape. The heuristics mean that there is no guarantee the global optimum will be found, instead, the heuristic function "hopes" it will improve in future iterations.

- Applying a hill climbing heuristic in a local optimum will not change the result (as there are no better solutions). To escape, we can either **move to a random solution**, or **generate a random solution** - this is known as reinitialisation. 
- We can also **change the objective function** that evaluates a solution, or use **different neighbourhood operators** - allowing us to find different solutions.

- Another option is to maintain a memory to prohibit certain moves, such as Tabu Search.
- We can also change the way to accept certain moves. Sometimes, we can get stuck on some regions such as plateaus, so accepting all non-worsening (therefore equal) moves can escape these regions.

**No mechanism is guaranteed to escape effectively from all local optima.**

### Termination criteria 
We can choose to stop searching depending on many factors:
- Iteration-based: stop after 1000 iterations, returning the best found of these.
- Moves: moving from one solution to another may not improve the objective function value, so stop it after a certain number of non-improvements. 
- Objective function changes: a new solution may be the same as the current. If it is worse, go back to the current solution. 
- CPU time: everyone has different CPUs so the result will be different depending on the hardware.

Others can look at the search progress. As we are moving to new regions, we may be able to detect if we are at the end of the search.
- Number of iterations since the solution was improved. (if at the best solution, escape, and find another solution that is "better". This can go on repeatedly, so limit this based on time since last optimum)
- Evidence that we are at the optimum (difficult as there is no guarantees; however, for some e.g. minimum satisfiability, if the result is 0, it is the best possible.)
- No feasible solution within a fixed limit.

### (In)feasibility of solutions
**Infeasible** solutions are those that do not satisfy the problem's constraints. For example, in the 0/1 Knapsack problem, all solutions that exceed the weight of the knapsack are infeasible.

There are generally 2 ways to deal with infeasibility: repairing and penalising. 
- We can **repair** infeasible solutions into feasible ones. For example, removing an item from the knapsack until it is under the limit.

We can penalise constraint violations by including them in the objective function in multiple ways:
- We can **set a fixed penalty** for any infeasible solution to make them more unlikely they are searched.
- We can also set a **penalty value**, based on the level of infeasibility: if we only exceed the knapsack capacity slightly, we apply a small penalty, but apply a larger penalty for larger violations.
- We can add a term to the objective function such that the cost of a solution with any violation is worse than that of the worst feasible solution, so it is never searched. 


General guidelines for searching techniques include to have a balance between exploration and exploitation. We can have a purely hill-climbing based method - which is bad as they can get stuck in local optima, or a purely random-walk (explorative) which has a large sample of the search space but is unable to improve the solutions it finds. 


### General template

For almost all local search metaheuristics, we:
```c

INPUT: s0 // Create starting solution

s* = initialise(s0) // Use the starting solution or improve on it


do
	s_prime = makeMove(s*, memory) // Choose a neighbour of s*, based on a neighbourhood relation or move sequence
	accept = moveAcceptance(s*, s_prime, memory) // Whether to move to neighbour or not
	if (accept)
		s* = s_prime // replace the old best with the new, for the next loop iteration
until all termination conditions are satisfied
```

We *can* replace the makeMove step with random initialisation. This is generally not a good idea - whilst there is a chance we create the best solution, it is less likely as we are not *exploiting* the search space in any way. 


## Iterated local search

Iterated Local Search (ILS) is about enforcing the balance between exploration and exploitation. It visits a sequence of optimal solutions.

```c
s0 = generateInitialSolution() // Use the starting solution or improve on it
s* = performLocalSearch(s0) // Optional.

do
	s_prime = performPerturbation(s*, memory) // a random neighbour - could be better OR worse than current
	s_prime = performHillClimbing(s_prime, memory)  // the best neighbor of the random neighbour - immedately following the perturbation, perform hill climbing to improve
	
	accept = moveAcceptance(s*, s_prime, memory)
	if (accept)
		s* = s_prime // replace the old best with the new, for the next loop iteration
until all termination conditions are satisfied

return s* // as the best solution
``` 

We perturb the solution (could be better/worse than current), then immediately improve it with hill climbing. We keep repeating it until the termination criteria are met, returning the best one. 

If the **perturbation strength** (CRUCIAL) is too high (e.g. 10 bits vs 1 bit), then we may jump over something a better region (an optimum), into somewhere different in the search space - essentially a random walk. **Generally, for all search landscapes, we want to stay in regions that are "close" to the same region** (unless we are stuck). Likewise, if the strength is too small, we may end up back in a valley of a local optimum.

![[../../../Images/Pasted image 20260210164334.png]]

To improve this, we can have **acceptance criteria** - e.g. non-worsening or stricly improving moves only - a move acceptance method (see Lecture 4), or memory - if details are remembered and the algorithm realises it is stuck, then restart by generating a random solution.

### Creating an ILS algorithm
To create an ILS algorithm, we need to choose each of the following
- Generating an initial solution - *random initialisation*
- Perturbation - *random bit flip, select a bit in the solution and flip*
- Hill climbing - *Steepest Descent Hill Climbing with 1-bit-flip neighbourhood - check all variables independently and choose the best one if it is better than current.*
- Move acceptance - *non-worsening moves only*

```
(1) (0) (1) (1) (1) (1)

012345
111100

```


For long computational budgets, the strategy to initialise a solution does not matter (reconsider for low budgets). The local search should also be fast and effective - steepest descent is much slower than Davis's bit. Ideally, when choosing the pertubation operator, we do not want the local search to undo the perturbation bit - as this may cause a cycle, with hill climbing reverting the pertubation depending on its strength, so they should be unrelated.

Advanced methods ma change the perturbation strength during the search or use memory to replace the current solution if it is determined to be stuck in a wider, locally-optimal space

