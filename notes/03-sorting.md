[← Return to Index](/readme.md)

# Sorting

## Selection Sort
|             | Complexity              | Note |
|---          |---                      |---   |
| Worst Case: | **O(n<sup>2</sup>)**    | Because it has to compare every item in the list |
| Best Case:  | **O(n<sup>2</sup>)**    | Because it has to compare every item in the list
| Stability:  | **No**              |
| In-place:   | **Yes**

1. For every item in the list, find the minimum item
2. Swap the minimum item with the current selected item
3. Repeat until all items have been iterated over

```python
def selection_sort(L):
	 n = len(L)
	 for k in range(n - 1):
	 	 min = find_min(L, k)
	 	 L[k], L[min], L[min], L[k]
	 	 
def find_min(L, k):
	 min = k
	 n = len(L)
	 for i in range(k + 1, n):
	 	 if L[i] < L[min]:
	 	 	 min = i
	 return min
```

## Insertion Sort
|             | Complexity              | Note |  
|---          |---                      |---   |
| Worst Case: | **O(n<sup>2</sup>)**    | When the list is sorted in reverse |
| Best Case:  | **O(n)**                | When the list is already sorted |
| Stability:  | **Stable**              |
| In-place:   | **Yes**

For every item in the list, insert it in the right position

```python
def insertion_sort(L):
	 n = len(L)
	 for mark in range(1, n):
	 	  temp = L[mark]
	 	  i = mark - 1
	 	  while i >= 0 and L[i] > temp:
	 	  	  L[i + 1] = L[i]
	 	  	  i -= 1
	 	  L[i + 1] = temp
```

## (Min) Heap Sort
|             | Complexity              | Note | 
|---          |---                      |---   |
| Worst Case: | **O(n log n)**    | Insertion takes O(n), Heap operations take O(log n) |
| Best Case:  | **O(n log n)**    | Insertion takes O(n), Heap operations take O(log n)
| Stability:  | **No**              |
| In-place:   | **Yes**

### (Min) Heap Data Structure

- Represented as a tree, implemented as an array
- The root of the tree is the smallest item in the array
- Child of any node is larger than parent node
- If `k` represents the position of a node in an array, the parent is in the `k//2` position of the array

```python
class Heap:
    def __init__(self):
        self.count = 0
        self.array = [None]

    def __len__(self):
        return self.count

    def __str__(self):
        return str(self.array)

    def add(self, item):
        self.array.append(item)
        self.count += 1
        self.rise(self.count)

    def rise(self, k):
        while self.array[k] > self.array[k//2] and k > 1:
            self.swap(k, k//2)
            k //= 2

    def swap(self, i, j):
        self.array[i], self.array[j] = self.array[j], self.array[i]

    def get_max(self):
        self.swap(1, self.count)
        maximum = self.array.pop(self.count)
        self.count -= 1
        self.sink(1)
        return maximum

    def sink(self, k):
        while 2*k <= self.count:
            child = self.largest_child(k)
            if self.array[k] >= self.array[child]:
                break
            self.swap(child, k)
            k = child

    def largest_child(self, k):
        if 2*k == self.count or self.array[2*k] > self.array[2*k+1]:
            return 2*k
        else:
            return 2*k + 1
```

### Heap Sort in O(n log n)

```python
def heapSort(L):
	heap = Heap()
	for item in L:
		heap.add(item)
	L = []
	while len(heap) > 0:
		L.append(heap.get_max)
	return L
```

### Heap Sort in O(n)

```python
def heapSort(L):
	for i in range(-1,len(L)-1,-1):
		sink(L, i)
	return L
```

## Merge Sort

|             | Complexity              | Note | 
|---          |---                      |---   |
| Worst Case: | **O(n log n)**    | Height of the binary tree times merge complexity |
| Best Case:  | **O(n log n)**    | Height of the binary tree times merge compexity
| Stability:  | **Stable**              |
| In-place:   | **No**

1. Split the list into two
2. For each sublist, split it again
3. Once fully split, merge back in the right order

```python
def merge_sort(L):
    if len(L) < 2:
        return L
    else:
        mid = len(array) // 2
        left = merge_sort(L[:mid])
        right = merge_sort(L[mid:])
        return merge(left, right)

def merge(L, R):
    i = 0
    j = 0
    ordered = []
    while i < len(L) and j < len(R):
        if L[i] < R[j]:
            ordered.append(L[i])
            i += 1
        elif L[i] > R[j]:
            ordered.append(R[j])
            j += 1
        else:
            ordered.append(L[i])
            i += 1
            ordered.append(R[j])
            j += 1
    while i < len(L):
        ordered.append(L[i])
        i += 1
    while j < len(R):
        ordered.append(R[j])
        j += 1
    return ordered
```

## Quicksort

|             | Complexity              | Note | 
|---          |---                      |---   |
| Worst Case: | **O(n<sup>2</sup>)**    | Height of the binary tree times merge complexity |
| Best Case:  | **O(n log n)**    | Height of the binary tree times merge compexity
| Stability:  | **No**              |
| In-place:   | **No**

1. Partition the list
2. Sort the first part (recursively)
3. Sort the second part (recursively)

To partition:

1. Choose an item, called the pivot then put it at the front of the list
2. Create a variable called the boundary and set it to the position of the pivot
3. Iterate over every item after the pivot
4. If the item is greater than the pivot, ignore
5. If it is less than the pivot, swap it with the item next to the boundary, then increment the boundary
6. Continue until the entire list has been iterated over
7. Swap the boundary with the pivot so that the pivot is now in the 'middle' of the list
8. Do this again for every sublist before and after the pivot

For quicksort, the pivot matters— the more unbalanced the partition, the more complex the runtime. The best choice of pivot for the pivot is the middle, as it will ensure the number of elements in each sub-array are almost equal.


```python
def quick_sort(L):
    start = 0
    end = len(L)-1
    quick_sort_aux(L, start, end)

def quick_sort_aux(L, start, end):
    if start < end:
        boundary = partition(L, start, end)
        quick_sort_aux(L, start, boundary-1)
        quick_sort_aux(L, boundary+1, end)

def partition(L, start, end):
    mid = (start + end) // 2
    pivot = L[mid]
    L[start], L[mid] = L[mid], L[start]
    index = start
    for k in range(start+1, end+1):
        if L[k] < pivot:
            index += 1
            L[k], L[index] = L[index], L[k]
    L[index], L[start] = L[start], L[index]
    return index
```
    

