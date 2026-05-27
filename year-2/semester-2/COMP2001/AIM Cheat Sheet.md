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


NP-complete problems have a yes/no answer. Solutions of NP-hard problems grow exponentially with instance size. **Most real-world problems are both NP-complete and NP-hard**. Combinatorial optimisation problems require finding the optimal solution from a finite solution set - is both NP-complete (asks "is \[representation\] the best solution?") and NP-hard (by definition).

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

![Pasted image 20260210164334339](../../../Images/Pasted%20image%2020260210164334.png)


The local search must be fast and effective; as this will be carried out several times during the search, choosing something like Davis's bit is much faster than steepest descent. The choice of perturbation should also be such that it is not easily undone by the local search - if the perturbation attempts to go up a hill, and hill climbing wants to go down, nothing happens. **Parameter control methods** from earlier can also be used to adapt perturbation strength if the search is determined to be stuck in a local optima.

### Tabu search 

This search method keeps a memory list of prohibited moved to avoid cycles. 

It contains a **forbidding strategy** to determine which moves to forbid, a **freeing strategy** (tenure) to remove (old) moves from the tabu list, and a **short-term strategy** to balance these.

The general idea: "Over a series of neighbourhood solutions, find the best one, and check if it is not in the tabu list. If it is, then choose the next-best one until one is available. Then, replace the current solution with it."

An example is below. Starting from `x0`, the search moves to `x2`. Crucially, after moving here, `x0` is added to the tabu list. This means that, despite `x0` having a better objective value than `x2`, it cannot be moved back to. As the only other element `x3` is in the neighbourhood, the search is forced to move in a worsening direction - but still closer to the global optimum. 

![](../../../Images/Pasted%20image%2020260525231502.png)


It is important to find a good value for tabu tenure (how long a search is on the tabu list before being freed). Small values will result in the same cycling, but high values mean the search becomes very restricted and loses the optima. An **aspiration level** can be defined to accept tabu moves, if a move meets this level. 


### Statistical Testing

Generally, a confidence interval of 95% is used to determine statistical significance.

- **One-tailed test**: if one (improvement/decrease) results in a corresponding change in the other. **Two-tailed test**: if one change in one affects another, either positively or negatively way.
- Comparing two algorithms with matched data: **one-tailed Wilcoxon Signed-Rank Test.**
- Comparing two algorithms with **unmatched** data: **Mann-Whitney U Test**
- Results can be compared with (notched) boxplots; if the notches/IQR does not overlap, the difference can be concluded to be statistically significant. 


## 4. Move Acceptance

There are many ways to accept moves, including **stochastic** decisions (randomly accept a percent of non-accepting moves), or non-stochastic methods that are based on **known values** **(basic)** or **calculated values** **(threshold)** - often based on a combination of a small offset and the current best found in the search - before deciding to accept.

### Acceptance configuration

Acceptance methods can are often parameterised - allowing for configurations to control whether moves are accepted. There are three main parameter settings:
- **static** - behave the same throughout the search. They have a fixed value: "accept worsening solutions if below 𝜀"
- **dynamic** - behave differently, based on a predetermined value e.g. interval/time/iterations. 𝜀 often decreases over time - allowing more changes at the start and "refining" the search later on.
- **adaptive** - behave differently, based on the current search conditions or memory. Adapts 𝜀 based on time AND also memory/state, often to create a threshold "target" value.

Examples of solution acceptance can are: comparing its objective value to pre-existing values (non-stochastic basic), or a chosen "better" value (non-stochastic threshold), or a random value is created at the start based on the known solution values (stochastic static), or a random probability is updated as the search finds better solutions over time (stochastic adaptive).

For example, accepting all non-worsening moves would be classified as static, non-stochastic basic acceptance: it behaves the same and does not change criteria during the search, does not use a randomisation element, and is based on known values (previous/current objective function value).

Late acceptance is a **non-stochastic basic adaptive** method as it accepts worsening moves if not worse than the move accepted a number of moves ago, configured at the start but changes based on the search state.

Moves acceptance can made in groups for single-stage search methods, with multiple acceptance methods deciding on a consensus. For multi-stage search methods, different move acceptance methods can be made dependent on the current search stage. 

