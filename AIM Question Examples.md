

## week 1: basics
 decision support systems are dependent on their environment, while  decision support systems are entirely independent of their environment. A decision support system that can solve a given problem instance to optimality can be considered  . If the optimal solution is achieved fast by that decision support system, then it can also be considered  .
Feedback
Your answer is correct.
The correct answer is:

[Open] decision support systems are dependent on their environment, while [Closed] decision support systems are entirely independent of their environment. A decision support system that can solve a given problem instance to optimality can be considered [Effective]. If the optimal solution is achieved fast by that decision support system, then it can also be considered [Efficient].
Question 2
Correct
Mark 1.00 out of 1.00
Flag question
Question text

A search algorithm based on the nearest neighbor constructive heuristic/operator can always find a better solution than a search algorithm based on the pairwise exchange perturbative heuristic/operator for solving a given instance of the Travelling Salesman Problem.
Question 2 Answer
True
False
Feedback
The correct answer is 'False'.
Question 3
Correct
Mark 2.00 out of 2.00
Flag question
Question text

The solutions obtained from a search method applied to a problem instance could vary at each run of that algorithm whereas a search method will always give the same solution given the same problem instance.

A search algorithm processes and returns a complete solution at all times, while a search algorithm can process a partial solution returning a new partial or complete solution.

Feedback
Your answer is correct.
The correct answer is:

The solutions obtained from a [stochastic] search method applied to a problem instance could vary at each run of that algorithm whereas a [deterministic] search method will always give the same solution given the same problem instance.

A [perturbative] search algorithm processes and returns a complete solution at all times, while a [constructive] search algorithm can process a partial solution returning a new partial or complete solution.

Question 4
Incorrect
Mark 0.00 out of 1.00
Flag question
Question text

In continuous optimisation,  the variables used in the objective function are required to be chosen from a set of real values between which there are no gaps (values from intervals of the real line).
Question 4 Answer
True
False
Feedback
The correct answer is 'True'.
Question 5
Correct
Mark 1.00 out of 1.00
Flag question
Question text

   1   long seed = 12345; 
   2   Random generator = new Random(seed); 
   3   double num;
   4   for (int trial=0; trial<3; trial++) 
   5   {

   6       num = generator.nextDouble() ; 
   7   }
   8   System.out.print(num);

Given the code above and assuming that the seed 12345 produces the following sequence of double values in the given order

<12.3, 75.489, 92.2, 6.8123, 1.234, 54.005, 72.01, ....>

which value would be printed out at line number 8?
Answer: Question 5
Feedback
The correct answer is: 92.2
Question 6
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Which one of the following algorithms is an exact method?
Question 6 Select one:
a.

Simulated Annealing
b.

Branch and Bound
c.

Genetic Algorithm
d.

Tabu Search
Feedback
Your answer is correct.
The correct answer is: Branch and Bound
Question 7
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Choose the statement or statements that can be considered as a drawback of using heuristic search methods for optimisation in problem-solving. 
Question 7 Select one or more:
a.

Usually, they can be used only for solving the problem for which they are designed.
b.

There is no guarantee for the optimality of the obtained solutions.
c.

Many heuristic search methods have parameters and their performance can be sensitive to the settings of those parameters.
d.

They may result with a near-optimal solution.
e.

They may result with  a poor solution.
Feedback
Your answer is correct.
The correct answers are: There is no guarantee for the optimality of the obtained solutions., Usually, they can be used only for solving the problem for which they are designed., Many heuristic search methods have parameters and their performance can be sensitive to the settings of those parameters., They may result with  a poor solution.
Question 8
Correct
Mark 1.00 out of 1.00
Flag question
Question text

A seed value will correspond to a specific sequence of generated values for a given random number generator.
Question 8 Answer
True
False
Feedback
The correct answer is 'True'.


## week 2: heuristic components and hill climbing
Question 1
Correct
Mark 1.00 out of 1.00
Flag question
Question text
Assume that the implementation of Davis's Bit Hill Climbing for MAX-SAT internally uses an accept-only-improving-moves strategy within. How might this strategy be changed (without accepting the worsening moves) to potentially improve the performance of Davis's Bit Hill Climbing?
Question 1 Select one:
a.

Accept only bit flips resulting with a FALSE truth assignment for the related literal
b.

Accept bit flips resulting in improving or equal solution costs
c.

Accept all bit flips
d.

Accept bit flips resulting in a better solution cost
Feedback
Your answer is correct.
The correct answer is: Accept bit flips resulting in improving or equal solution costs
Question 2
Correct
Mark 1.00 out of 1.00
Flag question
Question text

