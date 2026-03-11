The ”Data Structures” component to the Algorithms, Data Structures and Efficiency. Maths section - efficiency - is complete.


For almost all data structures, we need to implemenet:
- find (does an element exist)
- insert (add a new element)
- delete (remove at a position or with a value)

### Singly linked list

#### Node
A node in a singly linked list has:
- a pointer/reference to the next nodes
- a store of some data “D”, either directly as a primitive data type or as a pointer to some object. (we usually use integers as the common/default type)

An example is:
```c
Node {
	Node* next;
	int D; // 	can be D* d;
}
```
#### List
A list contains a pointer “head” to the start of a list. Often it will also have a pointer to the tail.

```c
List {
	Node* head;
	Node* tail;
	int   n; // Number of elements.
}
```

In a simple linked list, all data is accessible from the head by “walking” the list. Therefore, all standard operations are implementable.

#### Efficiency
The key question is: what operations are implementable efficiently? There is no direct access to the middle of the list, unlike an array with random (arbitrary) access in O(1) - where arithmetic decides where to go.

To insert 9 at head, we create a new node N containing “9”, point N.head at old head, and the Node.head at N. This is done in O(1) - it never needs to look at the rest of the list.

Similarly to inserting, removing at the head involves: getting the `head.next` from the `head`, pointing the head to the `head.next`, and deleting the old head node.

To insert at the tail, we create a new node `N` containing 1, then point the `tail.next` to `N`, and point `tail` at `N`. This is O(1).

To remove at the tail, we need to point the tail to the previous node, and update the previous node to point to `null`. **There is no way to do this without walking through the list. It is O(n).** 

Having a “pretail” would just result in the same problem; removing the tail once would be fine, but a second time would have to update the “pretail” pointer, requiring a new complete walk.

> Advanced option: “skip lists” - a number of pointers to the middle.

### Doubly linked list

Each node in a doubly-linked list has:
- a pointer to the next node
- **a pointer to the previous node**
- a store of some data, ”D”

```c
Node {
	Node* next;
	Node* prev;
	int   k;    // Or can be D* d
}
```


### Scanning
To find something in the middle, a walk is required which is O(n).

In singly-linked lists:
- removing at the tail is more expensive
- only stores one pointer per node

Doubly-linked lists:
- removal at the tail is O(1)
- stores 2 pointers/node, requiring more storage and increased cache use, and more maintenance

For both, processing and scanning data in the middle will require O(n) as opposed to arrays. 


## (Rooted) Trees

Trees are the basis of many more interesting data structures 

Abstract data types define the data storage system from the user’s perspective. They specify operaitions that must be supported but not how they are implemented. They are in the ”public interface” (in OO) - different from what is internally stored. We dont worry how it is stored - like Linked Lists and Trees. They may have a specification to work in e.g. O(n).

Concrete data types define the behavious from the implementation perspective. They are privately implemented (in OO). They might be inefficient but easy to implement, and then later on switching them out to being efficient but difficult to implement - all without users having to change code. Often, changing from O(n) to O(log n) is enormous.

### Definition
- There is a unique root with no parent - at the top, upside down
- Edges are relations, e.g. parent(A,B)
- Non-root nodes have exactly 1 parent
- Nodes may have any number of children, often ordered left -> right.
- Nodes with no children are called **leaf** nodes, otherwise they are **internal**.

Sub-trees:
- **Descendants** of a node are the children, and any children of those children recursively, reachable by descending
- **Ancestors** of a node are the parent, parent recursive
- A **sub-tree** from a node is all that node together with all its descendents. A root with any number of children, each of the children being a tree.

Depth and height:
- The **depth** is the number of edges to follow from the root to reach it.
- The **height** of a tree is the depth of the deepest node - the length of the longest path (number of jumps between nodes). 
- From the root to any node, there is a unique path. 
- The height is an upper bound on the length of any path from the root to a node

Arity:
- Aritiy of a tree is the number of children any node is allowed to have.
- It is allowed to have fewer children than the arity.

Binary trees:
- Have an arity of 2
- In a binary tree, the children are called left and right. This is not needed for higher arities.
- It is allowed and common for a node to have no left child but to have a right child.

Proper binary trees:
- A proper binary tree is one where all nodes have either 0 or 2 children. It is not allowed to have 1 child.

![Pasted image 20260219144519](../../../Images/Pasted%20image%2020260219144519.png)

Levels:
- A level refers to the set of nodes of a specified depth. 
- The last level is referred to the deepest level

Perfect trees:
- A tree is perfect if every leaf node has the same depth.
- Every level must be full and there cannot be any more nodes.
- The depth of every leaf node is the same as the tree’s height
- These are conceptual trees when analysing merge sort.

![Pasted image 20260219144500](../../../Images/Pasted%20image%2020260219144500.png)

Complete trees:
- A tree is complete if every level (**except the last**) is full, and every node must be as far left as possible

![Pasted image 20260219144450](../../../Images/Pasted%20image%2020260219144450.png)


> To test if it is a tree, cutting an edge falls it into two pieces. A graph will remain whole. **Ask for clarification in lab.**

#### Uses
- File systems - folders/directories can have arbitrary numbers of sub-folders, cannot usually have 2 parents, `/` is the root in Unix
- Syntax - parsed expression trees `(* 3 (+4 5))`
- Data structures - heaps, binary search trees
- Conceptual structures - search trees in min-max are not stored as a tree, but are processed similarly


### Nodes

Linking nodes in a tree is similar to that of a linked list. 

- Nodes have a pointer to the parent
- Nodes also contain data (A, or `*A`)
- An array/list of pointers to children nodes. 








