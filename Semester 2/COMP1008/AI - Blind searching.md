
### Depth-first search
- We follow/expand one branch before exploring another branch
- The queuing function is changed to add child nodes to the start of the queue


#### DFS evaluation 
- Space complexity
	- The path from the root to the leaf node must always be stored
	- All unexpanded neighbour nodes also must be stored
- Time complexity
	- b^n in the worst case, at the deepest level of the tree
	- *The same or worse compared to breadth-first search*
- Completeness
	- Generally, we cannot guarantee there is a goal state in that branch, risking an infinite branch and never terminating
- Optimality
	- Finds a solution but there may be a better solution at a lower level.

DFS is therefore neither complete nor optimal. It also cannot deal with weights for each link

> ***b*** is a branching factor; ***m*** is the maximum depth.

### Uniform Cost Search
It uses the total cost of the path to the root node *n*, after queuing them based on their values, recursively removing the smallest cost node next. The cost of the node is added 

> ***g*** is the cost so far (so 0 if root node)

**Evaluation**
- Completeness
	- It never misses a solution as it will always go from cheaper nodes to higher cost nodes
- Optimality
	- The cheapest operations will be explored first, so it always explores the cheapest node from the root; there is no better, no “more optimal” solution
	- *Global/local optimal: learn about in year 2!*
- Time complexity
	- The worst case is b^d, although it is often much better as solutions are typically found much earlier! 
- Space complexity
	- Expanding all the nodes are b^d




- BFS is only applied to problems where costs are the asme for each branch/move.
- UCS is applied to all problems, as long as the costs never decrease along the tree. Branches rapidly get cut off 
- DFS is useful when adapted for specific problems like games and trees of limited depth.


### General search algorithm
- Queue - keeping all nodes and connecting ones
- Queuing function - how adding child nodes to the queue

## Heuristic Search
> The 2nd year AI courses all use heuristic searches.


Blind search refers to blindly choosing where to search in the search tree: it is not practical when problems are larger.

In heuristic searches, we use an educated guess to guide the search to most likely node to reach the goal state. It uses domain knowledge (the algorithm is designed specifically for a problem) to be more informed: the learnt **heuristic function** is the educated guess to make judgements about how close a node is to the goal.

### The A* Algorithm
It combines the path cost so far and the estimated heuristic cost to the goal:
f(n) = g(n) + h(n)
- ***g*** is the path cost from the initial state to current state ***n***
- ***h*** is the heuristic cost from the current state to a goal state n
- ***f*** is the estimated cost of the cheapest solution to ***n***

If `h=0`, the A* essentially becomes a UCS search: complete but undirected.
If h is too large, it “dominates” g and becomes greedy and stuck to the ”local optimal” and not global, losing optimality.

The heuristic must be **admissible**. This means it must never overestimate the cost to reach the goal - it cannot be larger than the actual cost. *h(n)* must be a valid lower bound on cost to the goal. An example of this includes, between two cities, the straight line distance.



Search space: all possible solutions of a problem. This can be then replicated as a tree.


### Coursework hints
- Minmax scaler: Scales between 0 and 1: coefficeints comparatively & relatively show the importance. Only then we can tell that e.g. X is much more important than Y, meaning a change in Y will have very small impact on the output. 
- We can drop very low correlation to save time/money/training/compute. If we have only 1 feature, we can immediately do it, if not, it is better to scale. (say this in question 3??)
- How good the MSE is depends: overfitting depends on the context; only once it is applied to different scenarios we can go back and improve the model
- Model can use less input features and less training time if e.g. removing the newspaper whilst retaining
- Not like maths where there is an answer: we have to use domain/human knowledge for machine learning
- Depending on the task, we choose classification/regression, don’t choose a MLPClassifier for regression! 
- Weights are a black box, not easy to display


![[Pasted image 20250320105501.png]]![[Pasted image 20250320105816.png]]



![[Pasted image 20250320105935.png]]
- remove extremities
- choose the best visualisation tool