### Example algorithms

#### Great Deluges

Great Deluge is a **dynamic, non-stochastic threshold** acceptance method that only accepts worsening moves if not worse than a water level that decreases based on a "decay rate" over time. 

Extended Great Deluge is an **adaptive, non-stochastic threshold** method that uses the similar decay rate from Great Deluge, but allows restarts based on when the search is deemed to be stuck (after a certain number of non-improving iterations)

#### Simulated Annealing

Simulated Annealing is a **dynamic, stochastic** method that accepts worsening moves based on a probability that decreases over time and a "Boltzmann probability". 

Accepting a move is defined as: `Δ < 0 || 𝑟 < 𝑃 Δ, 𝑇`. If the delta (change from previous -> current solution) is better (`< 0`), it is always accepted. 

The Boltzmann probability: $P(Δ,T)=e^{\frac{−Δ}T}$. If the delta is 0 (equal cost), `e` becomes 1, so it is always accepted. 

Cooling schedules are very important and can have a big effect on the performance. They usually consider an initial $T_0$ and final $T_f$ temperature, mechanism to decrease the temperature, and the number of iterations per temperature. $T_0$ should start "hot" to allow must but not all worsening moves and can be set statically or dynamically. The final temperature should be close to 0. Example schedules include:

- **Linear** cooling - fixed reduction each iteration
- **Geometric cooling** - multiplies temperature by 𝛼 - around 0.99 every iteration, cooling quickly initially but slowing down later.
- **Lundy and Mees** uses a parameter 𝛽 close to 0.0001 similar to geometric cooling. Current iteration/1 + 𝛽\*iteration.

Simulated Annealing with Reheating extends this to be an **adaptive, stochastic** method, by increasing the temperature at certain points depending on e.g. if the search has not improved after a given number of iterations. 


### Parameter configuration


Parameters tuning occurs before the search process - such as changing mutation intensity in ILS or the starting temperature in SA. Parameter control adapts the parameters during the search process, such as increasing mutation intensity when the search is stale.

This can be done **arbitrarily** - randomly picking 𝛼 or 𝛽 values, or by **trial and error**, or **sequentially** going through a series of 𝛼 and 𝛽 to find the best combination.

### Experiment design

To help find the best parameters, there are three main sampling methods: **random** "m" number of configurations, use a **Latin hypercube** to not pick similar settings, or use an **orthogonal grid** to divide a search space into subspaces to explore. 


![](../../../Images/Pasted%20image%2020260526145247.png)


## 5. Evolutionary Algorithms

EAs simulate Darwinian evolution and the idea of "survival of the fittest" via selection, mutation and recombination. 

An **individual/chromosome** is a candidate solution for a problem. A set of individuals is the **population**. This population can **evolve** from one **generation** to the next (every iteration of the GA) depending on individuals' **fitness** (objective values) within the population. The last generation should contain the best solution.

**Evolutionary programming** evolves the parameters of a program with a fixed structure over time. **Genetic programming** evolves programs themselves, if represented in tree form. 

### Genetic algorithms

A genetic algorithm should have the components of (meta)heuristics: **representation** for candidate solutions, objective function (now **fitness function**), perturbation (**mutation**) and termination criteria. Additionally, GAs have an **initialisation scheme** to generate the first set of candidate solutions, a scheme for **selecting parents** and a way to **combine genes between parents** to **construct new child solutions** in the next generation. Additionally, values such as crossover rates, population sizes, number of generations/iterations etc. are used. 

#### Genetic algorithm template
Generally, GAs do the following:

- Initialise a population
- Calculate fitness of all individuals in the population
- While termination conditions are **not** satisfied:
	- Select parents and reproduce
	- Recombine parent genes by crossover
	- Mutate the new child genes
	- Calculate fitness values of all children
	- Replace the population with the new children

### GA components

The **fitness value** indicates how fit (and, by extension, how likely) it is to survive and reproduce to the next iteration. The fitness value is calculated from applying the fitness function to the chromosome (candidate solution).

