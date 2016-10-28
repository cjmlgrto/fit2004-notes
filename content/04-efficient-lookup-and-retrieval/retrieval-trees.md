[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Retrieval Trees (Prefix Trees)

```
    c
   / \
  a   o
 / \   \
r   t   w

^ Trie for [cat, car, cow]
```

### Properties

- The _max depth_ is the length of the longest string in the collection
- Insertion, Deletion and Lookup operations take time proportional to the length of the string being queried
- Much wasted space, as every node has 1 pointer per symbol in the alphabet, and depper nodes have typically null pointers
- Can reduce total space usage by turning each node into a linked list or binary search tree (trading time for space)

### Insertion

- Start at root
- Check 'connected' letters
- if no corresponding letter, 
	- attach the new letter as a new node
- Else
	- go down the path recursively until no corresponding node is found
	- attach the new letter node

### Searching

- Start at root
- For each character `c` in the string
	- If a node containing `c` exists
		- Move to the node
		- If no nodes are connected, it is found
	- Else
		- It is not found

### Implementing a Trie

- Every node will contain an array of size N (where N is the size of the set alphabet of the strings)
- This allows for O(1) operations per node

### Advantages and Disadvantages

#### Pros

- A better search structure than a Binary Search Tree for string keys
- A more versatile search than a Hash Table
- Allows lookup on prefix matching in O(M)-time, where M is the length of the prefix
- Allows sorting collection of strings in O(S) time where S is the total number of characters in all strongs

#### Cons

- On average, Tries can be slower (in some cases) than Hash Tables for lookups
- Requires _a lot of wasted space_ due to each node having an array with a size N for alphabet size N (and leaf nodes have null pointers)



