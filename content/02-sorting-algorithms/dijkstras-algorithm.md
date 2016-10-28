[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Dijkstra's Algorithm

|             | Complexity              | Note |  
|---          |---                      |---   |
| Worst Time: | **O(E log V + V log V)**    | For every vertex V and edge E: heap operations take log V  |
| Worst Space:  | **O(V + E)**  | Assuming an Adjacency List is used

Exactly like Breadth-First Search, but applied to finding the shortest distances between vertices. This is designed for **weighted** graphs.

The following algorithm can be used for searching a single vertex and a shortest path, by modifying it to stop as soon as the target is _finalised_. And then, the shortest path from the source to the target can be recovered easily by building a list of pointers from the start to end.

### Algorithm

1. Initialise a heap called `Discovered` and insert the starting vertex in it with distance `0`
2. Initialise a list called `Finalised` to store the distances from the source to every _finalised_ vertex
3. While `Discovered` is not empty:
	- Pop the root of the heap (this is the vertex `V` with the smallest distance from the source)
	- For each outgoing edge `(V, U, weight)` of `V`
		- If `U` is not in `Discovered`
			- Insert `U` in `Discovered` with the distance `distance of U from V` + `distance of V from source`
		- Else, if it is in `Discovered` and if `U` is not finalised,
			- Update the distance of `U` with the smaller distance: either `distance of U from V` + `distance of V from source` or leave it be
	- Move `V` from `Discovered` to `Finalised`

### Proof of Correctness

- Suppose S → T represents the shortest path from S to T
- Let `U` be the last vertex on the shortest path S → T
	- Shortest path S from S → U must be a part of S → T
	- The shortest path distance of S → U is smaller than S → T
- Since S → U is smaller than S → T, U is _finalised_ before T
- Therefore, the shortest path from S → T can be obtained by greedily extending previously known shortest paths	