The First Improvement Hill Climbing algorithm may get trapped at a local optimum regardless of the problem dealt with.
Question 2 Answer
True
False
Feedback
The correct answer is 'True'.
Question 3
Correct
Mark 1.00 out of 1.00
Flag question
Question text

One of the strengths of hill-climbing methods in search and optimisation is that they are generally easy to implement algorithms. 
Question 3 Answer
True
False
Feedback
The correct answer is 'True'.
Question 4
Partially correct
Mark 1.00 out of 3.00
Flag question
Question text

A heuristic processes a given candidate solution and generates an improved solution or returns the same solution, while a   heuristic processes a given candidate solution and generates a solution that is not guaranteed to be better than the input. All such heuristics are .
Feedback
Your answer is partially correct.
You have correctly selected 1.
The correct answer is:

A [hill‑climbing] heuristic processes a given candidate solution and generates an improved solution or returns the same solution, while a  [mutational] heuristic processes a given candidate solution and generates a solution that is not guaranteed to be better than the input. All such heuristics are [perturbative].
Question 5
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Applying the bit-flip operator randomly for once to the candidate solution of "0101010", which of the following new candidate solutions could be produced?
Question 5 Select one or more:
a.

0101000
b.

1111010
c.

1101010
d.

0100000
Feedback
Your answer is correct.
The correct answers are: 1101010, 0101000
Question 6
Partially correct
Mark 0.50 out of 1.00
Flag question
Question text

After applying the adjacent pairwise interchange operator three times at random to the candidate solution of "1-3-2-5-4-7-6", which of the following new candidate solutions could be produced?
Question 6 Select one or more:
a.

1-7-4-5-2-3-6
b.

6-7-4-5-2-3-1
c.

1-3-2-5-4-7-6
d.

1-3-2-5-7-4-6
Feedback
Your answer is partially correct.
You have correctly selected 1.

I should have defined how adjacent pairwise interchange operates, or simply the adjacency. The boundary cases matter. So, normally adjacent swap of ith item swaps the ith and (i+1)th item. Indexing all N items in the permutation from 0 to N-1, if N-1 is selected, the question is how the swap will happen. Two approaches could be implemented which requires explanation/clarification; do nothing (then 1-3-2-5-7-4-6 and 1-3-2-5-4-7-6 can both be correct), or  swap 0th and N-1th items (then only 1-3-2-5-7-4-6 is correct) assuming that’s how you define adjacency.
The correct answers are: 1-3-2-5-7-4-6, 1-3-2-5-4-7-6
Question 7
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Assume that Davis's Bit Hill Climbing and Steepest Descent Hill Climbing algorithms are run for 10 minutes to solve a MAX-SAT problem instance resulting in the average objective values of 12.4 and 3.8, respectively, over 30 runs/trials.
 
Which algorithm would perform the best for solving MAX-SAT problems assuming a minimisation problem formulation?

Question 7 Select one:
a.

Davis's Bit Hill Climbing
b.

Steepest Descent Hill Climbing
c.

Both algorithms would perform the same
d.

It is not possible to determine
Feedback

Your answer is correct.
The correct answer is: It is not possible to determine
Question 8
Incorrect
Mark 0.00 out of 1.00
Flag question
Question text

Assume that Davis's Bit Hill Climbing, First Improvement Hill Climbing and Steepest Descent Hill Climbing algorithms are applied to a MAX-SAT problem instance resulting in average objective values of 12.4, 34.3 and 25.7, respectively, over 30 runs.

Which algorithm performs the best based on the average objective value on this problem instance?
Question 8 Select one:
a.

Assuming that the problem is formulated as a maximisation problem, then First Improvement Hill Climbing
b.

First Improvement Hill Climbing
c.

Assuming that the problem is formulated as a minimisation problem, then Steepest Descent Hill Climbing
d.

Davis's Bit Hill Climbing
Feedback
Your answer is incorrect.
The correct answer is: Assuming that the problem is formulated as a maximisation problem, then First Improvement Hill Climbing


## week 3: metaheuristics
Question 1
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Which of the algorithms below is a local search metaheuristic?
Question 1 Select one:
a.

Iterated Local Search
b.

Greedy Randomized Adaptive Search Procedure
c.

Ant colony optimisation
d.

Particle Swarm Optimisation
Feedback
Your answer is correct.
The correct answer is: Iterated Local Search
Question 2
Correct
Mark 1.00 out of 1.00
Flag question
Question text

