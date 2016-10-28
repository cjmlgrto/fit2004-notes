[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Minimum Spanning Trees

A **tree** is a connected, undirected graph with no cycles in it

A **spanning tree** of a general, undirected, weighted graph G is a tree that spans G— i.e. a tree that includes every vertex of G, and is a subgraph of G

- A spanning tree of a connected graph G that has a _maximal set of edges_ contains _no cycles_
- One with a _minimal set of edges_ connects _all vertices_
- _Weight_ of a spanning tree is the sum of the weight of the edges in the tree
- A **minimum spanning tree** of a weighted graph is a tree that spans G, with the most minimal weight of all possible spanning trees of the graph
	- There may be more than one minimum spanning trees (i.e. min-span trees with equal weights)

### Constructing Min-Spanning Trees: The Strategy

- Let M denote the min-span tree we are constructing
- An edge `e` is said to be safe if M ⋃ `e` is a subset of a min-span tree

1. M = null
2. While M can be grown safely:
	- Find an edge `e = <x,y>` along M which is safe to grow
	- M = M union `e`
3. Return M