

## Analogy of evolution

> Evolution: gradual change in inherited characteristics of a population over successive generations

Many researchers believe that nature is a great problem-solver: complexity can be achieved in a short time. Can we simulate nature to solve complex problems on a computer?

### How evolution works
**Heritable characteristics or heritable traits** are passed from one generation to the next via DNA. 

Change, or genetic variation, comes from **mutation** (changes in DNA) and **crossover** (reshuffling of genes via sexual reproduction and migration between populations).

Evolution is driven by **natural selection - survival of the fittest**.

Genetic variations that enhance survival and reproduction become more common in successive generations of a population in an environment.



## Evolutionary algorithms: background


Evolutionary algorithms simulate natural evolution (Darwinian evolution) by using survival of the fittest, with selection, mutation and reproduction (recombination).

To carry out the search process, we do not use a single candidate solution: we use a population (set of individuals/chromosomes "alive"). Depending on the fitness of an individual (how close it is to the optimal solution), it may evolve from one generation to another.  The hope is that the last generation will contain the best solution.


## Genetic algorithms




The solution representation is in binary.

- Generate the initial population (intialisation): create the initial candidate solutions - the population contains the set of chromosomes/individuals (candidate solution)
- Calculate fitness values (objective/fitness function) evaluate the quality of the candidate solution. We need to say that e.g. candidate A is better than B. 

While the termination criteria is not satisfied: 
- Perform reproduction (select parents/mates). These candidate solutions will interact with each other, searching for the optimal solution.
- Apply crossover operation. To reshuffle the chromosomes, or candidate solution functions, we typically use a probability (0-1). In a standard genetic algorithm, this is typically 1; to apply it, we normally use a high value. After this, we have 2 new individuals/solutions.
- Apply mutation with a given probability to the new individuals. 
- Calculate the fitness values of the current population
- Replace the population with the new individuals


### Components 
- A genetic encoding for candidate solutions
- An initialisation function
- A fitness function to rate the solutions in the environment context
- A scheme for selecting mates for recombination
- Crossover/recombination of genetic material between mates
- Mutation of the new individuals
- Replacement strategy to select the next generation's individuals 
- Termination criteria
- Values for all of these parameters (probabilities, etc) - parameter tuning


### Initialisation
- Randomisation: each gene is given an allele value of 0.1 randomly.

### Tournament selection
This runs a number of "tournaments" among randomly-chosen individuals  and selecting the one with the best fitness at the end. This is repeated for each parent to recombine.

### Crossover
Selected mates are recombined. Crossover is applied with a crossover probability, generally close to 1. 

One-point crossover: generate a random number from 0-1. If it is smaller than the crossover probability:
- select a random crossover site
- split individuals
- swap the segments after the current position

otherwise, copy the individuals. 

![Pasted image 20260224171705](../../../Images/Pasted%20image%2020260224171705.png)



### Mutation



### Replacement Strategy
Strategies for replacing the old population (last generation) with the new offspring population to form the next generation. 


## Memetic algorithms
A meme is a contagious piece of information. 

Memes can change and evolve using rules and time scales other than traditional, genetic ones. Memetic algorithms aim to improve genetic algorithms by embedding local search.

The change versus genetic algorithms is just that a hill climbing step is applied after the offspring has been mutated. 




