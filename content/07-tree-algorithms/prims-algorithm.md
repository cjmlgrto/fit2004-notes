[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Prim's Algorithm

|             | Complexity              | Note |  
|---          |---                      |---   |
| Worst Time: | **O(E log V)**    | same as Dijkstra's, but V = E, and for every edge: heap operations take log V  |
| Worst Space:  | **O(V + E)**  | Assuming an Adjacency List is used

A _greedy_ algorithm to find the minimum spanning tree of a graph.

### Algorithm

Similar to Dijkstra's Algorithm, except stores sets of edges rather than distances

1. Start by picking any vertex `v` to be the root of the new min-span tree
2. While the min-span tree does not contain _all_ the vertices of the graph:
	- Find the shortest edge `e` connected to the min-span tree that does not create a cycle
	- Add `e` to the min-span tree

#### Algorithm, Dijkstra-Style:

- Initialise a list called `Discovered` and insert a random node
- Initialise a list called `Finalised`
- While `Discovered` is not empty:
	- Get the vertex `v` from `Discovered` with the smallest weight
	- For each outgoing edge `(v,u,w)` of `v`:
		- If `u` is not in `Discovered`:
			- Insert `u` in `Discovered` with weight `w` and edge `v → u`
		- Else if `u.weight` > `w`:
			- If `u` is not in `Finalised`, update the weight of `u` in `Discovered` to `w` and edge to `v → u`
	- Move `v` from `Discovered` to `Finalised` along with its corresponding edge


### Pseudocode

```
D = [random(V)]
F = []

while len(D) > 0:

	# invariant: F{inalised} is a growing min-span tree

	v = D.get_min()
	F.append(v)
	for each adjacent edge of (v,u,w) adjacent to v:
		if u is not in D:
			insert u in D with weight w and edge <v,u>
		else:
			if u is not in F:
				if u.weight > w:
					update the weight of u to w and edge to <v,u>
return F
```

### Correctness

- The loop invariant is that `Finalised` is a subset of a min-span tree
- The invariance is true when `Finalised` is empty initially
- Suppose the algorithm chooses a vertex E and an edge <C,E> having minimym weight 2
- Assume <C,E> is not an edge in any min-span tree
- Let M be a min-span tree that excludes <C,E>:
	- E must be connected to `Finalised` in M, because it is a min-span tree
	- Since M does not contain <C,E> there must be a path that connects `Finalised` with E
	- Let <C,B> be the first edge on the path that connects `Finalised` to E
- If we remove <C,B> from M and add <C,E> we will still get a spanning tree; Let this spanning tree be called T
- Since the weight of <C,E> is not smaller or equal to the weight of <C,B>, the weight of T is smaller than or equal to M— hence, either M is not a min-span tree or T is also a min-span tree
- Hence, `Finalised` after adding <C,E> is a part of a min-span tree
	- i.e. the invariance holds after adding the edge <C,E>

