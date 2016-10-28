[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Floyd-Warshall Algorithm

|             | Complexity              | Note |  
|---          |---                      |---   |
| Worst Time: | **O(V<sup>3</sup>)**    | 3 nested iterations of every vertex in the graph  |
| Worst Space:  | **O(V<sup>2</sup>)**  | Uses a V × V sized distance array

Used to return the shortest distances between **all** pairs of vertices in any graph. A step-by-step version can be seen [here](https://www.youtube.com/watch?v=4OQeCuLYj-4)

### Algorithm

1. Create an adjacency matrix called `dist[][]`
2. For each vertex `k` in the graph:
	- For every pair of vertices `i` and `j` in the graph:
		- If dist(i → k → j) < current dist(i → j)
			- Update/create shortcut i → j with weight equal to dist(i → k → j) (i.e. `dist[i][j] = dist[i][k] + dist[k][j]

### Pseudocode

```
let V = number of vertices in graph
let dist = V * V array of minimum distances
for each vertex v
	dist[v][v] = 0
for each edge (u,v)
	dist[u][v] = weight(u,v)
for k from 1 to V

# Loop Invariant: dist[i][j] corresponds to the shortest path from i to j considering the intermediate vertices 1 to k-1

	for i from 1 to V
		for j from 1 to V
			if dist[i][j] > dist[i][k] + dist[k][j]
				dist[i][j] = dist[i][k] + dist[k][j]
```

### Proof of Correctness

- The invariant in the code is central to the algorithm's correctness
- That is: at the start of the k-th iteration of the outer loop, dist[i][j] corresponds to the shortest path from i to j considering the intermediate vertices 1 to k-1
	- This is true for k=1
	- If the k-th vertex is to improve on the known path from vertex i to j, then it can only be by going from i to tk and then k to j
	- Thus, minimum of dist(i → k → j) and dist dist(i → j) gives the minmum distance from i to j considering intermediate vertices 1 to k

### Transitive Closure

- Given a graph G = (V,E), its **transitive closure** is another graph, (V,E') that contains the same vertices V but contains an edge between any two vertices u and v such that there is a path between u and v in the original graph
- In other words, the transitive closure is a way to check if there is a path from vertex a to vertex b.

#### The Floyd-Warshall Algorithm for Transitive Closure

Works the same way, but assign each edge a weight of 1. Then, scan through the matrix: if `dist[i][j]` is not infinity, then there is a path from `i` to `j` in the graph. Or, set it to True/False.

```
for vertex i in 1..V
	for vertex j in 1..V
		if there is an edge between i and j or i==j:
			dist[i][j] = True
		else:
			dist[i][j] = False

for vertex k in 1..V
	for vertex i in 1..V
		for vertex j in 1..V
			dist[i][j] = dist[i][j] or (dist[i][k] and dist[k][j])
```