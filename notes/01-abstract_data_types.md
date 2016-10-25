[← Return to Index]()

# Abstract Data Types

- Mathematical model for a structure of information, composed of a **definition**, some **operations**, **rules** and **functions**.
- Used because it makes constructing algorithms easier
- Also used because ADTs have expected behaviours and properties that stay consistent no matter how it's implemented in code

## Lists

### Definition

```lisp
TYPES
    type list e = nil | cons(e * (list e))
```