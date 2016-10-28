[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Binary Search Trees

|             | Time Complexity              | Note |
|---          |---                      |---   |
| Worst Case: | **O(n)**    | Node trail could be linear |
| Best Case:  | **O(log n)**    | Equivalent to the height of a tree with N items

### Properties

- Are binary trees where the items are arranged in a specific order
- Any item greater than a parent node is a right child, and any item less than a parent node is a left child
- If arranged this way, it makes searching for items easier as it only has to traverse through the nodes that are relevant
- When printed out using inorder traversal, it would show a sorted list
- Binary Search Trees can also be implemented as the underlying data structure of a _dictionary_ (due to key-value pairs and fast searching)

### Algorithm

#### Searching
1. Start at root node
2. If query is greater than current node value, go to right child, else go to left child
3. Repeat until found or no more nodes to traverse

#### Inserting
1. Find the right spot (search)
2. If the item exists already, raise an exception
3. If not, insert a new node where it should be

#### Deletion
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
