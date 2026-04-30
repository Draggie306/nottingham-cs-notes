

- Path: sequence of edges. In a directed graph, edges should go in the same direction.
- Connected: there is a path (sequence of edges) between any two nodes.
- Strongly connected: there is a path from any other node in a directed graph.

- Spanning tree: a tree that connects all vertices, only using the edges present in the original graph. **Any subset of edges that form a tree and still connect all nodes.**

> A graph may still work if a edge is removed. A tree will always fall into two subtrees if an edge is cut.

![](../../../Images/Pasted%20image%2020260430143603.png)


A spanning sub-graph is a subset of edges that span the graph but is not minimal - there may be a cycle.

![](../../../Images/Pasted%20image%2020260430143554.png)



A minimum spanning tree (MST) is the spanning tree that has the smallest weight of edges for any possible spanning tree, from a connected, undirected, weighted graph.

- Minimal: the local property - locally optimal with a small set of moves.
- Minimum: the global minimum. This is what is used for the MST.


MSTs are used in gas and water pipelines, fibre optic networks to reach all houses in a new estate while minimising cost of construction. Edges are pipes, nodes are supply/delivery locations, and it results in the cheapest system that meets the supply requirements.

A minimum spanning sub-graph is always a tree, as having a cycle means that an edge can always be removed. **It is not to be confused with a (minimum) path. This imposes too many constraints.** 

### Prim's Algorithm
To find and know the tree is a MST, it is simple to work out. Instead of brute forcing, a greedy method instead can always give a minimum solution.

1. Start from any node.
2. Add an edge until a spanning tree is reached.
	1. The new node to add is always an edge that has the minimum weight.
	2. The current tree is extended to the new minimum node.


Let tree-so-far = TSF, with vertex { M }
Until all verticies are in TSFm add the shortest edge from all vertices in TSF, to a vertex outside TSF.




