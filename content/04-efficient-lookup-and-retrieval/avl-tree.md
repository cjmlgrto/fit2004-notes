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


