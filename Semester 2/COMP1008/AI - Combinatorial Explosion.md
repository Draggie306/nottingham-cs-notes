
The travelling salesman problem: the number of routes between *n* cities is *n!* - which gets hideously large for even a moderate number of cities. It’s an unsolvable problem

> ***Combinatorial explosion is the feature that the number of solutions for a problem grows exponentially with the size of the problem.***

An example of this includes: chess, Moore’s law, neural networks (weights of neurones must be calculated in relation to each other)


## Search
Many problems can be thought of as a search for the right number. 

A search space is a set of all possible solutions to a problem. The input is the problem itself, and it outputs a solution to the problem.


- Depth of a node: the number of branches from the root to the node
- Depth of a tree: the number of the deepest node in the tree
- Leaves: nodes with no child nodes

To define a search problem with a search tree, we define:
- all possible states of the problem
- the set of all states reachable from the initial state (the search space)
- a set of actions that move one state to another (operations)
- all possible states reachable from a given state (neighbourhood)
- a test to a state to tell if the search reached a state that solves the problem (goal test)
- how much it costs to take a particular path (path cost)

The branching factor is the (average) number of branches of all nodes in a tree — a binary tree will have a a branching factor of 2. 


### General Search Algorithm
> 2nd year AI algorithms: heuristics & more in-depth functions

```
function GeneralSearch(p, QueueingFunction) -> Solution | Faliure
	nodes = MakeQueue(MakeNode(InitialState[p]))
	do
		if nodes is empty:
			return Failure
		node = RemoveFront(nodes)
		if GoalTest[p] on State(Node) == success:
			return Node
		nodes = QueueingFunction(nodes, Expand(node, Operators[p]))
```


Breadth-first search: add all immediately connected nodes into a queue. While the queue is not empty, pop it and add any further connected child nodes from this to the end of the queue. Repeat this while loop until goal found. 


All searching techniques can be evaluated with 4 criteria: 
- Completeness
	- Is it guaranteed to find a solution?
	- If we explore all nodes, we are indeed guaranteed to find one if there is one
- Time complexity
	- Time it takes to find a solution
- Space complexity
	- Memory is required to perform the search
- Optimality
	- Does it find the optimal solution or not?

Big O: defines the worst case of the algorithm’s resource usage.



### Coursework Hints
As long as there is reasoning, it’s okay.
For a particular problem, e.g. filling in data, try a variety of substitutions (such as mean/med/mode) and use the MSE to have the final say.
