[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Kahn's Algorithm

|             | Complexity              | Note |  
|---          |---                      |---   |
| Worst Time: | **O(E + V)**    | Initialisation takes O(E+V), inner loop takes O(E + V) |
| Worst Space: | **O(E + V)** | Using an adjacency list

### Algorithm

1. Initialise two lists:
	- `L`, to hold the sorted elements
	- `S`, all the vertices in the graph with no incoming edges
2. repeat until `S` is empty:
	- remove a vertex `n` from `S`
	- append `n` to `L`
	- for every vertex `m` that `n` connects to (i.e. `n` → `m`)
		- remove all of `m`'s connections from `n`
		- then add `m` to `S`
3. Return `L`

### Pseudocode

```
L = Empty list that will contain the sorted elements
S = Set of all nodes with no incoming edges

while S is non-empty
	remove a node n from S
	append n to L
	for each node m with an edge e from n to m
		remove edge e from graph
			if m has no other incoming edges then
				insert m into S
if graph has edges after above then
	return error (graph has at least one cycle)
else
	return L (a topologically sorted order)

```