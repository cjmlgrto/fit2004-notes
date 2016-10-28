[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Insertion Sort

|             | Complexity              | Note |  
|---          |---                      |---   |
| Worst Case: | **O(n<sup>2</sup>)**    | When the list is sorted in reverse |
| Best Case:  | **O(n)**                | When the list is already sorted |
| Stability:  | **Stable**              |
| In-place:   | **Yes**

### Algorithm

1. Set the second item as the 'mark'
2. If the 'mark' is smaller than the first item, put it before the first item otherwise leave it
3. Set the third item as the 'mark'
4. _Insert_ the 'mark' in the right position within the sublist of the first three items
5. Repeat steps 3-4 for the rest of the list, incrementing 'mark' and inserting it in that growing sublist

### Python Implementation

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
