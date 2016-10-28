[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Kruskal's Algorithm

|             | Complexity              | Note |  
|---          |---                      |---   |
| Worst Time: | **O(E log V + V log V)**    | Initialisation takes O(V), Sorting Edges takes O(E log E) using Merge Sort, for loop executes O(E) times, `UNION_SET()` takes O(V log V) |

Another greedy algorithm to find a minimum spanning tree for a connected graph. Here's a [step-by-step video](https://www.youtube.com/watch?v=71UQH7Pr9kU).

### Algorithm

1. Sort the edges in ascending order of weights
2. For each edge `(v,u,w)` in ascending order
	- If adding `(v,u)` does not create a cycle in `Finalized`
		- Add `(v,u)` in `Finalised`
3. Return `Finalised`

### Pseudocode

```
for each vertex x in V:
	create a new set containing only x

sort edges in increasing order by weight

Finalised = []

for each edge <u,v,w> in sorted order:
	# Loop Invariant: Finalised is a subset of a min-span tree
	if SET_ID(u) != SET_ID(v):
		Finalised.append(<u,v,w>)
		UNION_SETS(SET_ID(u), SET_ID(v))

return Finalised
```

#### Union-Find Data Structure

- For each set S<sub>i</sub>, maintain the vertices in it as a linked list
- Create an array `map_array` that will record for each vertex the set it belongs to
	- e.g. if vertex 3 belongs to set S<sub>4</sub>, then `map_array[3] = S4`

```
SET_ID(u):
	return map_array[u] # Cost O(1)

UNION_SETS(S_i, S_j) where S_i < S_j:
	for each vertex v in S_i:
		map_array[v] = S_j
	delete the linked list of S_i and append it to the linked list of S_j
	# Cost is O(V log V) which occurs when |S_i| = |S_j|
```

### Correctness

- Loop Invariant is that `Finalised` is a subset of a min-span tree
- Invariant is true when `Finalised` is empty
- At an arbitrary step, the algorithm combines two sets, S1 and S2 using an edge <D,F>
- Assume that adding <D,F> is incorrect
- The sets S1 and S2 must be connected by at least one edge in every spanning tree
- Let M be a min-span tree that does not contain <D,F>
- Let <D,G> be the first edge on the path that connects S1 and S2 in the min-span tree M
- We will get a spanning tree if we add <D,F> in M and remove <D,G>— let's call this tree T
- The weight of T is smaller or equal to M because the weight of <D,F> is smaller or equal to <D,G>
- Hence T is also a min-span tree of M is a min-span tree— i.e. the invariance holds after adding <D,F> in `Finalised`

	