- The genotype is the solution representation - e.g. 010101.
- The phenotype is the "decoded" result of applying the genotype. For example if 010101 results in there being 1 unsolved solution in a MAX-SAT problem then the phenotype is 1.
	- *This is similar to biology; the phenotype is the observable "result" of the encoded genotype*

The **reproduction** process requires the selection of (typically 2) parent candidate solutions. **Selection pressure** determines how strongly the selection process is "elitist": high pressure means greater chance of choosing fittest individuals. This is often done by:

- a **tournament selection** process: where a number of "tournaments" is conducted over a random number of individuals (tour size). The fittest individual is chosen at the end, and is repeated for both parents (and can choose the same parent!).
- a **roulette wheel selection** process - where the whole population's fitness is evaluated, and the probability of selecting any given individual is based on its "slice" of the overall population's fitness. (*A simplified version of this is sorting and ranking from best to worst fitness.*)

Recombination is applied with a crossover probability: $p_c$ which is often close to 1. If this probability is reached, **one point crossover** splits the parent chromosomes at a random point, and exchanges one "segment" from one parent with the segment of the other parent, creating two new individuals. *If the crossover probability is not reached, the parents can be copied into the next generation anyway.*  Other crossovers exist, such as **uniform crossover** (considering each bit in the parent strings, and having a half chance to copy each). 

**Mutation** is then **applied to the children**, with a small chance $p_m$ of occurring for each gene in the chromosome - `1/chromosomeLength` gives an average of 1 gene mutation per individual. This allows for some **diversity** and allows the search space to explore different regions and, again, balance exploration and exploitation. 

Finally, the **population is replaced**.  The **generation gap** (𝛼) refers to the percentage of population to be replaced. As the population size must stay fixed, a value of 𝛼=0.02 over a population of 100 results in 2 offspring being produced. A value 𝛼 = 1 over the same population size means 100 new offspring will be created, all replacing the previous generation.

**Transgenerational generic algorithms** produce 𝛼N offspring. Therefore, we temporarily have `N + 𝛼N` individuals. This must be reduced back to N, so we often replace the worst 𝛼 individuals from the old population. 

**Convergence** is the progression towards uniformity between individuals. When 95% of a population have the same gene, it is converged. When all genes have converged, this is **genotypic** convergence. When all fitnesses approach the best individual in the population, this is phenotypic convergence.

The evolutionary algorithm will continue until **termination criteria** are satisfied. This could be genotypic convergence, a static number of generations, or a combination of termination criteria.


### Memetic algorithms

Memes can change over time with different rules, compared to genes. A meme is essentially a local search heuristic, that explicitly balances exploitation and exploration. Compared to GA, MAs apply the local search operator after offspring have been mutated - such as DBHC - before being added to the next generation.

### Benchmark functions

Benchmark functions are pre-existing search spaces that have been searched extensively already. This allows meta- and hyper- heuristics to be tested on them. They have a known global minimum and can be easily computed, potentially representing existing real-world problems. They also have several characteristics that allow us to determine how well they perform ***and*** how likely they are to fail/get stuck.

- Generally, we classify benchmark functions in terms of **continuity**: continuous vs discontinuous.
- **Dimensionality** also generally increases the difficulty of a benchmark function. 
- **Separability** affects difficulty, with separable functions being much easier to solve a each variable is independent of other variables (and calculating for delta evaluation is more efficient) - and each can be tuned/controlled independently.
- **Modality** also has an influence: **unimodal** means it contains one optimum, whereas **multimodal** means the solution can have a few local minima or a huge number of local minima.

> To work out if something is separable (**and can be delta-evaluated**), ask if the equation permits writing each term with only one variable. For example: $f(x_1,x_2,x_3)=x_1^2+\sin(x_2)+x_3^4$ IS separable because each term only uses one variable. However: $f(x_1,x_2)=x_1x_2$ is NOT because one term uses two coupled variables.

### Optimisation representation

We use encoding and decoding to represent different scenarios. For example, to represent $-512 < x \le 512$, we can use 10 bits. 

- -511 would be `00000 00000`
- -510 would be `00000 00001`

First, convert the binary number to decimal, and subtract 511 to obtain its encoding.

