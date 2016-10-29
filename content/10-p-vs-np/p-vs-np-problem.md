[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# The P vs NP Problem

- **P-class** problems are ones that can be solved in *Polynomial* time— or there is an upper bound O(N<sup>k</sup>), where k is a constant
	- e.g. algorithms implemented in O(N), O(N<sup>2</sup>), O(log N), ...
- **NP-class** problems are ones with a complexity above the upper bound O(N<sup>k</sup>)— solved in _Non-deterministic_ Polynomial time.
	- e.g. algorithms that require O(2<sup>N</sup>), O(N!)

### The Million-Dollar Dilemma
	
- If we can solve one NP-complete problem in polynomial time, this means every NP problem can be solved in polynomial time
- This would mean that P = NP
- Unfortunately, we are unable to solve any NP-complete problem in polynomial time AND we are unable to prove that a polynomial time solution is impossible
- Thus, we are not sure if P = NP or P ≠ NP
- This is the P vs NP problem

If P = NP is proved:

- We will be able to solve a lot of challenging and really useful problems efficiently
- But cryptography is based on the challenging nature of factorization and will fail if P = NP is proved

If P ≠ NP is proved:

- A great theoretical leap
- We will move towards finding alternate solutions to NP problems— though we're already doing it since it is largely believed that P ≠ NP

### Decision Problems

**Decision Problems** are problems that require only a _Yes_ or _No_ solution, for example:

- Is there a path from S to T in the graph G?
- Does this graph have a cycle?

The following are not decision problems:

- Find the shortest path from S to T in the graph G
- Find a cycle in this graph

## NP Class Problems

A 'certificate' of a decision problem is an instance for which the answer to a particular problem is _YES_.

A decision problem belongs to the NP class if its certificate can be _verified_ in polynomial time.

Examples of NP class problems are:

- Vertex Cover Decision Problem
	- A _vertex cover_ in a graph G is a subset of vertices that covers all edges— the question asks if there is a vertex cover of size _k_ in a graph.
- Clique Decision Problem
	- A _clique_ is a subset of vertices that are all connected to each other— the question asks if there is a clique of size _k_ in a graph
- "Is there a path from S to T in a graph G?"


## P Class Problems

A decision problem is in P class if it can be _solved_ in polynomial time.

Examples are:

- "Is there a path between S and T?"
	- solved using breadth-first search
- "Is there a minimum spanning tree in the graph with weight W?"
	- Compute min-span tree using Prim's algorithm and check its weight

Note: a problem in P class is also in NP class (since any P-class-problem's certificate can be verified in Polynomial time)

## NP-Complete Class

- A problem X belongs to NP-complete class if:
	- It is in NP class AND
	- every NP problem Y can be reduced to X in polynomial time
- Suppose we denote Y → X to show that Y can be reduced to X
- If Z → Y and Y → X then Z → X (i.e. Z can be reduced to X)
- To show that a problem is NP-complete, all we need to do is to show that
	- Its certificate can be verified (i.e. it is in NP class)
	- At least one NP-complete problem can be reduced to it
- e.g. Let Z be a problem in NP-complete, and we want to prove that X is also in NP-complete. To prove this, we need to show that Z → X.

## Polynomial Time Reduction

- We do know now the polynomial time solutions for _Vertex Cover_ and _Clique_  problems
- Suppose we have a 'magic box' that transforms (reduces) Vertex Cover to the Clique problem and this reduction takes polynomial time
- Assume that in the future, someone solves the Clique problem in polynomial time
- This means that Vertex Cover can then be solved in polynomial time!
- This concept is known as Polynomial Time Reduction

### Examples

- Suppose we have proved that the problem of computing Clique is NP-complete
- To prove that Vertex Cver is NP-complete, we need to show that:
	- Its certificate can be verified in polynomial time
	- It can be reduced in polynomial time to at least one NP-complete problem (e.g. Clique)
- Clique Problem: is there a clique of size k in graph G?
- Vertex Cover: is there a vertex cover of size k in graph G?
- Complement of a graph G=(V,E) is a graph G' = (V,E') that has the same vertices V as G, and has an edge between two vertices u and v iff there is not an edge between u and v in the original graph G
- Given a graph G = (V,E) it has a vertex cover of size k iff its complement graph G' has a clique of size N-k where N is the number of vertices
