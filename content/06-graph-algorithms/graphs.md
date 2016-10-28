[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Graphs

A **Graph** is a set of vertices (nodes) and edges. A graph can be defined as `G = (V,E)` where `V` is the set of vertices, and `E` the edges.

An **Edge** is represented as `e = (u,v)`, which is a path that connects two vertices `u` and `v`. For _undirected_ graphs, `(u,v) = (v,u)`.

A **Weighted** graph is represented as `G = (V,E,W)` where `W` lists the weight for edges, and each edge is represented as `e = (u,v,w)` in which `w` is the weight.

The maximum number of edges in a _directed_ graph (excluding self-edges) is V(V-1) ≈ O(V<sup>2</sup>).

The maximum number of edges in an _undirected_ graph (excluding self-edges) is V(V-1)/2 ≈ O(V<sup>2</sup>).

A graph is called **sparse** if |E| << V<sup>2</sup>, and **dense** if E ≈ V<sup>2</sup>.

## Representing Graphs

### Adjacency Matrix

- A V<sup>2</sup>-size matrix `M` where `M[i][j]` stores the information between vertex `i` and vertex `j`.
- Information is just `T` if there is an edge in between, and `F` if none
- For weighted graphs, weight has a value, otherwise if there is no edge, it is `None`

### Adjacency List

- An array of size V, where the `i`-th item stores the indices of the vertices it is connected ti
- Can also store tuples that hold not just the indices, but also the weight
