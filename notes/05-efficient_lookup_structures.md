[← Return to Index](/readme.md)

# Efficient Lookup Structures

## Direct Addressing

- Uses an array of size N for a set of information that's sequenced from 1 to N
- Finding items can be done in O(1) constant time
- If the items aren't sequenced, they can be found using binary search in O(logN) time

## Hash Tables

|             | Time Complexity              | Note |
|---          |---                      |---   |
| Worst Case: | **O(n)**    | Linear, depending on collision handling |
| Best Case:  | **O(1)**    | Thanks to hashing

### Data
- Each item must have a unique key— or the value is converted into a unique key through _hashing_.
- Underlying data structure is either an incredibly large array or a linked list

### Operations
- Hash (maps a unique key to a position in the list)
- Insert
- Search
- Delete

### Hashing
Converts a specified word into a unique key that can be used to determine its position in the underlying array.

The goal is to have a function that maps a _unique_ key for any input value— this is to ensure no 'collisions' occur (that is, two differnt words having the same key). A good hash function requires the following:

- type dependent (otherwise it cannot compute a value)
- must return a value within the array range (otherwise it will return an index error when inserting)
- not have too many operations (otherwise slowness)
- use as much of the key as possible (minimise collisions)
- avoid common factors (minimise collisions)

Below is a _universal_ hash function implemented in Python. It is best to use prime numbers for `TABLE_SIZE`, `a` and `b`.

```python
def hash_function(word, TABLE_SIZE):
    value = 0
    # random seeds
    a = 10651
    b = 10531
    for i in range(len(word)):
        value = (a*value + ord(word[i])) % TABLE_SIZE
        a = a * b % (TABLE_SIZE-1)
    return value
```

### Insertion
1. Use the hash function to get a position
2. Try to insert at position
3. Otherwise, deal with the collision

### Search ("Check if in hash table")
1. Use hash function to get a position
2. If the query matches, return True
3. Otherwise, deal with the collision until found
4. If not found, return False

### Delete
1. Use the hash function to get a position
2. Search for the item, deal with collisions
3. If it exists and is found, remove the item

## Collision Resolution
Clustering occurs when elements of similar keys create groups in a hash table array (called a probe chain)

This is a problem because when a search occurs for a particular key and the actual key location has another item that doesn't belong there, it has to traverse over the entire cluster— which would affect performance.

### Linear Probing
- Checking every item in the array until the position's conditions are perfect
- Check query position, then look at the next, then the next... wrapping around the entire table until you're back to the original position

### Quadratic Probing
- Like Linear Probing, but moving in larger and larger steps, wrapping around the list
- A problem with probing is that items with similar hash values tend to 'cluster'

### Double Hashing
- Using a second hash function to determine the probe 'step' to prevent clustering
- Should not hash to 0, and the table size and step size are co-prime

### Seperate Chaining
- Using linked lists for every item in the large array
- If a collision occurs, just append a node to the end of the chain in the array position and traverse


## Example: Hash Table Dictionary Object
```python
class Dictionary:

	def __init__(self, table_size, prime):
		self.prime = prime
		self.item_count = 0
		self.table_size = table_size
		self.array = [None] * table_size

	def hash(self, key):
		index = 0
		a = 2692
		b = 8523
		for i in range(len(key)):
			index = (a * index + ord(key[i])) % self.table_size
			a = a * b % (self.table_size-1)
		return index

	def is_full(self):
		return self.item_count >= self.table_size

	def insert(self, key, value):
		index = self.hash(key)
		if self.is_full():
			found = False
			end = (index - 1) % self.table_size
			while index != end:
				if self.array[index][0] == key:
					self.array[index] = [key, value]
					found = True
					break
				index = (index + 1) % self.table_size
			if not found:
				raise Exception("Dictionary is full!")
		else: 
			while not self.is_full():
				if self.array[index] != None and self.array[index][0] == key:
					self.array[index] = [key, value]
					break
				if self.array[index] == None:
					self.array[index] = [key, value]
					self.item_count += 1
					break
				index = (index + 1) % self.table_size

	def search(self, key):
		index = self.hash(key)

		if self.array[index][0] == key:
			return self.array[index][1]
		else:
			end = (index - 1) % self.table_size
			if self.array[end][0] == key:
				return self.array[end][1]
			index = (index + 1) % self.table_size
			while index != end:
				if self.array[index][0] == key:
					return self.array[index][1]
				else:
					index = (index + 1) % self.table_size
			raise KeyError(str(key) + " not found!")
```
#### Probability of Collision

