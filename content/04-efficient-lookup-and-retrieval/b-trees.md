[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# B-Trees

```
         |4|8|
       /   |   \
      /    |    \
     /     |     \
    /      |      \
   /       |       \
|2|3|    |6|7|  |10|11|12|

^ A B-Tree, where t = 3

```

## Properties

- Are balanced search trees
- Tree is no longer binary, but has many branches per node
- Used on many systems that rely on a large amount of data storage and retrieval (e.g. hard disks and databases)

### Nodes

- Nodes have `n` keys and `n+1` pointers to its children
- Keys (K) are stored in ascending order
	- i.e. K<sub>1</sub> ≤ K<sub>2</sub> ≤ K<sub>3</sub> ≤ ... ≤ K<sub>n</sub>
- All elements in a subtree (T) of a node are less than or equal to a corresponding key
	- i.e. {T<sub>1</sub>} ≤ K<sub>1</sub> ≤ {T<sub>2</sub>} ≤ K<sub>2</sub> ≤ ... ≤ {T<sub>n-1</sub>} ≤ K<sub>n</sub> ≤ {T<sub>n</sub>}
- Each pointer in a node points to the location of the node in the memory
- Each _non-root_ node must have at least `t-1` keys (`t` is the **minimum degree**)
- Each node (including root) can have at most `2t-1` keys
	- If > `2t-1`, it is _overflowed_ and must be fixed
	- If < `t-1`, it is _underflowed_ and also must be fixed
	- If = `2t-1`, it is full and perfect 👌

### Trees

- B-trees begin with a root node
- All leaf nodes have the same depth
- The height of a B-Tree is O(log<sub>`t`</sub> N), where N is the number of entries in a B-Tree
	- log<sub>`t`</sub> N << log<sub>2</sub> N if `t` is not small
	- e.g. if N ~ 1B, the height of a binary search tree is at least 30; the height of a B-tree would be 3 (`t = 1000`) or 5 (`t = 100`) with the same N

## Algorithms

### 🔎 Searching

|             | Time Complexity              | Note |
|---          |---                      |---   |
| Worst Case: | **O(t log<sub>t</sub> n)**    | height of tree is O(log<sub>t</sub> n), and there are t operations for every level  |
| Best Case:  | **O(1)**    | First item is the search key

Similar to searching in a Binary Search Tree

1. Load the root node
2. Look at each key in the node and find the appropriate pointer
3. Traverse down the pointers until the node is found

### ✳️ Inserting

|             | Time Complexity              | Note |
|---          |---                      |---   |
| Worst Case: | **O(t log<sub>t</sub> n)**    | height of tree is O(log<sub>t</sub> n), and there are t operations for every level  |
| Best Case:  | **O(1)**    | First item is the entry point

#### Splitting Full (Root) Nodes

1. Choose the median key of the node N, and create a new root node R containing the median
2. Split N into two halves, which will be the children of R

#### Splitting Full Non-Root Nodes

1. Move the median to the parent node
2. Split the current node into two halves and add pointers

#### Inserting a Key X

1. Traverse the tree as if we are searching for X
2. If a full node is retrieved during traversal, split it
3. When a non-full leaf node is reached, insert X in it

### ❌ Deletion

|             | Time Complexity              | Note |
|---          |---                      |---   |
| Worst Case: | **O(t log<sub>t</sub> n)**    | height of tree is O(log<sub>t</sub> n), and there are t operations for every level  |
| Best Case:  | **O(1)**    | First item is the item to be deleted

- A node is **underflowed** if it has < `t-1` elements
- A node is **rich** if it has at least `t` elements 
	- i.e. it can give away one element
- A node is **poor** if it has exactly `t-1` elements
	- i.e. deletion will cause this to be underflowed

#### Case 1: X belongs to a rich leaf node

- Trivial; delete from leaf node

#### Case 2: X belongs to a rich non-leaf node

- **Case 2a**: one of the children of X is rich
	- If left child L is rich, find the largest element t in the subtree rooted at L, then delete and replace X with t (mirrored for right child)
- **Case 2b**: both children of X are poor
	- Merge parent element x with child nodes
	- Recursively delete x from new node

#### Case 3: The traversal to X passes through a poor non-root node N

- **Case 3a**: at least one immediate subling of N is rich
	- Access relevant child node, if reached a poor node, pass a node from the rich sibling to the parent, then pass a node from the parent to the poor node, then delete X
- **Case 3b**: the immediate sibling(s) is/are poor
	- Merge parent key with children, then continue as normal
