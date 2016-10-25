[← Return to Index]()

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
length function
    length(nil) = 0 
    | length(cons(h,T)) = 1 + length(T)

append function
    append(nil, L2) = L2
    | append(L1, L2) = append(cons(h1,T1),L2)
                   = cons(h1, append(T1, L2))

;COMMENT: L1, L2 are two lists.
                         
merge function
	; produces a sorted list if |L1| & |L2| not nil
    merge(nil, nil) = nil
    | merge(nil, L1) = L1
    | merge(L1, nil) = L1
    | merge(L1, L2) = 
    if head(L1) < head(L2) then
        cons(head(L1), merge(tail(L1), L2))
    else
        cons(head(L2), merge(L1, tail(L2))
        
reverse function
    reverse(nil) = nil
    | reverse(cons(h,T) = append(reverse(T), cons(h,nil))
```

