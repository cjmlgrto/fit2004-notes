[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Selection Sort

|             | Complexity              | Note |
|---          |---                      |---   |
| Worst Case: | **O(n<sup>2</sup>)**    | Because it has to compare every item in the list |
| Best Case:  | **O(n<sup>2</sup>)**    | Because it has to compare every item in the list
| Stability:  | **No**              |
| In-place:   | **Yes**

### Algorithm

1. For every item in the list, find the minimum item
2. Swap the minimum item with the current selected item
3. Repeat until all items have been iterated over

### Python Implementation

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
