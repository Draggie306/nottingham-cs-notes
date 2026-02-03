Designed to give some background, leading up to Big-O notation. Why the definition is the way it is (a better understanding of it) which leads to other members of the Big-O family. 

Topics:
- Measuring `😂` running times
- Counting primitive operations
- Ambiguities in the counts


## Running time experiments

The running time of an algorithms typically with the input size.

There are already ambiguities in this definition. We usually focus on the worst-case runtime at any given size: this is the most useful and relatively the easiest to compute from the theory.

> The average case is difficult to measure - it could be the mean/mode/median and distribution of input instances. The best-case rarely matters (except for cryptography: the best case should be bad to prevent key cracking)

The general pattern to work it out is:
1. Write a program
2. Run it with inputs of various size and composition
3. Use a system method to get the running time
4. Interpret and analyse the result

> Even though n<sup>2</sup> has an exponent, it is NOT exponential growth. For exponential growth, the size n must be in the exponent.

![](../../../Images/Pasted%20image%2020260129141357.png)

Here, the worst case is roughly linear, the average is something else, and the best base is constant. 

However, we should be more mathematically precise:

### Limits of experiments

Experiments are good but not everything:
- Implementing the algorithm may be difficult/time-consuming;
- Results may not be indicative of the running time on other inputs not included in the experiment - thereby missing the true “worst case”.
- To compare algorithms, the same hardware and software must be used across all tests.


### Limits of theory
- Implementing the theory may be difficult or time-consuming
- Results may not be indicative of the typical running time on inputs encountered. 

## Theoretical analysis

We do not want a detailed implementation: we use a high-level description of the algorithm, instead of an implementation. This description should take into account all inputs, which evaluates the speed of an algorithm independent of the hardware, software or language. It characterises the runtime as a function of the input size *n*.

Pseudocode is a high-level description of an algorithm. It is more structured than English prose, but less detailed than a program. It is the preferred notation for describing algorithm but hides program design issues. 



## Primitive operations

Primitive operations are **basic computations performed by an algorithm**. They are identifiable, language-independent, and their exact definition is not important.

In high level languages, “hidden expenses” may occur that are not written in pseudocode. Therefore we assume the RAM model - closer to assembly language.


These include:
- Assigning a value to a variable
- Comparing two numbers
- Performing an arithmetic operation
- Calling a method
- Returning a value

### Converting time

We need to know the time it takes for the CPU to run an operation. We can approximate this by supposing that the quickest time is q and the slowest time is s. The true worst-case runtime, TW(n), will be sandwiched between two linear functions:

$$q(6n-2) <= TW(n) <= s(6n-2)$$
> The fine details of counting primitive operations would depend on compiler, assembly code, CPU pipelining, etc. 



How many times can I halve something: log2(n)  