[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Quick Sort

|             | Complexity              | Note |
|---          |---                      |---   |
| Best Time: | **O(n log n)**    | Pivot chosen is median; equal split on every recursive call |
| Average Time:  | **O(n log n)**    | Same as above
| Worst Time:  | **O(n<sup>2</sup>)**    | Poor choice of pivot; list is naively sorted at n recursive calls
| Stability:  | **No**              |
| In-place:   | **No**
| Best Space:  | **O(log n)**    | log n recursive calls, and pointers stored for every recursive call 
| Average Space:  | **O(log n)**    | Same as above
| Worst Space:  | **O(n)**    | Poor pivot, and thus n recursive calls

### Algorithm

1. Partition the list
2. Sort the first part (recursively)
3. Sort the second part (recursively)

#### To partition:

1. Choose an item, called the pivot then put it at the front of the list
2. Create a variable called the boundary and set it to the position of the pivot
3. Iterate over every item after the pivot
4. If the item is greater than the pivot, ignore
5. If it is less than the pivot, swap it with the item next to the boundary, then increment the boundary
6. Continue until the entire list has been iterated over
7. Swap the boundary with the pivot so that the pivot is now in the 'middle' of the list
8. Do this again for every sublist before and after the pivot

For quicksort, the pivot matters— the more unbalanced the partition, the more complex the runtime. The best choice of pivot for the pivot is the middle, as it will ensure the number of elements in each sub-array are almost equal.

### Python Implementation

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
    

