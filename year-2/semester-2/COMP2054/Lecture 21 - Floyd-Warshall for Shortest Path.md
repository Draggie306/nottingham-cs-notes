
Dijkstra's algorithm finds the shortest path costs from one given starting node. However, we may need to find the shortest path between all pairs of start and end nodes.





Sometimes, self-edges can't exist; other cases this may not be true (exist and have 0 cost) - as implicit in Dijkstra. We assume the same - cost is 0 to self-node.

### Example
TO read the graph into an adjacency matrix, if the graph is undirected, the matrix is symmetric. Simply read off the graph and add it to the matrix.

![](../../../Images/Pasted%20image%2020260430141647.png)



Outer loop to add all the nodes. Then two nested inner loops to iterate over each node.

> $O( \space | V |^3 \space )$

If the graph is sparse, the number of edges is always less than the number of nodes.

FW works with negative edges, but there must be no possible cycles of total negative weight (as this would result in a very negative path value and meaningless shortest path).

For example, a cycle of n4-n3-n1-n2-n4 where w(n4,n3) is -1, then -1+2+8+1=10 so is allowed.





