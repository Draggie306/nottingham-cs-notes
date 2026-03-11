

Selection sort has the same structure as bubble sort, but the inner loop keeps track of the largest element seen so far and only swaps the selected element at the end if needed. 

```c
sort (int[] A) 
	int n = A.size 
	for (int k = n-1 ; k > 0 ; k-- )
		int max=0; 
		for (int j = 1 ; j <= k ; j++ )
			if ( A[j] > A[max] )
				max=j
		
		// after inner loop
		if ( max < k ) “swap A[k] and A[max]”
```

The first pass scans the first $n-1$ elements, selecting the largest and moves it to the end. 

![Pasted image 20260302130719](../../../Images/Pasted%20image%2020260302130719.png)

As elements may jump over others, it is not stable.

### Complexity
- The number of comparisons is $\Theta(n^2)$ for best and worse - it is not **adaptive**.
- It only has $O(n)$ swaps - so better than bubble sort if swaps are expensive. 


## Insertion sort
In bubble and selection sort, we build an already-sorted subarray at the end.

In insertion sort, it builds this already-sorted subarray at the start. It takes elements, one at a time, from the array, inserting them at the right place in the already-sorted subarray at the beginning. It goes backwards through the subarray at the beginning, swapping elements around until they fit.

![Pasted image 20260302131350](../../../Images/Pasted%20image%2020260302131350.png)

The advantage of insertion sort is that the backwards scan can stop immediately. In bubble and selection sort, it must compare all elements.

It is stable, as we never need to move past identical elements on the backwards scan. 

The worst case is $\Theta(n^2)$ - for an array starting in reverse order.

The best case is O(n), - and $\Theta(n)$ - as the backwards scan will stop immediately with no swapping. As the case gets much better for best cases, it is adaptive.  

## Mergesort

This uses a b algorithm. It divides the problem into or more smaller pieces, and the problem is solved by putting the pieces back together, recursively.

1. Divide the array into 2 smaller arrays.
2. Sort each smaller array.
3. Merge the sorted smaller arrays into one sorted array.


```java
mergeSort(int[] A) { 
	if ( A.size <= 1 ) return; 
	int [] A1, A2
	(A1,A2) = split(A)
	
	// Binary recursion - two calls in the callstack
	mergesort(A1)
	mergesort(A2)
	A = merge(A1,A2) 
}
```

The merge step compares the first elements of A1 and A2 while they are not empty, and moving the smallest into A.

![Pasted image 20260302133031](../../../Images/Pasted%20image%2020260302133031.png)



This can be represented as a tree:
![Pasted image 20260302133639](../../../Images/Pasted%20image%2020260302133639.png)

The height of the tree, given n = $2^k$, we need to divide $k$ times to reach 1. Therefore the height is $log_2(n)$ when $n = 2^k$


### Work analysis
We need to store markers - at each level, there are double the number of markers - $2^0 + 2^1 + 2^2 + ... + 2 ^n$. For 4 levels this is 7 markers needed.

When merging subarrays, we must read each element of the subarrays. With each level, it requires $O(n)$ work per level. 

![Pasted image 20260302134201](../../../Images/Pasted%20image%2020260302134201.png)

Therefore, $O(n)$ work per level + $O (log \space n)$ levels = $O(n\space log\space n)$. This uses all the division and merges combined. 



### Stability and adaptability
Mergesort is stable, as 2 entries that compare as equal has no need to change the order, as we can keep the left-side value every time. 

The naive mergesort is not adaptive, as it goes through the entire process even if the original list is sorted. However, in the middle of the search process, we can consider if there is a subarray that is in the correct order (a "**run**" - of correctly ordered pairs). In standard mergesort, runs of size 1 are created. 

For example, if A1 is already sorted, naive mergesort will split the array and recombine it. Mergesort can be made more adaptive by firstly checking if subarrays are already sorted.  Even better results could be achieved by realising the first 6 elements are sorted, so change the position of the split to be later.

![Pasted image 20260305141240](../../../Images/Pasted%20image%2020260305141240.png)
















