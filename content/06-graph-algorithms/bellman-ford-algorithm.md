[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Bellman-Ford Algorithm

|             | Complexity              | Note |  
|---          |---                      |---   |
| Worst Time: | **O(VE)**    | V-1 iterations, and for every iteration, go through every edge E in the graph  |
| Worst Space:  | **O(V + E)**  | Assuming an Adjacency List is used

A path traversal algorithm for graphs **negative weights** for edges. A step-by-step example [can be found here](https://www.youtube.com/watch?v=obWXjtg0L64).

Dijkstra's algorithm will fail for graphs with negative weighted-edges because it is a _greedy_ algorithm. The Bellman-Ford algorithm is not.

[How Bellman-Ford works](https://www.youtube.com/watch?v=9PHkk0UavIM) is that it uses the fact that the shortest path from A to B with V vertices in total in a graph, will take at most V-1 edges to get there. If there is greater than V-1 edges, then some edges will either cycle or repeat.

The algorithm minimises traversing extra edges by iterating at most V-1 times.

### Algorithm

1. Let `s` be the start vertex and `V` be the number of vertices in the graph
2. Set the distance of all vertices in the graph to ∞
3. Repeat V-1 times:
	- for every edge in the graph:
		- if the edge distance is smaller than the distance to the source, update the distance
4. For every edge in the graph:
	- If the distance between from one vertex to the next is less than the distance of the previous vertex, return an error

### Pseudocode

```
dist[1...V] = infinifty
pred[1...V] = Null
dist[s] = 0

for i = 1 to V-1:
	for each edge <u,v,w> in the whole graph:
		est = dist[u] + w
		if est < dist[v]:
			dist[v] = est
			pred[v] = u

for each edge <u,v,w> in the whole graph:
	if dist[u] + w < dist[v]:
		return error
		#	negative edge cycle found

return dist[...], pred[...]
```

### Proof of Correctness

- A negative cycle is when negative edges force a greedy algorithm to take extra edges to get to a vertex
- The maximum number of edges in a shortest path between two vertices is V-1
- The estimated distance (on every iteration) is updated as many times as the possible path length; and as such, the shortest path will converge:
	- The first iteration guarantees the shortest distances to all vertices considering paths of length at most 1 edge
	- The second iteration guarantees the shortest distances to all vertices considering paths of length at most 2 edges
	- ...
	- The V-1-th iteration guarantees the shortest distances to all vertices considering paths of length at most V-1 edges
- If the V-th iteration reduces the distance of a vertex, this means there is a 'shorter' path using V edges, and thus implies there is a negative cycle
- The Bellman-Ford algorithm iterates at most V-1 times, thus considering only the paths that take V-1 edges, and hence, no negative cycles