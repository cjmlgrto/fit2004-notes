[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)


# AVL Trees

|             | Time Complexity              | Note |
|---          |---                      |---   |
| Worst Case: | **O(log n)**    | No linear trails due to AVL property |
| Best Case:  | **O(log n)**    | Equivalent to the height of a tree with N items

### Properties

- Are height-balanced binary search trees
- The left and right subtrees of every node _differ by at most one_
- Rebalancing and _rotation_ is done to restore this property

## Rotations

The following has been adapted from [John Hargrove's super easy-to-read tutorial sheet](https://www.cise.ufl.edu/~nemo/cop3530/AVL-Tree-Rotations.pdf).

### Left-Left Rotation (LL)

```
A
 \
  B
 / \
b   C

```

1. `B` becomes the new root
2. `B`'s left child becomes `A`'s right children
3. `A` becomes `B`'s left child

```
  B
 / \
A   C
 \
  b
```

### Right-Right Rotation (RR)

```
    A
   /
  B
 /
C
```

Same as above, but mirrored:

1. `B` becomes the new root
2. `B`'s right child (in this case, none) becomes `A`'s left children
3. `A` becomes `B`'s right child

```
  B
 / \
A   C
```

### Left-Right Rotation (LR)

```
A
 \
  C
 /
B
```

1. RR the `C-B` subtree
2. LL Rotate

```
A
 \
  B
   \
    C
```
```
  B
 / \
A   C
```

### Right-Left Rotation (RL)

```
  A
 /
C
 \
  B
```

Same, but mirrored:

1. LL the `C-B` subtree
2. RR Rotate

```
    A
   /
  B
 /
C
```
```
  B
 / \
A   C
```

### Pseudocode for Rotations

```pseudocodeIF tree is right heavy{  IF tree's right subtree is left heavy  {     Perform Double Left rotation  }ELSE {     Perform Single Left rotation  }}ELSE IF tree is left heavy{  IF tree's left subtree is right heavy  {     Perform Double Right rotation  }ELSE {     Perform Single Right rotation  }}
```
### Python Implementation

The following code has been adapted from [here](http://blog.coder.si/2014/02/how-to-implement-avl-tree-in-python.html).

```python
class Node:
	def __init__(self, key):
		self.left = None
		self.right = None
		self.key = key

	def __str__(self):
		return str(self.key)

class AVLTree():
	def __init__(self):
		self.node = None
		self.height = -1
		self.balance = 0

	def insert(self, key):
		n = Node(key)
		if self.node == None:
			self.node = n
			self.node.left = AVLTree()
			self.node.right = AVLTree()
		elif key < self.node.key:
			self.node.left.insert(key)
		elif key > self.node.key:
			self.node.right.insert(key)

		self.rebalance()

	def rebalance(self):
		self.update_heights(recursive=False)
		self.update_balances(False)

		while self.balance < -1 or self.balance > 1:
			if self.balance > 1:
				if self.node.left.balance < 0:
					# LR Case
					self.node.left.rotate_left()
					self.update_heights()
					self.update_balances()
				# LL Case
				self.rotate_right()
				self.update_heights()
				self.update_balances()

			if self.balance < -1:
				if self.node.right.balance > 0:
					# RL Case
					self.node.right.rotate_right()
					self.update_heights()
					self.update_balances()
				# RR Case
				self.rotate_left()
				self.update_heights()
				self.update_balances()

	def update_heights(self, recursive=True):
		if self.node:
			if recursive:
				if self.node.left:
					self.node.left.update_heights()
				if self.node.right:
					self.node.right.update_heights()
			self.height = 1 + max(self.node.left.height, self.node.right.height)
		else:
			self.height = -1

	def update_balances(self, recursive=True):
		if self.node:
			if recursive:
				if self.node.left:
					self.node.left.update_balances()
				if self.node.right:
					self.node.right.update_balances()
			self.balance = self.node.left.height - self.node.right.height
		else:
			self.balance = 0

	def rotate_right(self):
		new_root = self.node.left.node
		new_left_sub = new_root.right.node
		old_root = self.node
		self.node = new_root
		old_root.left.node = new_left_sub
		new_root.right.node = old_root

	def rotate_left(self):
		new_root = self.node.right.node
		new_left_sub = new_root.left.node
		old_root = self.node
		self.node = new_root
		old_root.right.node = new_left_sub
		new_root.left.node = old_root

	def delete(self, key):
		if self.node != None:
			if self.node.key == key:
				if not self.node.left.node and not self.node.right.node:
					self.node = None
				elif not self.node.left.node:
					self.node = self.node.right.node
				elif not self.node.right.node:
					self.node = self.node.left.node
				else:
					successor = self.node.right.node
					while successor and successor.left.node:
						successor = successor.left.node

					if successor:
						self.node.key = successor.key
						self.node.right.delete(successor.key)
			elif key < self.node.key:
				self.node.left.delete(key)
			elif key > self.node.key:
				self.node.right.delete(key)

			self.rebalance()

	def inorder_traverse(self):
		result = []
		if not self.node:
			return result
		result.extend(self.node.left.inorder_traverse())
		result.append(self.node.key)
		result.extend(self.node.right.inorder_traverse())

		return result

tree = AVLTree()
data = [1,2,3,4,5,6,7,8,9]

for key in data:
	tree.insert(key)
print tree.inorder_traverse()
```