Given a chromosome of 30 bits, we can encode the values in x1, x2 and x3 (with 10 bits each). We then decode it by adding (the squares of) each 3 values to compute the overall fitness value. 

Encoding representations in binary can also be challenging. A **hamming wall** can be reached when it is unlikely that the genetic algorithm will mutate in a way to produce a better fitness value: e.g. changing `011` to `100` requires all bits to flip for a change in value of just one. To solve this, we can use **gray encoding**: adjacent numbers always have a single-digit difference.

![](../../../Images/Pasted%20image%2020260526195941.png)

### Genetic permutation operators

Partially-mapped crossover creates new offspring by choosing a subsequence from one parent, choosing two "cut points", and swapping the segment between the cut points. The other (entrance/exit) points are kept the same, keeping the order and position for cities from the other parent.

Order crossover exploits the property that the order, not the location, is what is important. It chooses a subsequence of a tour from one parent and copies the cities in the same order for one parent into the other.

Cycle crossover selects a starting point in the first parent, and copies the corresponding city in the second parent at the index, into the offspring. This corresponding city is then found back in the first parent, and then the corresponding parent is indexed at the same location, copying into the offspring. This is copied until a cycle is found, and the complement is then the other offspring.

### Multi-meme memetic algorithms 

MMAs give each individual in the population two types of information. This allows for the co-evolution of both genes and memes in an individual:

- **genetic material** - chromosome; the solution encoding itself,
- **memetic material** - instructions for how that individual should self-improve. 

A meme encodes how to apply a local search operator: where (before/after mutation), when (iteration limit, acceptance criteria), how to apply it (by using DBHC/SDHC) and how frequently to apply it (always/1 in `n` iterations). We can combine multiple memes into a **memeplex** that each individual can choose from.

Memes are mutated based on their **innovation rate**. Mutation affects parameters like mutation probability, crossover probability, where to apply hill climbing, the number of iterations for the hill climbing step, etc. This is typically encoded alongside the solution representation (genetic material). 

![Pasted image 20260303173843](../../../Images/Pasted%20image%2020260303173843.png)

An innovation rate of 0 means there is no innovation, and memetic material does not change in children. With an innovation rate of 1, all available memes and all available strategies may be used equally. This can also be used in the benchmark function.

Memes can be evaluated by their **concentration** in the generation ($c_i(t)$) or by their **evolutionary activity** - a slope that accumulates that shows rate of meme concentration increase.

MMAs help to identify the best memes within a memeplex, and can also help to find "synergy between memes" to find even better solutions more quickly. If there are many different memes and meme operators, then experiment design should be used to reduce the number of options for a more optimal performance of the MMA.

## 6. Hyperheuristics

Hyperheuristics are high-level search methods and learning mechanisms that **select or generate heuristics** to solve problems. They operate **on the search space of lower-level (meta)heuristics, not the search space of solutions** themselves. Because of this, they are more "general" and aim to be useful for a broader range of problems "general-purpose solver", by taking advantage of the heuristics that perform well and avoiding the weaker ones. It does not use any problem-specific knowledge - there is a **domain barrier**.


### Selection hyperheuristics

The size, difficulty and optimality of different heuristics affect which solution is the most advantageous. Generally, hyperheuristics are easy to implement and design: we just need to define a problem domain of heuristics, which will then be evaluated based on the selection mechanism. **All the hyperheuristic knows is the name and ID of the heuristic below the problem-domain barrier.** 

Hyperheuristics can **learn**, not. 
- No learning: predefined series/random selection of variables. 
- Offline: tune in advance based on a training set, but the parameters do not adapt over time
- Online: takes in feedback during the search to affect parameters.

#### Selection hyperheuristics template
Generally, Selection HHs do the following:

- Generate initial solution
- Set current solution as initial solution
- While termination conditions are **not** satisfied:
	- Select heuristic(s) to apply
	- Generate a temp solution by applying heuristic to current solution
	- Decide to accept or reject the temp solution
	- If accept, replace current solution with temp solution
- Return current solution as the best solution







## 7. (Bonus) Fuzzy Systems


