[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Breadth-First Search

|             | Complexity              | Note |  
|---          |---                      |---   |
| Worst Time: | **O(V + E)**    | Where V is the number of vertices and E is the number of edges |
| Worst Space:  | **O(V + E)**  | Assuming an Adjacency List is used

An algorithm to traverse (or specifically search for) nodes in an **unweighted** graph. The basic idea is to traverse every node by placing any newfound nodes into a queue to be traversed through.

### Algorithm

1. Initialise a list called `Discovered` and insert the starting node `A` with distance `0`
2. Initialise a list called `Finalised`
3. While `Discovered` is not empty:
	- Get the first vertex `V` from the `Discovered` list
	- For each adjacent vertex `U` of `V`:
		- If `U` is _not discovered_ or _finalised_:
			- Set the distance of `U` to the distance of `V` + `1`
			- Insert `U` at the end of `Discovered`
	- Move `V` from `Discovered` to `Finalised`

	