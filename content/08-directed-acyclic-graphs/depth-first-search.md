[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Depth-First Search

|             | Complexity              | Note |  
|---          |---                      |---   |
| Worst Time: | **O(E + V)**    | Initialisation takes O(E+V), inner loop takes O(E + V) |
| Worst Space: | **O(E + V)** | Using an adjacency list

### Algorithm

1. Initialise `L`, an empty list that will contain the sorted vertices
2. While there are unmarked vertices:
	- `visit(vertex)`

#### `visit(vertex)`

1. If `vertex` has a temporary mark then stop (not a DAG)
2. if `vertex` is not marked (i.e. has not been visited yet)
	- mark `vertex` temporarily
	- for each `node` with an edge from `vertex` to `node`
		- `visit(node)`
	- mark `vertex` permanently
	- unmark `vertex` temporarily
	- add `vertex` to the beginning of `L`

### Pseudocode

```
Sorted = []
Color all vertices yellow

while there are yellow vertices:
	select a yellow vertex X
	visit(X)
	
visit(X):
	if X is green
		return ERROR
	if X is yellow
		color X green
		for each neighbor Y of X
			visit(Y)
		color X red # red means it has been sorted
		add X to the beginning of Sorted
```

Note that a vertex is _sorted_ only after all its neighbouring vertices have been added