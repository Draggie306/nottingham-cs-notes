Trees, Traversals and Array-Based representations

A common task is to traverse all stored data elements.
- "Visiting" a node means to process the contents of it. "Via" merely passes through a node, without looking or processing its stored contents. 



### Pre-order and post-order
A simple forward scan is natural for an array or linked list. For trees, however, there are multiple ways to order nodes. 

For each set of parents/children, we need to make a decision on which are processed first.
- Preorder: parent firth then children.
- Postorder: children then parent afterwards.

The preorder processes the parent first, for each set of parent and children. 
![[../../../Images/Pasted image 20260223131525.png]]
```
Preorder(Node n) { 
	process(n) 
	foreach child c of n 
		Preorder(c)
}
```



For post-order, we recursively process the children first, and the parent last. 
![[../../../Images/Pasted image 20260223131819.png]]

We do not do anything immediately on A or B, but then as C does not have any children (leaf node) we process C first, then going to node D. As D has a child E, we process E second, then go back to D (as E is a leaf node)

```
Postorder(Node n) {
	foreach Child c of n
		Postorder(c)
	process(n) 
}
```


In a binary tree, there are at most 2 children: left and right. Another option is to place the parent in the middle:

### In-order
It is conventional to process the left child (and the left sub-tree), then the parent, and then the right child (and right sub-tree)

![[../../../Images/Pasted image 20260223132153.png]]

```
Inorder(Node n) {
	Inorder(n.left)
	process(n)
	Inorder(n.right) 
}
```

### Arrays vs Linked List

Arrays are fast and compact, with no pointers, resulting in a good memory locality. However, they are difficult to insert/delete into them.

Linked lists are easier to do insertions/deletions, but uses more space and has poor memory locality.

## Tree to array

We could order the tree by levels: shallower nodes are earlier in the tree, with left earlier than right. By labelling the root as 1, the left child will be 2. The left child of this will be 4. This allows integer division by 2 to return to the parent of the current node. 

![[../../../Images/Pasted image 20260223133453.png]]


This allows:
- the root set to 1
- for a given parent node, `p`, at 

- `1` is the root.
- `11` is the right child of the root.
- `1101` is root -> right -> left -> right
- `10001101010` is root -> left \* 3 -> right \* 2 -> left -> right -> left -> right -> left...

A tree of height `h` will need an array size of about $2^h$ - this could be bad ,as it is potentially exponential to the number of tree nodes


Height is a vital property of trees. Running times depend on the number of levels, rather than the size (total nodes) - so many implementations of trees focus on getting the Big-Oh to O(height) versus O(size). 

The maximum height for a given number of nodes $n$  is #tbd 

### Perfect binary tree
The number of nodes M(L) at level L is $2^L$.


> Andrew Parkes quote: "Do the algebra, reorganise some stuff"

The height of a perfect binary tree of size $n$:
- n = $2^{h+1} - 1$, so:
- $2^{h+1}$ = n + 1
- h + 1 = log$_2$ (n+1)
- h = log$_2$(n+1) - 1

Therefore the height of the tree is logarithmic to the size of the tree. The size is exponential to the height of the tree.

- If the tree is perfect, it has height that is logarithmic to the size of the tree: $\Theta(log(n)$.
- If the tree is imperfect, then for the same n it must have at least this height: $\Omega(log(n))$ 
- For a simple "chain" - basically a linked list, where each non-leaf has just one child. This has height of n-1 so trees have height of $O(n)$. 
- Therefore, for a general binary tree with $n$ nodes, the height is $\Omega(log(n))$ and $O(n)$









