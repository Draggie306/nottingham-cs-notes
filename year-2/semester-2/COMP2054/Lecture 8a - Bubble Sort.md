
Properties of sorting algorithms:
- Stability
- Recurrence struture
- Efficiency
- Adaptive?

## Bubble sort
The structure of bubble sort is:
- An outer loop, repeating scans through an array
	- An inner loop, on each scan, compare with the immediate neighbours. Swap to make sure the largest number moves to the end
- After each inner loop, the size of the scan can be decremented, as the end element is the largest 

![[../../../Images/Pasted image 20260226142628.png]]

![[../../../Images/Pasted image 20260226142637.png]]

Bubble sort is **stable**. This means because the order of duplicates is preserved. Here, 8' comes after the 8, and the final result keeps 8' after the 8. 

The comparison function, e.g. `compare(o1,o2) == 0` may mean that objects are equal in terms of the order, but do not have the same contents. **Therefore, being equal may not mean being identical.**

Usually, we do not want e.g. spreadsheets to swap around rows with the same sorting key but with different contents. 

### Complexity and adaptivity
In analysis, we only count usage of comparison operators and swaps. 

- The worst case for bubble sort is that every swap is needed, and so the number of comparisons and swaps are both $\Theta(n^2)$.
- The best case for bubble sort is that the array is already sorted. However, every comparison still needs to be performed, so the overall complexity is $\Theta(n^2)$. 

In practice, we often sort arrays that are already "almost sorted". If a sorting algorithm is much faster when the array is already "almost sorted", we can call it **adaptive**, as it *adapts* well to good input. Bubble sort is not adaptive - it does not take advantage of inputs that are already almost sorted.

### Generalise to simplify

This can be paradoxical - we do more things than it looks like we need. Instead of always sorting the array, we can sort a sub-array defined by first and last indices. 


### Space usage
The auxillary (extra) space bubble sort requires are only the indices `i` and `j` for the loop, and the `tmp` for the element to swap. This is 3 numbers, which do not depend on `n`, so is O(1). This is very good. 