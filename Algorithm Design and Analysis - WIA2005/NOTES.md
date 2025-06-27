# L5 : Divide and Conquer

## Merge Sort

> [!NOTE]- Pseudocode Merge Sort
> ```python
> Merge-Sort(A,p,r)
> 	if p < r 
> 		q = [(p + r) / 2]
> 		Merge-Sort(A,p,q)
> 		Merge-Sort(A,q+1,r)
> 		Merge(A,p,q,r)
> 
> Merge(A,p,q,r)
> 	n1 = q - p + 1
> 	n2 = r - q
> 	let L[1 ... n1 + 1] and R[1 ... n2 + 1] new array;
> 	for i = 1 to n1
> 		L[i] = A[p + i - 1]
> 
> 	for j = 1 to n2 
> 		R[j] = A[q + j]
> 
> 	L[n1 + 1] = ∞
> 	R[n2 + 1] = ∞
> 	i = 1
> 	j = 1
> 	for k == p to r
> 		if L[i] <= R[j]
> 			A[k] = L[i]
> 			i = i + 1
> 		 else A[k] = R[j]
> 			 j = j+1
> ```

$$T(n) = 2T(n/2) + \theta(n)$$
$$T(n) = \theta(nlogn)$$

## Quick Sort

> [!NOTE]- QuickSort Pseudocode
> ```c
> QuickSort(A,p,r)
> 	if p < r 
> 		q = Partition(A,p,r)
> 		QuickSort(A,p,q-1)
> 		QuickSort(A,q+1,r)
> 
> Partition(A,p,r)
> 	x = A[r]
> 	i = p - 1
> 	for j = p to r -1 
> 		if A[j] <= x
> 			i = i + 1
> 			exchange A[i] with A[j]
> 	exchange A[i+ 1] with A[r]
> 	return i + 1
> ```

$$T(n) = T(k) + T(n-k-1) + \theta(n)$$
Worst Case : $T(n) = \theta(n^2)$
Best Case    : $T(n) = \theta(nlogn)$

## Binary Search

$$T(n) = T(n/2) + \theta(1)$$
$$T(n) = \theta(logn)$$

## Powering Number

Naive algorithm : $T(n) = \theta(n)$
Divide and Conquer : $T(n) = \theta(logn)$

## Fibonacci number 

Bottom up : $T(n) = \theta(n)$
Naive recursive squaring = $T(n) = \theta(logn)$

## Matrix Multiplication

> [!NOTE]- Square Matrix Multiplication Recursion Pseudocode
> ```c
> n = A.rows
> let C be a new nxn matrix
> if n==1
> 	c11 = a11.b11
> else partition A,B and C as in equation(4.9)
> 	C11 = SQMR(A11 , B11) + SQMR(A12,B21)
> 	C12 = SQMR(A11 , B12) + SQMR(A12,B22)
> 	C21 = SQMR(A21 , B11) + SQMR(A22,B21)
> 	C22 = SQMR(A21 , B12) + SQMR(A22,B22)
> return C
> ```

$$
T(n) =
\begin{cases}
\Theta(1), & \text{if } n = 1, \\
8T(n/2) + \Theta(n^2), & \text{if } n > 1.
\end{cases}
$$
$$T(n) = \theta(n^3)$$


# L6 : HeapSort
https://youtu.be/2DmK_H7IdTo

> [!NOTE]- HeapSort Pseudocode
> ```c
> Heapsort(A as array)
> 	BuildMaxHeap(A)
> 	for i = n to 1
> 		swap(A[1],A[i])
> 		n = n - 1
> 		Heapify(A,1)
> 		
> BuildMaxHeap(A as array)
> 	n = elements_in(A)
> 	for i = floor(n/2) to 1
> 		Heapify(A,i)
> 
> Heapify(A as array,i as int)
> 	left = 2i
> 	right = 2i + 1
> 
> 	if(left <= n) and (A[left] > A[i])
> 		max = left
> 	else
> 		max = i
> 
> 	if(rigth<= n) and (A[right] > A[max])
> 		max = right
> 
> 	if(max != i)
> 		swap(A[i],A[max])
> 		Heapify(A,max)
> ```

# L7 

## Permute By Sorting

> [!NOTE]- Permute By Sorting Pseudocode
> ```
> n = A.length
> let P[1...n] be a new array
> for i = 1 to n 
> 	P[i] = Random(1,n^3)
> sort A,using P as sort keys
> ```

## Randomize In-Place

> [!NOTE]- Randomize In-Place Pseudocode
> ```
> Randomize-in-Place(A)
> 	n = A.length
> 	for i = 1 to n 
> 		swap A[i] with A[Random(i,n)]
> ```

## Randomized-Select

> [!NOTE]- Randomized Select Pseudocode
> ```
> Randomized-Select(A,p,r,i)
> 	if p == r
> 		return A[p]
> 	q = Randomized-Partition(A,p,r)
> 	k = q -p + 1
> 	if i == k 
> 		return A[q]
> 	elseif i < k
> 		return Randomized-Select(A,p,q-1,i)
> 	else return Randomized-Select(A,q+1,r,i-k)
> ```


# L11


# L12

[!NOTE]- Kruskal's Algo Pseudocode
```
MST-KRUSKAL(G,w)
	A = 
```


