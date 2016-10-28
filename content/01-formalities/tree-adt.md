[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# The Tree ADT

### Definition

A `tree` can be empty (`nilTree`) or an element `e` that forks between two trees

```lisp
TYPES
    type tree = nilTree | fork e * (tree e) * (tree e) 
```

### Operations
   
```lisp
OPERATIONS
    empty : tree e -> boolean
    leaf : tree e -> boolean
    fork : e * tree e * tree e -> tree e
    left : tree e -> tree e
    right: tree e -> tree e
    contents : tree e -> e
```

### Functions

#### Height

Recursively defined; height equals 1 plus the height of the subtrees below.

``` lisp
height(nilTree) = 0
    | height(fork(e, TL, TR)) = 1 + max(height(TL), height(TR))
```

#### Weight

Also recursively defined; weight equals 1 plus the weights of every subtree as it forks.
  
``` lisp  
weight(nilTree) = 0
    | weight(fork(e,TL, TR)) = 1 + weight(TL) + weight(TR) 
```

#### Preorder Traversal

Root, then left subtree then right subtree

``` lisp
preorder(nilTree) = nil
	| preorder(fork(e,TL,TR)) = print(e), preorder(TL), preorder(TR)
```

#### Inorder Traversal

Left subtree, root, then right subtree

``` lisp	
inorder(nilTree) = nil
	| inorder(fork(e,TL,TR)) = inorder(TL), print(e), inorder(TR)
```

#### Postorder Traversal

Left subtree, right subtree, then root

``` lisp
postorder(nilTree) = nil
	| postorder(fork(e,TL,TR)) = postorder(TL), postorder(TR), print(e)
```
	
#### Breadth-first Traversal

Root is visited, then children, then grandchildren
	
``` lisp
breadthfirst(nilTree) = nil
	| ; left as exercise
```