Given 100 items, the probability of collision for:

- 23 items is ~50%
- 50 items is 97%
- 70 items is 99.9%


## Binary Search Trees

|             | Time Complexity              | Note |
|---          |---                      |---   |
| Worst Case: | **O(n)**    | Node trail could be linear |
| Best Case:  | **O(log n)**    | Equivalent to the height of a tree with N items

- Are binary trees where the items are arranged in a specific order
- Any item greater than a parent node is a right child, and any item less than a parent node is a left child
- If arranged this way, it makes searching for items easier as it only has to traverse through the nodes that are relevant
- When printed out using inorder traversal, it would show a sorted list
- Binary Search Trees can also be implemented as the underlying data structure of a _dictionary_ (due to key-value pairs and fast searching)

### Searching
1. Start at root node
2. If query is greater than current node value, go to right child, else go to left child
3. Repeat until found or no more nodes to traverse

### Inserting
1. Find the right spot (search)
2. If the item exists already, raise an exception
3. If not, insert a new node where it should be

### Deletion
1. Find the right key (search)
2. If it is a leaf, set the parent's reference to None
3. If it has one child, set the parent's reference to the child
4. If it has two children, find _successor_ (node with the next largest key). The successor takes the position of the deleted node. If the successor leaves an orphan child, link it to the successor's parent.

### Python Implementation
```python
class BinarySearchTreeNode:
    def __init__(self, key, item=None, left=None, right=None):
        self.key = key
        self.item = item
        self.left = left
        self.right = right
        
class BinarySearchTree:
    def __init__(self):
        self.root = None
        
    def is_empty(self):
        return self.root is None
        
    def __getitem__(self, key):
        return self.getitem_aux(self.root, key)
        
    def _getitem_aux(self, current, key):
        if current is None: # base case: empty
            raise KeyError("Key not found")
        elif key == current.key # base case: found
	         return current.item
	     elif key < current.key:
	         return self._getitem_aux(current.left, key)
	     else:
	         return self._getitem_aux(current.right, key)
	         
	 def insert(self, key, item):
	     self.root = self._insert_aux(self.root, key, item)
	     
	 def _insert_aux(self, current, key, item):
	     if current is None: # base case: at the leaf
	         current = BinarySearchTreeNode(key, item)
	     elif key < current.key:
	         current.left = self._insert_aux(current.left, key, item)
	     elif key > current.key:
	         current.right = self._insert_aux(current.right, key, item)
	     else: # key == current.key
	         raise ValueError("Duplicate Item")
	     return current
	     
	 def __setitem__(self, key, item):
	     self.root = self._insert_aux(self.root, key, item)
	     
	 def _setitem_aux(self, current, key, item):
	     if current is None: # base case: at the leaf
	         current = BinarySearchTreeNode(key, item)
	     elif key < current.key:
	         current.left = self._setitem_aux(current.left, key, item)
	     elif key > current.key:
	         current.right = self._setitem_aux(current.right, key, item)
	     else: # key == current.key
	         current.item = item
	     return current
	     
	 def __delitem__(self, key):
	     # left as an exercise
	     pass
```

## AVL Tree

|             | Time Complexity              | Note |
|---          |---                      |---   |
| Worst Case: | **O(log n)**    | No linear trails due to AVL property |
| Best Case:  | **O(log n)**    | Equivalent to the height of a tree with N items

- Are height-balanced binary search trees
- The left and right subtrees of every node _differ by at most one_
- Rebalancing is done to restore this property

### Balancing an AVL Tree

#### Left-Left Case

If a left subtree has a larger tree on its left:


