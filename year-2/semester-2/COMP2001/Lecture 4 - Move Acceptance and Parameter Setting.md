
When deploying any algorithm to a deployment, we have to determine what parameter set we use, depending on the 

## Move Acceptance Methods

> Motivation: how can we decide to accept/reject candidate solutions to move into a better place into the landscape, so that the input operator results in better solutions?

1. Given a starting solution/init procedure
2. Repeat: 
	1. Make a move, based on one or more (meta)heuristics that takes the current solution (and memory), giving a candidate solution. 
	2. Given current, s\*, and the new, c', and some memory, should we accept it (becoming the current solution) OR discard it and use another move? 
	3. Repeat

- Using a value of `p` of 1, every time a candidate solution worse than the current, we accept it anyway.
- With a `p` of 0, we only accept better values.
- With a `p` of 0.05, we accept 5% of worse moves, resulting in a worse result than 0
- With a `p` of 0.01, it results in better result than 0.05, but still worse than 0.
- With `a` p of 0.00001, it is better than 0 (as the search landscape is allowed to be traversed more?)

### More move acceptance methods

### Algorithmic parameter settings

Many parameters can be used: the way they are set/controlled varies based on the categorisations:
- Static methods - behave the same during the search. Given p = x, then its behaviour will not change from bein p = x at any points
- Dynamic methods - we may want to start with a high value of p, but on each iteration, we may decrement it by a certain amount. We can deterministically say whether it has been accepted/rejected at a given iteration.
- Adaptive - different, based on history and memory, and will try to change the parameters to attempt to move into a different search landscape. 

The nature of the acceptance decision is how values are determined within the move acceptance method. 

> If it has any chance of randomisation, it is categorised as stochastic.

- All Moves acceptance always accepts True.
- Improving or Equals (non-worsening) are examples of static, non-stochastic basic criteria.
- Only Improving means $f(s') < f(s)$

### Late acceptance

It has a list of $L$ previously accepted objective values of previously-seen solutions. We need some way of populating the list of values: 
- initial solution cost
- infinity (randomly walk for $L$ steps)
- zero (force non-worsening moves for L iterations - hill-climb)

Generating a new solution at a random iteration, 


Given the branch settings:
- Accepted = 50
- Candidate = 60

![Pasted image 20260217163304](../../../Images/Pasted%20image%2020260217163304.png)

Here, we initially reject the solution (as we are trying to minimise; 60 is **greater** than 50). When $L$ is 3, we look at the 3rd previous iteration: 



### Non-stochastic Threshold Methods

Threshold values can be any value whatsoever. 




#### Parameter settings

We use epsilon (a small value) added to the candidate solution - to allow some worse value. This is different to naive (with low percentage) - here, we are accepting all worst moves, but only if they reach a certain value.

It is reasonable to assume if we have not achieved a better value, we arestuck, so apply *flex deluge*


### Great Deluge

This is a dynamic, non-stochastic threshold that accepts worst-cost moves, if they are not worse than a "water level" that decreases towards a specific target, over time. It progressively improves until it cannot make any improvement, where it flatlines.

Extended Great Deluge updates the water level and decay rate based on search feedback - allowing it to restart if the search is deemed to be stuck.


### Stochastic methids
These determine neighbourhood move criteria based on a randomised part. 

> None of these limit better-cost moves. They only affect the limits for worsening-case moves. 


#### Parameter settings
- Static methods - use a fixed probability $p$ naively.
- Dynamic methods - adjusting probability over time. 
	- Includes *Simulated Annealing* - decreasing a "temperature" over time
- Adaptive methods - uses some search history and feedback to adapt the search. 
	- Simulated Annealing - if the temp is decreased too fast, we can "reheat" - increasing the chance that worst-cost moves are accepted, to find another search place

### Simulated Annealing

> Analogy: Cooling metal down too fast creates weak crystals. Instead, we can control it with a gradual temperature reduction, creating stronger formations.  Similarly, if temperatures reduce too fast, we get worse results. If we simulate temperature in a specific way, it is more likely to find an optimal solution.

It is a dynamic, stochastic move acceptance method that accepts worst cost moves based on a probability that decreases over time and based on the change rate.


![Pasted image 20260217164757](../../../Images/Pasted%20image%2020260217164757.png)

It accepts all improving moves, whilst non-improving moves are accepted using the Boltzmann probability:  $e ^{(- \frac \Delta T)}$ if the random number is less than the value. $T = \alpha \space T$

A high temperature allows more, worsening moves to be accepted. A low temperature rejects worsening moves, instead only accepting a few minor worsening moves. Decreasing T decreases the chance that a worsening move is accepted. 




### Cooling schedules

- If the temperature is set too high, we allow many more worsening moves to be accepted. 
- If the temperature is too low, worsening moves are rejected, accepting only a few minor worsening moves (getting stuck...)

We generally specifcy an **initial** and **final** temperature, a mechanism/function to decrease it (**linear** cooling), and a number of iterations per temperature setting (only cool after 50 iterations, or cool  a small amount every iteration).
We usually assume the final temperature should be close to 0 - to balance exploration (at the start) and exploitation (at the end, to find the best solution in a small search space). 


#### Types of cooling schedules
There are multiple cooling schedules:
- Linear
	- A fixed amount each iteration.
- Geometric
	- Multiplies the current temperature by a value $\alpha$ close to, but never at, one - typically 0.9 to 0.99 (context-dependent).
- Lundy and Mees
	- More exploitative - reduces much faster at the start. Current iteration divided by 1 + beta\*iteration.

#### Iterations per temperature
- Standard approach: decide whether to accept/reject, then decrease temperature
- Other approaches exist: 
	- reduce $T$ after X iterations
	- reduce $T$ by number of iterations based on search location.
- **Adaptive** approaches: 
	- reduce $T$ over time, if the solution has not improved after X iterations.
	- increase $T$ if the search may appear to be stuck - reset to initial/added 

In a single-stage search method, 


## Parameter Configuration 

### Tuning Methods
These are set offline, before the process starts.
- Arbitrary choice - randomly pick a value in the set of options
- Trial and error - maybe with some intuition
- Sequential tuning - fix parameter settings of all parameters and, one-by-one, try all possible settings of $a$ when $b$ is fixed, then fix $a$ to the best found and try all in $\beta$. 


### Design of Experiments



### Taguchi Orthogonal Arrays
This is a structured statistical (DoE) method to determine the best combination of parameter settings for an objective


