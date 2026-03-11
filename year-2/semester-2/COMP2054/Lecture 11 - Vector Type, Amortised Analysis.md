 
## Resizable arrays
**These are arrays that automatically extend in size and capacity when another entry is added, that would otherwise overrun/run out of space.** This is hidden to the user. Useful for when data is coming in but the amount is unknown ahead of time. 

It creates a new array of a larger size and copies the old elements, called a vector in C++.
### Vector ADT - CDT
It can be used like an array, but wrapped with get/set methods:
- `get(int k)` – gets the element at index k – is `V[k]` 
- `set(int k, Element e)` equivalent of `V[k] = e`


### Size vs capacity
The size if not the same as the capacity. **The capacity is the length of array**, and the **size is the total number of elements stored at the moment**. 

If the size is less than the capacity, we add a new element at the next available space and increment the size.  This is `O(1)`.

If the size = capacity, adding to a normal array would throw an exception. For a vector, we need to create a new array with a larger capacity. 

Any resize is **O(size)** as we need to copy the whole array, plus **O(1)** for the add.

### Picking a new capacity
Picking any `newCap > capacity` is required. We consider two policies:

- incremental: `newCap = capacity + d`, where d $\ge$ 1 is a constant
- doubling = `newCap = capacity * 2`

For the worst case, the cost of add is O(n) due to the resize, so it is not very useful. In practice and generally, we do not always resize: we have many adds with few resizes.

In practice, we often do a long sequence of add operations: reading data from a file, we do not always know how many elements are needed. Therefore, considering the total cost of a long sequence of adding, we compute the average, in that long sequence, the cost per add.

> **T(N) = total cost of the entire sequence of N add operators.** 

The mean cost per operation over the complete sequence is therefore T(N)/N

Amortised: spreading costs over long periods



### Amortised cost of adding
In the incremental strategy, the cost is the capacity + a constant.

- The worst case is O(N) per add. The amortised cost is O(N) - this is bad, as many adds are just O(1). Resizing cost O(N).

In the doubling strategy, the cost is the capacity * 2.

- THe worst case is still O(N) per add. However, the amortised cost is O(1) - which is good, as an add is also O(1). The Big-Oh hides the extra cost of the resize operations. 