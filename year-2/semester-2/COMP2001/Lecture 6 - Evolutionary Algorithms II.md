# Lecture 6 - Evolutionary Algorithms II

Instead of configuring an algorithm, is it possible to let the algorithm decide what approach to use?

This lecture teaches how to identify types of evolutionary algorithms, the issues with the choice of representation (particularly binary problem which require **permutation representation**) related to the choice of genetic operators. Also, the basic components of Multimeme Memetic Algorithms, to design a new Genetic/Memetic algorithm to an unknown problem. 

Based on experience, memetic algorithms perform very well. Even with the same population time and generations, the performance can vary.

> A **meme** means hill climbing/local search. For example, random mutation hill climbing or Davis's Bit hill climbing.

A genetic algorithm in 1 iteration creates 2 solutions, iterates and evaluates them. With a memetic algorithm, we do not just mutate and evaluate: we mutate *and* apply hill climbing to evaluate a candidate solution. 

We may also benefit from combining several memes, and if this makes a difference to the \[] algorithm.

## Benchmark functions
Benchmark functions are used to test performance comparison for any given search algorithm designed for optimisation. 

These are functions with a known global minimum, can be computed easily, and represent different real-world problems - such as separable vs non-separable. 

### Benchmark functions, classified
Generally, we classify benchmark functions in terms of continuity: discontinuous and continuous. 

We also have dimensionality: a 3D benchmark function is harder to solve than 2D, etc. The question raised is: can we use the same function on multiple dimensions? If true, the function is known as scalable. 

Separability is a property: given a function p variables, can all p variables be minimised individually \[]. IT helps with delta/incremental evaluation. 

Modality: uni-modal means it can contain one local optima or **multimodal** with a few local minima or with an exponential number of local optima. These are not global, as we try to create a "difficult" search landscape that has many local optima points. 


### Sphere function (unimodel)
This is a continuous, differentiable, separable and scalable (modality can be increased) function. It is easy to arrive at local optima very quickly, because of the gradient. 

![Pasted image 20260303162409](../../../Images/Pasted%20image%2020260303162409.png)

Separable functions allow delta evaluation. 

![Pasted image 20260303162704](../../../Images/Pasted%20image%2020260303162704.png)

Here, the sequence represents numbers squared. The delta is simply the difference between the last and the first. 

### Rastrign's function
![16](../../../Images/Pasted%20image%2020260312130129.png)

### Ackley's function
It only has 2 variables, x1 and x2, 


## Optimisation representation

We use encoding and decoding to represent different scenarios. For example, to represent $-512 < x \le 512$, we can use 10 bits. 

- -511 would be `00000 00000`
- -510 would be `00000 00001`

First, convert the binary number to decimal, and subtract 511 to obtain its encoding.

Given a chromosome of 30 bits, we can encode the values in x1, x2 and x3 (with 10 bits each). We then decode it by add the squares of each 3 values to compute the overall fitness value. 

### More options

To handle decimal/real numbers e.g. $-5.12 < x_i \le 5.12$, we cna use the same numbers as above but divide by 100 at the end. 


We need to see how the algorithm changes, with a number of bits we increase, we increase the solution size which will also be a larger search space. 

### Types of benchmark functions

- Rosenbrock: a valley to escape and peak to climb before the final descent
- Foxhole: "needle in a haystack" - many local optima to escape and it is extremely difficult to find the global optima
- Royal Road: many repeat numbers 

### Gray encoding vs binary
Gray encoding is similar to binary, but in that it ensures there is a hamming distance of 1. To go from 0 to 1, there is only 1 bit change in both. `000` -> `001`. However, from 3 to 4, binary would change all bits: `011` -> `100`. Gray encoding changes this to be `010` -> `110`.


### Termination and performance criteria

Benchmarks are designed to be easy. It is common to repeat runs 50 times, and performance indicators include: 
- Success rate - how many runs return the optimal solution, versus the total number of runs.
- The average number of evaluations/configurations (efficiency)

After 50 runs, we count the number of successful runs where the optimal value is achieved. 


Different memes yield different performances, so to tackle a problem, we should use many different memes. If we need a quick implementation, DBHC is generally the best. 


## Encoding the TSP

A bianry representation is not suitable for the TSP, as it can cause illegal tours to form - including not all cities being visited, undefined city codes, visiting cities multiple times and loops forming within the tour. Therefore, **repair algorithms** are needed.

![Pasted image 20260303170751](../../../Images/Pasted%20image%2020260303170751.png)


## Generic permutation-based genetic operators

### Partially-mapped crossover (PMX)

This operator builds offspring by choosing a subsequence of a tour from one parent. It uses two randomly-cut points to serve as swapping boundaries, and swaps the segmenets between cut points. **The middle points are swapped, but the other (entrance/exit) points are kept the same.** It preserves the order and position for as many cities as possible from another parent, exploiting similarities in both the value and order.


### Order crossover ([OX](ox.ac.uk))

This operator builds offspring by choosing a subsequence of a tour from one parent, and preserves the relative order of cities from another parent. 

It tries to keep the order of cities, but not the location.

### Cycle Crossover (CX)

This tries to maintain the position of a city from one of the parents, and tries to complete a cycle. Once done, the remaining cities are filled from the other parent. 

It preserves the absolute positions of elements from the parent sequence. 

1. Randomly select a starting point in `p1`.
2. Follow the mapping from this point to the next.
3. Once a point on maps to the starting point, it recognises this and completes.
4. Element indexes that have not been visited are 

## Multimeme memetic algorithms

This introduces memetic material for each individual, to co-evolve genetic and memetic material. 

This allows a meme to encode *how* to apply an operator, when to apply it, where to apply it and how frequently to apply it. The meme of each operator can be combined under a **memeplex** - the algorithm decides when to apply each of these. 

### Features

They feature:
- Memes represent instructions for self-improvement
- Interaction between memes and genes are not direct
- Memes can evolve and change 

%%
He goes from "easy to understand" to "if you can understand it, that's great" in 15 minutes. 
%%

### Implementation

![Pasted image 20260303173843](../../../Images/Pasted%20image%2020260303173843.png)

TO propagate genetic material into offspring, we look at 

> Innovation rate (IR) between 0-1: **the probability of mutating memes** (memetic material). 
> At 0, there is no innovation. With all the memetic material in a population, it never changes in offspring and children. 
> At 1, all different strategies implied by all available memes, $M$, may be used equally. 

Mutation randomly sets all memetic material to different values. 

### Evaluating meme performance

The concentration of a meme is the total number of individuals that carry the meme $i$ (a certain value) at a given generation of population.

The evolutionary activity of a meme is the accumulation of a meme conenctration until a given generation (how many times a meme has been used in a population). The slope in a plot represents the rate of meme concentration increase.

![Pasted image 20260303174808](../../../Images/Pasted%20image%2020260303174808.png)



### Compound of Memes






