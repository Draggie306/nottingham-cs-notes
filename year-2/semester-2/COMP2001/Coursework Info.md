Warren Jackson's advice:

Do the labs, online documentations, have a look at documentations of hyflex, https://people.cs.nott.ac.uk/pszwj1/chesc2011/javadoc/AbstractClasses/HyperHeuristic.html


 %%> Coursework: delta evaluation should be used for high marks!%%


### heuristics/hyperheuristics ideas


- Population replacement - "Opposites Attract Elitism": during population selection, have single-point crossover selected between "opposites" in the population $p$. For example, from $n$ samples, pick $p[0]$ and $p[n-1]$ to be paired and crossed over stochastically. Continue this until $p[\frac{n}2]$ is the first element. 
- Heuristic - "Subset Floyd-Warshall": perform Floyd-Warshall algorithm (see ADE Lecture 21) on a subset/series of subsets (potentially useful to cross between large clusters) 
- Hyperheuristic - "Hyper-factor hyperheuristics": have a higher-level hyperheuristic that operates on the search space of lower-level hyperheuristics. For example hyper-squared hyperheuristic operates 2 levels above the domain barrier, and may have a set of hyperheuristics that use different metaheuristics and metaheuristic parameters 