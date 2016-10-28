[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Heap Sort (Min-Heap)

|             | Complexity              | Note | 
|---          |---                      |---   |
| Worst Case: | **O(n log n)**    | Insertion takes O(n), Heap operations take O(log n) |
| Best Case:  | **O(n log n)**    | Insertion takes O(n), Heap operations take O(log n)
| Stability:  | **No**              |
| In-place:   | **Yes**

### (Min) Heap Data Structure Properties

- Represented as a tree, implemented as an array
- The root of the tree is the smallest item in the array
- Child of any node is larger than parent node
- If `k` represents the position of a node in an array, the parent is in the `k//2` position of the array
- If `k` represents the position of a node in an array, the children are either the `2k`-th or the `2k+1`-th items of the array

### Algorithms

#### Insertion

1. Add the item to the end of the list
2. _Rise_ the item

#### Rise (item in position `k`)

1. While the `k`-th item is larger than the `k//2`-th item,
2. Swap them

#### Retrieval

1. Swap the root and the last node of the heap
2. Pop the last node
3. _Sink_ this new root

#### Sink (item in position `k`)

1. While 2 × `k` is less than the number of items in the heap,
2. Set `child` as the largest child of the current `k`-th item (children are in position `2k` or `2k+1`)
3. If the current `k`-th item is greater than or equal to the child, STOP
4. Otherwise, swap the `child` and the `k`-th item
5. Set `k` as the position of the last `child`

#### Sorting in O(n log n)

1. Insert every item into the heap
2. Let the heap do its magic 🔮
3. Pop the root of the heap until its empty
4. Ta-da, a sorted list

#### Sorting in O(n)

1. Iterate over the list backwards
2. Sink every item of the list

### Python Implementation

#### Heap Data Structure

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

#### Heap Sort in O(n log n)

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

#### Heap Sort in O(n)

```python
def heapSort(L):
	for i in range(-1,len(L)-1,-1):
		sink(L, i)
	return L
```
