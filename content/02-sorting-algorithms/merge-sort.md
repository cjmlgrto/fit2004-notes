[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Merge Sort

|             | Complexity              | Note |
|---          |---                      |---   |
| Best Time: | **O(n log n)**    | Merge operation on every step |
| Average Time:  | **O(n log n)**    | Same as above
| Worst Time:  | **O(n log n)**    | Same as above
| Stability:  | **Stable**              |
| In-place:   | **No**
| Best Space:  | **O(n)**    | Requires splitting list into new ones
| Average Space:  | **O(n)**    | Same as above
| Worst Space:  | **O(n)**    | Same as above

### Algorithm

1. Split the list into two
2. For each sublist, split it again
3. Once fully split, merge back in the right order


### Python Implementation

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