Warren Jackson's advice:

Do the labs, online documentations, have a look at documentations of hyflex, https://people.cs.nott.ac.uk/pszwj1/chesc2011/javadoc/AbstractClasses/HyperHeuristic.html


 %%> Coursework: delta evaluation should be used for high marks!%%


### heuristics/hyperheuristics ideas


- "Opposites Attract Elitism": during population selection, have single-point crossover selected between "opposites" in the population $p$. For example, from $n$ samples, pick $p[0]$ and $p[n-1]$ to be paired and crossed over stochastically. Continue this until $p[\frac{n}2]$ is the first element. 