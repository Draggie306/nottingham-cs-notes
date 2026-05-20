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

- Exact methods systematically traverse the search space and are guaranteed to eventually find the optimum. Dynamic programming (COMP2054) is an example. 
- Inexact methods are not guaranteed to find the optimum. They use heuristics to sample the search space and attempt to move in a better direction over time.

There are also many search paradigms:

- **Deterministic** search (typically exhaustive) will always give reproducible answers.
- **Stochastic** algorithms use an element of randomness to traverse - and may not give the same result.
- Local search only performs a search refinement in a given neighbourhood. 


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


### Binary-represented solutions

Where each bit represents a boolean value, we can flip a bit with the bit-flip operator. This has a hamming distance of 1: the difference between two bit strings of equal length: `HD(00110, 00111) = 1`.  For a string of length $n$, the neighbourhood size is $n$ (as we can reach all solutions by applying it once), and the hamming distance is always 1.


## 3. Metaheuristics


## 4. Move Acceptance


## 5. Evolutionary Algorithms


## 6. Hyperheuristics


## 7. (Bonus) Fuzzy Systems


