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

### Python Implementation

```python
class TrieNode:
	def __init__(self, char, value=None):
		self.char = char
		self.value = value
		self.children = [None] * 26
		# 26 = alphabet
		self.indices = []
		
	def __contains__(self, char):
		if self.children[ord(char) % 26] is None:
			return False
		else:
			return True
			
	def __setitem__(self, char, value):
		i = ord(char) % 26
		self.children[i] = value
		self.indices.append(i)
		
	def __getitem__(self, char):
		return self.children[ord(char) % 26]
		
class Trie:
	def __init__(self):
		self.root = TrieNode('')
		
	def insert(self, string, value):
		current = self.root
		for char in string:
			if char not in current:
				current[char] = TrieNode(char)
			current = current[char]
		current.value = value
		
	def get(self, string):
		current = self.root
		for char in string:
			if char in current:
				current = current[char]
			else:
				return None
		return current.value
		
	def match(self, prefix):
		current = self.root
		for char in prefix:
			if char in current:
				current = current[char]
			else:
				return None
		return self.collect(current)
		
	def collect(self, current)
		collection = []
		self._collect_aux(current, collection)
		return collection
		
	def _collect_aux(self, current, collection):
		if current.value is not None:
			collection.append(current.value)
		for i in current.indices:
			self._collect_aux(current.children[i], collection)
```