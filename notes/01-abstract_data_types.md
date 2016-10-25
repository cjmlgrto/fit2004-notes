[← Return to Index](/)

# Abstract Data Types

- Mathematical model for a structure of information, composed of a **definition**, some **operations**, **rules** and **functions**.
- Used because it makes constructing algorithms easier
- Also used because ADTs have expected behaviours and properties that stay consistent no matter how it's implemented in code

## Lists

### Definition

A list of elements of type `e` is (`=`) either empty (`nil`) or (`|`) is constructed (`cons`) using an element of type `e` and (`*`) a list.

```lisp
TYPES
    type list e = nil | cons(e * (list e))
```

### Operations

```lisp
OPERATIONS
    isNull : list e -> boolean
    head : list e -> e
    tail : list e -> list e
    cons : e * (list e) -> list e
```

### Rules

```lisp
RULES
    isNull(nil) = true
    isNull(cons(h, T)) = false
    head(cons(h,T)) = h
    head(nil) = error
    tail(cons(h,T)) = T
    tail(nil) = error
```

### Functions

```lisp
length(nil) = 0 
    | length(cons(h,T)) = 1 + length(T)

append(nil, L2) = L2
    | append(L1, L2) = append(cons(h1,T1),L2)
                   = cons(h1, append(T1, L2))

;COMMENT: L1, L2 are two lists.
                         
merge(nil, nil) = nil
	; produces a sorted list if |L1| & |L2| not nil
    | merge(nil, L1) = L1
    | merge(L1, nil) = L1
    | merge(L1, L2) = 
    if head(L1) < head(L2) then
        cons(head(L1), merge(tail(L1), L2))
    else
        cons(head(L2), merge(L1, tail(L2))
        
reverse(nil) = nil
    | reverse(cons(h,T) = append(reverse(T), cons(h,nil))
```

## Trees

### Definition

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

``` lisp
height(nilTree) = 0
    | height(fork(e, TL, TR)) = 1 + max(height(TL), height(TR))
    
weight(nilTree) = 0
    | weight(fork(e,TL, TR)) = 1 + weight(TL) + weight(TR) 

preorder(nilTree) = nil
	| preorder(fork(e,TL,TR)) = print(e), preorder(TL), preorder(TR)
	
inorder(nilTree) = nil
	| inorder(fork(e,TL,TR)) = inorder(TL), print(e), inorder(TR)
	
postorder(nilTree) = nil
	| postorder(fork(e,TL,TR)) = postorder(TL), postorder(TR), print(e)
	
breadthfirst(nilTree) = nil
	; root is visited, then children, then grandchildren etc
```
