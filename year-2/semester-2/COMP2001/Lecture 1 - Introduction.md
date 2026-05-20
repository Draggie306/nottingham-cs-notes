

Many problems can all be solved by optimisation and search techniques.

The potential for optimisation/search techniques can automatically create timetables, decrease carbon emissions through routing/sequencing, reducing operational costs in supply chains, increase energy production with better windfarm layouts, optimising structures combining composite and porous layers.

Techniques include Genetic Programming, Grammatical Evolution, Genetic/Memetic Algorithms, Heuristics, Hyper-heuristics, Great Deluge, Simulated Annealing.

10-credit: theory. 20-credit: implementing and using these practically. 

First in-lab exam: in mid-March.
In-lab practical exam on project: solve unseen problems, how a hyperheuristic was designed. 

AI tools can be used, but only if you can explain your implementation.

Anything said, presented, written, on discussion forums, in demos, formative assessments is examinable. Lab material is examinable for coursework.

### Activities and Coursework
![Pasted image 20260127163715](../../../Images/Pasted%20image%2020260127163715.png)




A system is the number of related elements which together perform a function.

Two classes are used based on the dependence of the environment.

- Effectiveness: the degree to which goals are achieved. We can only approach, not always reach, it, in some systems.
- ….

**Searching paths to goals** involves finding a set of actions that will move from a given initial state to a goal state. It is used in many AI problems (A*, BFS, DFS). 

**Searching for solutions** is more general then searching for paths to goals. It is a general approach: it involves efficiently finding a problem solution in a large search space. It includes paths to goals. 

### Single-objective optimisation



Variables may/may not be bounded, and the search space may be infinitely large. 



### Local vs global optimum
The **global optimum** is better than all other solutions.

The **local optimum** is better than all other solutions in a given neighbourhood.

> In most cases, there is not a single optima, especially for local optima.

Algorithms should not stop at local optimums. It is common to get stuck at locally optimum locations.

![Pasted image 20260127170225](../../../Images/Pasted%20image%2020260127170225.png)


### Continuous vs Discrete Search Spaces

Continuous search space: find the optimum setting for the wing of a race car for the best performance. 

Discrete search space: assign tourist groups to buses to produce the optimum number of 70-seater tour buses for given tourist group sizes. All bus configurations are discrete.

- A **problem** is the high-level question/optimisation issue to be solved. 
- An **instance** of a problem is a concrete expression that represents the input for a decision or problem. 



- NP-Complete: responds to a problem with a yes/no answer.
- NP-hard: 

Combinatorial Optimisation problems requiring an optimal solution for a finite solution set. For NP-Hard problems, this finite set grows exponentially with instance size. 


- Inexact/local/approximate methods are our focus. These involve heuristics, hyperheuristic and metaheuristics, and there is no optimality guarantee.
- Exact/exhaustive/systematic: searches through all points, guaranteed to find the global optimum. 

There are also many search paradigms and there are different algorithms for each. Single-point/trajectory (our focus), multi-point/populations.

**Deterministic search** (usually exhaustive methods) walk the whole search landscape, vs **stochastic methods** involving randomness. 

Local search does not go through all exhaustive solutions, and just carries out the search in a given neighbourhood. 

### Bin packing problem
Underlying the tourist bus problem is the bin packing problem. 


## Heuristic Search and Optimisation


Heuristic approaches for the Travelling Salesman Problem includes the Nearest Neighbour algorithm. 

1. Choose a city randomly.
2. Travel to the nearest neighbour to this city.
3. Choose the nearest unvisited city, repeatedly until all cities are visited. 

Constructive Stochastic Local Search:


1. Choose a random city.
2. Apply Nearest Neighbour.
3. Compare the new solution to the best solution found so far, updating if needed.
4. Repeat for n iterations is reached
5. Return the best solution.

### Recap: caveats of heuristic search:

- There are no optimality guarantees
- Ususally new heuristics are required for different problems - different heuristics for different problem domains.
- Often parameterised and sensitive to their settings - e.g. number of iterations
- It may result in poor-quality solutions when used for different problem instances or if it is applied a second time (for stochastic methods).

## Pseudo-random numbers

As stochastic heuristic searches use random numbers (unlike deterministic heuristic search algorithms), multiple runs should be performed for the same instance, and we use different metrics such as calculating the **average performance**. Being able to repeat and replicate trial runs for experiments is very important, too. 

To repeat the randomness, we use seeding. They appear to be random but are actually deterministic. A good pseudo-random geenrator has a large number of periods; Java’s random has a period of 2<sup>48</sup> 