The pseudocode below is provided for Iterated Local Search solving a minimisation problem. Which line of the code is problematic, and why?

1 s*= GenerateInitialSolution()
2 Repeat
3    s' = applyLocalSearch(s*) // apply hill climbing 
4    s' = perturbSolution(s' ) // make a random move
5    accept = moveAcceptance(s*, s', memory);  // remember best solution found so far
6    if (f(s') < f(s*)) s* = s'; // else reject new solution s'
7 Until (termination conditions are satisfied) 
8 return s* 


Question 2 Select one:
a.

line #6, because improving and equal moves acceptance method must have been used instead.
b.

line #2, because application of local search is missing before the main loop.
c.

line #5, because 'memory' is useless.
d.

line #4, because perturbation must have been performed before local search.
Feedback
Your answer is correct.
The correct answer is: line #4, because perturbation must have been performed before local search.
Question 3
Correct
Mark 1.50 out of 1.50
Flag question
Question text

Assume that a generic Iterated Local Search (ILS) algorithm is implemented embedding the Improving Only (IO) acceptance method, Davis's Bit Hill Climbing (DBHC) for local search controlled by the depth of search (DOS) parameter, random bit-flip for perturbation controlled by the intensity of mutation (IOM) parameter. These parameters take integer values in the range [0, 10] that correlate to the number of times of calls to DBHC and bit-flip operator before moving on to the next step in the algorithm. For example, DOS=0 (i.e., DOS is set to 0) indicates that DBHC is not applied, or  DOS=3 (i.e., DOS is set to 3) indicates that DBHC is applied to a solution for 3 passes over that solution, while IOM=3 (i.e., IOM is set to 3) indicates that 3 bit-flips are applied to the incumbent solution.  [This text is common for all the following questions ]

Is the following statement TRUE or FALSE?

If IOM=10 (IOM is set to 10) and DOS=0 (DOS is set to 0), ILS becomes a Random Mutation Hill Climbing algorithm.
Question 3 Select one:

TRUE

FALSE
Feedback
Your answer is correct.
The correct answer is: TRUE
Question 4
Correct
Mark 1.50 out of 1.50
Flag question
Question text

Assume that a generic Iterated Local Search (ILS) algorithm is implemented embedding the Improving Only (IO) acceptance method, Davis's Bit Hill Climbing (DBHC) for local search controlled by the depth of search (DOS) parameter, random bit-flip for perturbation controlled by the intensity of mutation (IOM) parameter. These parameters take integer values in the range [0, 10] that correlate to the number of times of calls to DBHC and bit-flip operator before moving on to the next step in the algorithm. For example, DOS=0 (i.e., DOS is set to 0) indicates that DBHC is not applied, or  DOS=3 (i.e., DOS is set to 3) indicates that DBHC is applied to a solution for 3 passes over that solution, while IOM=3 (i.e., IOM is set to 3) indicates that 3 bit-flips are applied to the incumbent solution.  

Is the following statement TRUE or FALSE?

If  IOM=0 (IOM is set to 0) and DOS=10 (DOS is set to 10), ILS is likely to get stuck at a local optimum.
Question 4 Select one:

TRUE

FALSE
Feedback
Your answer is correct.
The correct answer is: TRUE
Question 5
Correct
Mark 2.00 out of 2.00
Flag question
Question text

Assume that a generic Iterated Local Search (ILS) algorithm is implemented embedding the Improving Only (IO) acceptance method, Davis's Bit Hill Climbing (DBHC) for local search controlled by the depth of search (DOS) parameter, random bit-flip for perturbation controlled by the intensity of mutation (IOM) parameter. These parameters take integer values in the range [0, 10] that correlate to the number of times of calls to DBHC and bit-flip operator before moving on to the next step in the algorithm. For example, DOS=0 (i.e., DOS is set to 0) indicates that DBHC is not applied, or  DOS=3 (i.e., DOS is set to 3) indicates that DBHC is applied to a solution for 3 passes over that solution, while IOM=3 (i.e., IOM is set to 3) indicates that 3 bit-flips are applied to the incumbent solution. 

Which one of the following options would convert the ILS algorithm into a Random Walk algorithm (randomly sampling the search landscape)?
Question 5 Select one:
a.

By setting IOM=2 and DOS=0, and changing IO to the All Moves acceptance method
b.

By setting IOM=0 and DOS=2, and keeping the move acceptance method
c.

By setting IOM=0 and DOS=0, and changing IO to All Moves acceptance method
d.

By setting IOM=2 and DOS=2, and keeping the move acceptance method
Feedback
Your answer is correct.
The correct answer is: By setting IOM=2 and DOS=0, and changing IO to the All Moves acceptance method
Question 6
Incorrect
Mark 0.00 out of 1.00
Flag question
Question text

Given n jobs to be processed by a single machine, each job (j) with a due date (dj) (i.e. hard deadline), processing time (pj), and a weight (wj), which one of the following scheduling notations indicate the problem of finding the optimal sequencing of jobs producing the earliest time for the last job exiting the system (assuming that the time starts at t=0).

Question 6 Select one:
a.

1 | dj | ΣwjLj
b.

1 | dj | ΣCj
c.

1 | dj | Cmax
d.

1 | dj | ΣTj
e.

1 | dj | ΣwjTj

Feedback
Your answer is incorrect.
The correct answer is: 1 | dj | Cmax
Question 7
Correct
Mark 2.00 out of 2.00
Flag question
Question text


Given the box-plots for 3 algorithms A, B and C  based on the objective values obtained from 100 trials while solving an instance of a minimisation problem (and no other information), which of the following statement(s) about the search algorithms is definitely true?


Question 7 Select one or more:
a.

Algorithm A is an Iterated Local Search algorithm.
b.

Algorithm C is a Tabu Search algorithm.
c.

Algorithm B is either an Iterated Local Search or Tabu Search algorithm.
d.
Algorithm C is the worst performing algorithm among the three for this instance considering the objective value of the median solution obtained in 100 trials.
Feedback
Your answer is correct.
The correct answer is: Algorithm C is the worst performing algorithm among the three for this instance considering the objective value of the median solution obtained in 100 trials.


## week 4: move acceptance and metaheuristics
Question 1
Correct
Mark 1.00 out of 1.00
Flag question
Question text

All parameters of the local search metaheuristics,  Simulated Annealing with Lundy Mees cooling schedule and  Iterated Local Search using Steepest Descent for hill climbing and random bit flip for perturbation are both tuned using the Taguchi method for solving the MAX-SAT problem. 

Which one of the following statements on the performance comparison of Simulated Annealing and Iterated Local Search is more likely to be correct? 
Question 1 Select one:
a.

Both metaheuristics would perform the same for MAX-SAT
b.

Simulated Annealing would perform better than Iterated Local Search for MAX-SAT
c.

No performance comparison can be done based on the given information.
d.

Iterated Local Search would perform better than Simulated Annealing for MAX-SAT
Feedback
Your answer is correct.
The correct answer is: No performance comparison can be done based on the given information.
Question 2
Correct
Mark 2.00 out of 2.00
Flag question
Question text
Parameter techniques are used for detecting the best initial parameter settings of an optimisation algorithm in an offline manner, while parameter techniques operate during the search process in an online manner.
Feedback
Your answer is correct.
The correct answer is: Parameter [tuning] techniques are used for detecting the best initial parameter settings of an optimisation algorithm in an offline manner, while parameter [control] techniques operate during the search process in an online manner.
Question 3
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Is the following statement TRUE or FALSE?

Simulated Annealing is a non-stochastic threshold move acceptance method.
Question 3 Select one:
a.

TRUE
b.

FALSE
Feedback
Your answer is correct.
The correct answer is: FALSE
Question 4
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Is the following statement TRUE or FALSE?

The geometric cooling schedule in Simulated Annealing is used to cool the temperature parameter T used within the Boltzmann probability equation using the formula T =  α T. 
Question 4 Select one:
a.

TRUE
b.

FALSE
Feedback
Your answer is correct.
The correct answer is: TRUE
Question 5
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Is the following statement TRUE or FALSE?

The parameters of the Simulated Annealing metaheuristic using the Lundy and Mees cooling schedule include only β and initial temperature (T0).
Question 5 Select one:
a.

TRUE
b.

FALSE
Feedback
Your answer is correct.
The correct answer is: FALSE
Question 6
Partially correct
Mark 1.00 out of 3.00
Flag question
Question text

A move acceptance method with no parameters is a method. 

Great deluge is a move acceptance method. 

You have merged great deluge and extended great deluge creating a group decision-making move acceptance method that is . This method accepts a new solution if the great deluge and extended great deluge both return true (accept the new solution) at a given step, otherwise, the new solution is rejected.  


Feedback
Your answer is partially correct.
You have correctly selected 1.
The correct answer is:

A move acceptance method with no parameters is a [static] method. 

Great deluge is a [dynamic] move acceptance method. 

You have merged great deluge and extended great deluge creating a group decision-making move acceptance method that is [adaptive]. This method accepts a new solution if the great deluge and extended great deluge both return true (accept the new solution) at a given step, otherwise, the new solution is rejected.  


Question 7
Correct
Mark 1.00 out of 1.00
Flag question
Question text

What happens as the temperature parameter T used within the Boltzmann probability equation in Simulated Annealing decreases?
Question 7 Select one:
a.

The probability of accepting worsening solutions increases
b.

The probability of accepting worsening solutions becomes higher than the probability of accepting improving solutions
c.

The probability of accepting worsening solutions does not change
d.

The probability of accepting worsening solutions decreases
Feedback
Your answer is correct.
The correct answer is: The probability of accepting worsening solutions decreases


## week 5: evolutionary algorithms 1
Grade 	9.25 out of 10.00 (92.5%)
Question 1
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Which one of the following is a reason why benchmark functions are used for performance comparison of search/optimisation algorithms?
Question 1 Select one:
a.

The benchmark functions are difficult to implement
b.

The global optimum is usually known for the benchmark functions
c.

The benchmark functions always allow delta/incremental evaluation
d.

The benchmark functions have similar characteristics
Feedback
Your answer is correct.
The correct answer is: The global optimum is usually known for the benchmark functions
Question 2
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Is the following statement TRUE or FALSE?

Hill climbing/local search cannot be applied to parents and offpring, before crossover and after mutation, respectively, in a memetic algorithm.
Question 2 Select one:
a.

TRUE
b.

FALSE
Feedback
Your answer is correct.
The correct answer is: FALSE
Question 3
Correct
Mark 1.00 out of 1.00
Flag question
Question text

A generic trans-generational memetic algorithm is applied to an instance of the MAX-SAT problem. Assume that binary encoding for the representation, generic one-point crossover, mutation, Davis's bit hill-climbing, elitist replacement and tournament parent selection methods are utilised while the population size is fixed as 5. The tournament selection operator allows the same individual to be selected as parents that will undergo crossover.

What would happen if the tour size for the parent selection is set to 5?

Choose from the following answers which apply.
Question 3 Select one or more:
a.

The second-ranking individual in the population never has a chance to be selected for crossover
b.

The best individual with the best fitness in the population will always be selected for crossover
c.

The newly generated two solutions (children) produced after crossover could be the same
d.

No new solutions will be introduced as the search progresses from one generation to another
Feedback

Your answer is correct.
The correct answers are: The best individual with the best fitness in the population will always be selected for crossover, The newly generated two solutions (children) produced after crossover could be the same
Question 4
Correct
Mark 1.00 out of 1.00
Flag question
Question text

A generic memetic algorithm is applied to an instance of the MAX-SAT problem. What is likely to happen at the end of the search process if all individuals in the population of size 20 get replaced with the newly produced 20 offspring at every generation?
Question 4 Select one:
a.

The best solution might be lost.
b.

The worst solution when achieved persists until to the end.
c.

The optimal/perfect solution can be found much faster.
d.

The best solution when achieved persists until to the end.
Feedback
Your answer is correct.
The correct answer is: The best solution might be lost.
Question 5
Correct
Mark 2.00 out of 2.00
Flag question
Question text

Genetic Algorithms simulate natural evolution based on the concept of  via processes of selection, , and reproduction. In GA, a collection of individuals currently “alive”, called  is evolved from one  to another depending on the fitness of individuals in a given environment.


Feedback
Your answer is correct.
The correct answer is:

Genetic Algorithms simulate natural evolution based on the concept of [survival of the fittest] via processes of selection, [mutation], and reproduction. In GA, a collection of individuals currently “alive”, called [population] is evolved from one [generation] to another depending on the fitness of individuals in a given environment.


Question 6
Partially correct
Mark 0.25 out of 1.00
Flag question
Question text
Choose the benchmark functions below for which delta/incremental evaluation can be utilised.
Question 6 Select one or more:
a.


b.


c.


d.


Feedback
Your answer is partially correct.
You have correctly selected 1.
The correct answers are: , , ,
Question 7
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Which of the following evolutionary algorithms is used for evolving computer programs? 
Question 7 Select one:
a.

Genetic Algorithms
b.

Evolution Strategies
c.

Evolutionary Programming
d.

Genetic Programming
Feedback
Your answer is correct.
The correct answer is: Genetic Programming
Question 8
Correct
Mark 1.00 out of 1.00
Flag question
Question text
Is the following statement TRUE or FALSE?

Memetic Algorithms are iterative single-point based search methods.
Question 8 Select one:
a.

TRUE
b.

FALSE
Feedback
Your answer is correct.
The correct answer is: FALSE
Question 9
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Is the following statement TRUE or FALSE?

A memetic algorithm extends a genetic algorithm using hill climbing/local search.
Question 9 Select one:
a.

TRUE
b.

FALSE
Feedback
Your answer is correct.
The correct answer is: TRUE


## week 6: evolutionary algorithms 2/Multi-meme Memetic Algorithms

Question 1
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Which one of the following is a reason why benchmark functions are used for performance comparison of search/optimisation algorithms?
Question 1 Select one:
a.

The benchmark functions are difficult to implement
b.

The global optimum is usually known for the benchmark functions
c.

The benchmark functions have similar characteristics
d.

The benchmark functions always allow delta/incremental evaluation
Feedback
Your answer is correct.
The correct answer is: The global optimum is usually known for the benchmark functions
Question 2
Correct
Mark 1.00 out of 1.00
Flag question
Question text

There is no difference between a self-adaptive multi-meme memetic algorithm and a memetic algorithm with adaptive control.
Question 2 Select one:
a.

TRUE
b.

FALSE
Feedback
Your answer is correct.
The correct answer is: FALSE
Question 3
Correct
Mark 1.00 out of 1.00
Flag question
Question text

A multi-meme memetic algorithm is based on a framework where both genetic and memetic materials are co-evolved.
Question 3 Select one:
a.

TRUE
b.

FALSE
Feedback
Your answer is correct.
The correct answer is: TRUE
Question 4
Incorrect
Mark 0.00 out of 2.00
Flag question
Question text
Assume that you are solving MAX-SAT using a generic multi-meme memetic algorithm and there is only one meme controlling the choice of the hill-climbing operator with two options, where 0 indicates Davis's Bit Hill Climbing and 1 indicates Steepest Gradient Hill Climbing. The meme values are randomly initialised and the simple inheritance mechanism is used for transmitting the memes from the parent individuals to offspring. A meme gets mutated to a different value based on the innovation rate.

If the population size is fixed as 200 and the innovation rate is set to 0.0, which of the following observations would be highly likely?


Question 4 Select one:
a.

About half of the individuals in the initial population would have the value of 0 for the meme 
b.

At an intermediate stage during the search process, the number of 1s could exceed the number of 0s in the population for the meme
c.

At the end of the search process, about half of the individuals in the final population would have the value of 1 for the meme 
d.

None of the individuals would have a value of 1 for the meme at any generation
Feedback
Your answer is incorrect.
The correct answer is: About half of the individuals in the initial population would have the value of 0 for the meme 
Question 5
Partially correct
Mark 1.00 out of 2.00
Flag question
Question text

Assume that you are solving MAX-SAT using a generic multi-meme memetic algorithm and there is only one meme controlling the choice of the hill-climbing operator with two options, where 0 indicates Davis's Bit Hill Climbing and 1 indicates Steepest Gradient Hill Climbing. The meme values are randomly initialised and the simple inheritance mechanism is used for transmitting the memes from the parent individuals to offspring. A meme gets mutated to a different value based on the innovation rate.

If the population size is fixed as 200 and the innovation rate is set to 1.0, which of the following observations would be highly likely?
Question 5 Select one or more:
a.

At the end of the search process, about half of the individuals in the final population would have the value of 0 for the meme 
b.

At an intermediate stage during the search process, the number of 1s would never exceed the number of 0s in the population for the meme
c.

None of the individuals would have the value of 1 for the meme at any generation
d.

About half of the individuals in the initial population would have the value of 0 for the meme 
Feedback
Your answer is partially correct.
You have correctly selected 1.
The correct answers are: About half of the individuals in the initial population would have the value of 0 for the meme , At the end of the search process, about half of the individuals in the final population would have the value of 0 for the meme 
Question 6
Correct
Mark 2.00 out of 2.00
Flag question
Question text

Assume that you are solving MAX-SAT using a generic multi-meme memetic algorithm and there is only one meme controlling the choice of the hill-climbing operator with two options, where 0 indicates Davis's Bit Hill Climbing and 1 indicates Steepest Gradient Hill Climbing. The meme values are randomly initialised and the simple inheritance mechanism is used for transmitting the memes from the parent individuals to offspring. A meme gets mutated to a different value based on the innovation rate.

If the population size is fixed as 200 and the innovation rate is set to 0.2, which of the following observations would be highly likely?
Question 6 Select one:
a.

At an intermediate stage during the search process, the number of 0s could exceed the number of 1s in the population for the meme
b.

About half of the individuals in the initial population would have the value of 0 for the meme 
c.

None of the individuals would have the value of 1 for the meme at any generation
d.

At the end of the search process, about half of the individuals in the final population would have the value of 1 for the meme 
Feedback
Your answer is correct.
The correct answer is: About half of the individuals in the initial population would have the value of 0 for the meme 
Question 7
Correct
Mark 2.00 out of 2.00
Flag question
Question text

Assume that a multi-meme memetic algorithm is run for 50 trials on the problem instance Inst with an innovation rate of 0.2 based on the memplex of p#o#, which identifies the choice of probability (p) of applying the operator indicated by (o). The meme options are p={0: 0.005, 1: 0.01, 2: 0.02, 3: 0.03, 4:0.5, 5:0.9} and o={0:randomSwap, 1:insertion, 2:randomReversal, 3:adjacentSwap}. Given the mean evolutionary activity plot above, which of the following conclusions can be driven about the search behaviour of the multi-meme algorithm?


Question 7 Select one or more:
a.

The memetic algorithm using the operator randomReversal with the probability of 0.01 can outperform this multi-meme memetic algorithm on Inst.
b.

The number the meme randomReversal with the probability of 0.03 surpasses the others in the population as the search progresses on average.
c.

Some of the memes are rarely used during the search process.
d.

The innovation rate should be increased to improve the performance of the multi-meme memetic algorithm.
Feedback
Your answer is correct.
The correct answers are: The number the meme randomReversal with the probability of 0.03 surpasses the others in the population as the search progresses on average., Some of the memes are rarely used during the search process.


## week 7: hyper-heuristics 1

Grade 	7.00 out of 10.00 (70%)
Question 1
Correct
Mark 2.00 out of 2.00
Flag question
Question text
Select the option(s) below indicating the characteristic(s) of a hyper-heuristic.
Question 1 Select one or more:
a.

A hyper-heuristic targets to exploit the strengths and avoid the weaknesses of the low level operators.
b.

A hyper-heuristic is a parameterless search method.
c.

A hyper-heuristic is an atomic move operator.
d.

A hyper-heuristic operates over the search space of low level heuristics.
e.

A hyper-heuristic does not require a candidate solution representation.
Feedback
Your answer is correct.
The correct answers are: A hyper-heuristic operates over the search space of low level heuristics., A hyper-heuristic targets to exploit the strengths and avoid the weaknesses of the low level operators.
Question 2
Correct
Mark 2.00 out of 2.00
Flag question
Question text

The hyper-heuristics can be broadly categorised as hyper-heuristics that automatically construct new heuristics from given components, while hyper-heuristics that choose and control a predefined set of heuristics.   learning hyper-heuristics are usually trained on a set of selected instances and then generalise to unseen instances, while learning hyper-heuristics receive feedback during the search process while solving a given instance of a problem.
Feedback
Your answer is correct.
The correct answer is:

The hyper-heuristics can be broadly categorised as [Generation] hyper-heuristics that automatically construct new heuristics from given components, while [Selection] hyper-heuristics that choose and control a predefined set of heuristics. [Offline]  learning hyper-heuristics are usually trained on a set of selected instances and then generalise to unseen instances, while [Online] learning hyper-heuristics receive feedback during the search process while solving a given instance of a problem.
Question 3
Incorrect
Mark 0.00 out of 1.00
Flag question
Question text

Assume that you have applied a hyper-heuristic for 50 trials, managing a set of 9 low-level heuristics from LLH1 to LLH9, to a set of Vehicle Routing Problem instances denoted as VRP and obtained the following PieChart reporting the share of improvements produced by each low-level heuristic overall.

PieChart

Is the following statement TRUE or FALSE?

The hyper-heuristic might be a generation hyper-heuristic.


Question 3 Answer
True
False
Feedback
The correct answer is 'True'.
Question 4
Correct
Mark 1.00 out of 1.00
Flag question
Question text

Assume that you have applied a hyper-heuristic for 50 trials, managing a set of 9 low-level heuristics from LLH1 to LLH9, to a set of Vehicle Routing Problem instances denoted as VRP and obtained the following PieChart reporting the share of improvements produced by each low-level heuristic overall.

PieChart

Is the following statement TRUE or FALSE?

The performance of this hyper-heuristic would definitely be the same if the experiments are repeated removing the low-level heuristics LLH1, LLH5, and LLH6 from the set.


Question 4 Answer
True
False
Feedback
The correct answer is 'False'.
Question 5
Incorrect
Mark 0.00 out of 1.00
Flag question
Question text

Assume that you have applied a hyper-heuristic for 50 trials, managing a set of 9 low-level heuristics from LLH1 to LLH9, to a set of Vehicle Routing Problem instances denoted as VRP and obtained the following PieChart reporting the share of improvements produced by each low-level heuristic overall.

PieChart

Is the following statement TRUE or FALSE?

LLH9 generates the lowest number of improvements overall.


Question 5 Answer
True
False
Feedback
The correct answer is 'False'.
Question 6
Correct
Mark 1.00 out of 1.00
Flag question
Question text

The majority of the selection hyper-heuristics managing perturbative low-level heuristics usually contain
Blank 1 Question 6
Feedback
Your answer is correct.
The correct answer is:

The majority of the selection hyper-heuristics managing perturbative low-level heuristics usually contain [heuristic selection and move acceptance methods]
Question 7
Partially correct
Mark 1.00 out of 2.00
Flag question
Question text

The following table provides Formula 1 scores of the top nine hyper-heuristics among CHeSC finalists and Robinhood hyper-heuristic (RHH) across six problem domains, where TOT denotes the total score. 

Table of results

Which of the following conclusion(s) below can be driven based on this table?


Question 7 Select one or more:
a.

AdapHH is the best hyper-heuristic ranking the top in all domains.
b.

Robinhood hyper-heuristic delivers the best performance for the BP and VRP domains when compared to its performance on the other domains.
c.

Robinhood hyper-heuristic is the worst performing method among the other hyper-heuristics for TSP.
d.

Robinhood hyper-heuristic has a better cross-domain performance than six of the CHeSC finalists.
Feedback
Your answer is partially correct.
You have correctly selected 1.
The correct answers are: Robinhood hyper-heuristic has a better cross-domain performance than six of the CHeSC finalists., Robinhood hyper-heuristic delivers the best performance for the BP and VRP domains when compared to its performance on the other domains.

## week 8: hyper-heuristics 2
What is the minimum number of colours that can be used to colour the vertices of the following strongly connected graph such that no two adjacent vertices share the same colour?


Question 1 Select one:
a.

6
b.

5
c.

4
d.

3
e.

1
Feedback
Your answer is correct.
The correct answer is: 6
Question 2
Correct
Mark 1.00 out of 1.00
Flag question
Question text

The Largest Degree first graph colouring heuristic can obtain the optimal colouring for any given graph.
Question 2 Answer
True
False
Feedback
The correct answer is 'False'.
Question 3
Partially correct
Mark 2.00 out of 3.00
Flag question
Question text

Which of the following statements about Genetic Programming (GP) are true?
Question 3 Select one or more:
a.

GP provides a method for automatically creating a working computer program from a high-level problem statement of the problem.
b.

GP is a single-point based search method invoked multiple times.
c.

GP iteratively transforms a population of computer programs into a new generation of programs via evolutionary process.
d.

GP uses parse trees representing computer programs
Feedback
Your answer is partially correct.
You have correctly selected 2.
The correct answers are: GP uses parse trees representing computer programs, GP iteratively transforms a population of computer programs into a new generation of programs via evolutionary process., GP provides a method for automatically creating a working computer program from a high-level problem statement of the problem.
Question 4
Incorrect
Mark 0.00 out of 2.00
Flag question
Question text

Which one of the following is the best method to cope with division by zero in a program being evolved by a genetic programming approach?
Question 4 Select one:
a.

To return the maximum long integer value after division by 0.
b.

To catch the error and return with an error message.
c.

To allow the division.
d.

To use a protected division by zero which returns 1 if a division by zero is attempted.
Feedback
Your answer is incorrect.
The correct answer is: To use a protected division by zero which returns 1 if a division by zero is attempted.
Question 5
Correct
Mark 3.00 out of 3.00
Flag question
Question text

Which algorithmic components listed below should be designed if Genetic Programming algorithm will be used for solving a given problem? 

Tick all that applies.
Question 5 Select one or more:
a.

Fitness measure that is used to evaluate a given evolved program
b.

Representation
c.

Termination criteria
d.

Terminals and non-terminals
Feedback
Your answer is correct.
The correct answers are: Terminals and non-terminals, Fitness measure that is used to evaluate a given evolved program, Termination criteria