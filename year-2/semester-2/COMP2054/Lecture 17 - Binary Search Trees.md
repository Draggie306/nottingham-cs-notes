A map allows us to look up items with a key, unlike heaps which only allow access to the minimum.

If the array is unsorted, we are forced to scan all elements - O(n).

Binary search in a sorted array is much faster:
![](../../../Images/Pasted%20image%2020260323130417.png)

The key "trick" is to ignore a whole half of the array on every frame. If the middle says go left, then ignore the right. 

> **The structure itself guarantees we do not need to traverse half of the (sub)tree at every iteration**
### Complexity
![](../../../Images/Pasted%20image%2020260323130649.png)


## Motivations
Binary Search is fast, as the array is halved each iteration, so it is O(log n).

However, arrays suffer from being slow: O(n) to insert an elements, as O(n) elements must be shifted before the element can be added.

A Binary Search Tree attempts to fix this inefficiency whilst keeping O(log n) properties of binary search. The tree needs to know which way to go then looking for an element.


## Definition
A binary search tree is a binary tree, storing key-value entries in the nodes. It satisfies a search tree property:

![](../../../Images/Pasted%20image%2020260323131030.png)

For every node in the Binary Search Tree:
- ALL keys in its left subtree bust be strictly smaller
- ALL keys in its right subtree must be strictly larger


A "binary" search tree just means it must have at most two children, so a BST can just be a long chain with height of O(n). 

## Traversals

In-order traversal:

![](../../../Images/Pasted%20image%2020260323131737.png)



To get the minimum element, we repeatedly take the left child. If there is a left child, it must have a smaller key. The cost is O(height). The maximum value is to always take the right child.


### Inserting
To add a node, we follow the same process for getting a node, and if there is an existing node, it is overwritten. Otherwise, we create a new node in the correct child position. 

### Deletion
Deletion can be more difficult. We firstly find the node to delete, in the same way as getting it. Depending on the cases: 
- If the k-node has no children, the node can be disconnected from the parent. For example, `delete(6)` could set the right child of `5` to be `null`
- If the `k-node` has one child, the entire subtree of node `k` will move up a level to become the direct child of `k`'s parent node.
- If the k-node has 2 children, it is more difficult:
	- Perform an in-order traversal of the tree.
	- The element immediately after the removed node should be moved to where the removed node was.
	- The sub-tree of the node moved then moves up one position. 

## Performance & Rebalancing
All operations are O(h). In the best case, h is O(log n), and the worst case is O(n)

An tree may become "imbalanced", as new nodes can always be added to e.g. the right of a tree. The cost of operations becomes O(n) rather than O(log n).

To rebalance, we extract a sorted list of keys, and insert the median, and recursively insert the left and right subtrees. THis optimally reduces the height to O(log n) - similar to "best partitioning" in quicksort.

### SElf-balancing
A total rebuild of the array requires O(n) which is inefficient versus the required O(log n). 








