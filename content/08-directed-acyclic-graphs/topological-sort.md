[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Topological Sort

In a _Directed Acyclic Graph_, vertices have a 'partial' order:

- if A → B, then A < B. If A → B → C
- then we know that A < B, B < C
- and therefore, A < C

A **Topological Sort** is a list of the vertices in partial order.

Bonus: [here's a real-life example of a DAG in use](https://github.com/iOS10-KIT/UI/network).



