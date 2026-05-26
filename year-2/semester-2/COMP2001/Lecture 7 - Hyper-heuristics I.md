# Lecture 7 - Hyper-heuristics I


### Background
Hyperheuristics raise the generality of the solution, introducing a level of abstraction.

- Heuristics are problem-specific methods to define the neighbourhood of a solution: how objective values are defined, the neighbourhood, etc. **Key point: if we need to solve a slightly different problem, we may need to significantly change the heuristics.** They have a high development cost & time. 

- Metaheurisitcs provide definitions for how we can design methods for solving multiple problems. However, we must design e.g. mutation operator, hill-climbing operations, which often require domain expertise. 

- A single search method can be used to solve different types of problems - that are unknown, problems that have not been designed yet. They do not require problem-specific information. The idea: if we have a general solver, we can solve a new problem without needing any more information. 


### Definition
Hyperheuristics are high-level search methods or learning mechanisms for selecting or generating heuristics to solve computationally difficult problems. The difference is that hyperheuristics operate on the search space of low-level heuristics whereas metaheuristics operate on the search space of solutions. 

Hyperheuristic research is motivated by raising the level of generality of search methods, aiming towards the general solver. 


## Selection hyper-heuristics

There exists a problem domain barrier that hides low-level heuristics that affect the problem domain. We initialise a solution, and select a heuristic below the problem-domain barrier, identifiable by an ID. All that is known about the heuristic is its name and ID. 

They select from a predefined set of available heuristics - not deciding which bit to flip, etc. 

The size, difficulty, optimality of different heuristics affect which solution is the most advantageous. Generally, hyperheuristics are easy to implement and design: we just need to define a problem domain of heuristics. Metaheuristics can be embedded within the heuristics (ILS says perturbation then hill climbing for local search)

Hyperheuristics can learn or not. 
- No learning: predefined series/random selection of variables. 
- Offline: tune in advance based on a training set, but the parameters do not adapt over time
- Online: takes in feedback during the search to affect parameters.

Heuristic generation: smaller heuristic components that combine to solve a problem
- Constructive heuristics: build a solution up from an empty or incomplete solution.
- Perturbative heuristics: take complete, change something, to find a neighbouring



## HyFlex (Hyper-heuristics Flexible Interface)

The steps are broadly defined as:

- Init solution at some memory index
- Set the current solution $s$  to the initialised ones
- While the termination criteria is not satisfied:
	- Select one or more low-level heuristic(s) $h \in H$ 
	- Generate a new candidate solution by applying it to $s$
	- Decide to accept or reject
- End while
- Return the best solution found

**The domain barrier restricts what information is passed between the domain and hyper-heuristics layers.**

Methods are called in the domain layer with a reference to (j: current solution) 

- A predefined set of problem domains (problem-specific)
- Hyflex, an abstraction layer
- A predefined set of hyperheuristics (general-purpose)

### Framework
Each of the 6 problem domains (MAX-SAT, bin packing, TSP, etc.) define a set of low-level heuristics.

Hyperheuristics can control the parameterised settings (e.g. depth of search and intensity of mutation) based on their types. 
### 1D bin packing
Objective funciton minimises fullness across all open bins.

The HyFlex framework provides a set of instances. For example, it can set bin count and capacity, alongside generating an integer solution representation. 

Mutation heuristics can include:
- swapping (selects items and swaps bins if there is a space)
- splitting (selects a bin with more items than the average, into 2 bins containing half the number of items)
- repacking (removes all items from lowest-filled bin, repacking them into remaining bins with the best-fit heuristic)

IoM: defines how many low-level heurstucs repeat; 0.2 = once, 1 = 5 times

Hill climbing heuristics include:
- first-improvement with swap (swaps 2 items randomly keeping the new solution if it is non-worsening)
- HC1 (First Improvement (IE) with Swap from lowest filled bin) – Takes the largest item from the lowest filled bin and swaps it with the smallest item from a randomly selected bin (subject to feasibility and improvement).

Depth of search defines how many times each LLH is repeated with 0.2 = repeat 10 times through 1.0 = repeat 20 times.

Ruin-and-recreate heuristics include: 
- destroy x hughest bin (remove all items from the x highest-filled bins and repacking them with best-fit)
- destroy x lowest bins (same as above but lowest)
- etc.



### CheSC
For every problem instance, we look at the leading result (all hyperheuristics in the competition) uses the Formula 1 ranking system. 


## Selection hyperheuristics

These are a class of hyperheuristics that select from one or more defefined lowlevle heuristics to be applied to the solution, at a given point in the search.

- Non-learning selection hyper-heuristics: arbitrarily choose from a set of LLHs
	- Random selection: applies a low level heuristic at random to the solution.
	- Greedy selection: applies each low-level heuristic, choosing the one that moves in the most locally-promising direction. 
	- Tournamnt greedy selection: chooses a subset of e.g. 3 randomly-chosen LLHs, going to the best solution within this subset. 
- Selection HHs contain learning mechanisms for selecting the best heuristic from a set, at any point in the search.

> CW: use further reading here to find the best one.


### Reinforcement learning 
If it does something bad, punish, else, reward the heuristic.

Heuristics can be given certain scores (e.g. 0-100%) with higher scores having a higher probability to be selected. This is repeated over multiple iterations: after each iteration, the score can change. (We can also punish based on other factors, e.g. time taken to generate the solution)

To reward and punish:
- multiplication can be used (asymmetrically): score times 1.1 if good (small benefit), 0.5 if bad (significant punishment, halving the score)
- decide if equal solutions should be rewarded or punished? (as the score is not getting worse)
- decide how scores are initialised (all 5? 10? even need to be equal)
- decide how to handle tied scores

During RL, different LLH can be selcted based on probability.

### Choice function
The choice function considers multiple LLH performance metrics to give a score:

- Individual performance
- How well the LLH performend when previously applied 
- If a heuristic has not been applied in a long time, it may perform better now - prevents starvation

Ideally we apply the LLH that runs faster and results in the best solution quality. 


## Examples of selection hyper-heuristics


### Framework for single-point search

![Pasted image 20260310172605](../../../Images/Pasted%20image%2020260310172605.png)



Multistage:
- There are 2 hyperheuristics, S1 and S2
- S1 is fast but simple.
- S2 is slow but more sophisticated.
- S2 is applied after S1 based on a random probability.




Hyper-hyper-heuristics: select from the set of hyperheuristics (no currnet research on this?!) - hyper$^2$ heuristics / hyper-factor heuristics - my idea



## Steady-state memetic algorithms

Select 2 parents, crossover, mutation and local search, but immediately replace the worse of 

When the tournament size is the population size, we chose 


