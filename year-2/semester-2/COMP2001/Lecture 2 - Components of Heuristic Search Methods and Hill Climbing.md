- Intro to COmbinatorial Optimisation Problem
- Components of meta/hyperheuristic search methods
- Focus on hill-climbing/local search methods
	- These are fairly easy to apply to any computationally hard problem

### Bin Packing Problem

Given a set of items $I$, $| I | = n$, each with a size of $i j$, where $0 \le j \le n - 1$ and an unlimited number of bins.  The j value is the j number in the list. Each item has a fixed size and they go to fixed capacity bins. The goal is to minimise bin usage. 

### Travelling Salesman Problem 

Given a set of cities $C$ of size $N$, and distances between city pairs is $d(i, j$) for all $i \in C, j \in C$. What is the shortest route that visits each city once, and returns to the origin city


### 0/1 Knapsack Problem
Given a knapsack with capacity $C$, and a set of items $I, n = | I |$, where each item has a weight $wx$ and value $vx, 0 \le x \le n - 1$ , which should be packed into the knapsack to maximise the total value? As each item has a constraint, we cannot have all items in the bag.


### Boolean Satisfiability problem
All problems can be reduced to this. There are 2 problems: a decision and optimisation problem. 

NP-complete: computationally hard. Exhaustive methods can take forever for large size instances. 

Given a formula $\phi$ of $n$ Boolean variables $x$, where $0 \le i \lt n$, is there an assignment of True/False values to each variables such that $\phi$ is satisfied? (All variables made True)

Conjunctive normal form: 
$$( \lor ) \land ( \lor ) \land ( \lor )$$

> If there is a yes/no output (binary function) , such problems are decision problems.
> Combinatorial optimisation problems seek the best solution

![[../../../Images/Pasted image 20260203162441.png]]

Decision problems can be turned into combinatorial optimisation problems by saying "can the truth assignment that maximises the number of satisfied clauses". A simple yes/no is not sufficient.

## Components of meta & hyper-heuristic search

Initialisation methods and mechanisms for escaping local optima are essential for metaheuristic optimisation functions

### Representations

> Representation: the way to encode a solution to a problem. For example, an array showing the truth assignment for an associated variable.

Representations should be:
- Complete: if it is able to represent all possible solutions in the search space.
- Connex: a solution if, for all candidate solutions, there exists a search path between itself and all other possible solutions in the search space. (Should be able to reach all other encoding)
- Efficient: fast and easy to manipulate the representation's data structure - e.g. constant time. 

#### Binary (bitstring) representation
Used when each variable is a binary decision. Each bit represents each of the $n$ variables, each variable gets a True/False value.

A binary array of $n$ elements has a search space of 2<sup>n</sup>.

It is the common representation, and serves as the basis for most problems and other representations.

#### Permutation Representation
Used when a sequence of N events is being searched for. For example, the Travelling Salesman Problem (where this is called *path representation*).

Each entity in the permutation has an index that represents the order.


#### Integer Encoding 
Used to denote choices within each entity referenced by its index 
This is not a sequencing method - as each "layer" can use the same/previous entity.

Given a set of materials, $C, | C | = M = 5$, and a structure containing 8 layers, we can use integer encoding to represent solutions as $<11235532>$


#### Value encoding 
It may be seen to be common to use integer encoding for e.g. DNA sequencing. We can keep the same alphabet without using integer encoding - this is used for **continuous optimisation with real values**. 

Given a starting point and an end point, and a set of items to sample, find a point from the start tot the end that samples all items. This can be encoded with value encoding, such as $< (Up), (Left), (Left), (Up), (Right) >$. This is a playing strategy.


#### Non-linear encodings
Used in **generic programming** (a metaheuristic) where heuristics and components of heuristics can be generated. An example is tree encoding: the algorithm can return a tree of very large size (an algorithm, that can be used to solve optimisation problems), depending on the search space context. 

Different solutions are possible but may still be valid.


## Neighbourhoods
A neighbourhood of a solution is a set of solutions that can be reached by applying an operator/heuristic. 


### Binary-represented solutions
A bit flip operator flips a but in a solution. 

The **hamming distance** is the number of different bits. For example, `HD(00110, 00111) = 1`. 

For a binary string of length $n$, the neighbourhood size is $n$ and the hammering distance is 1. 

### Integer-represented solutions
A random operator replaces a discrete value with another, from a given alphabet $\Sigma$. For example, $\Sigma = { 0,1,2,3 }$ and  $X = 0023$ -> $2023$.

The hamming distance of a single, random perturbation is 1. 


### Permutation-represented solutions

- Adjacent (pairwise interchange/swap).
- Insertion operator.
- Exchange operator.
- Inversion operator

The adjacent (pairwise swap) operator swaps two adjacent entries in the permutation. For example: **51**432 -> **15**432. For a permutation of size $n$, the neighbourhood size is $n - 1$.  The hamming distance is always 2 - only the two swapped items.

Insertion:


Exchange: 


Inversion: 



## Evaluation functions
An evaluation function, or objective function, indicates how good a given solution is, between one that is objectively better or worse.

Designing an evaluation function is important:
- It needs to 

- Multimodal: number of global optima.



### Delta evaluation
The idea is to only update what has been changed. Data (or *incremental*) evaluation is used to improve efficiency by calculating the effects/differences between the current search position $s$ and a neighbouring solution, $s'$ on the evaluation function.

This allows us to search more points and is essential for efficient implementation of all types of heuristics. 



## Hill climbing
This is a local search algorithm that moves in the target direction (increasing/decreasing objective value) for a given problem (min/max) problem to find the (lowest/highest) point



### Random mutation hill climbing 
For the given problem instance, 





> Exploration: being able to jump to other, more promising neighbourhoods.
> Exploitation: 





