[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Complexity

| Class | Big O | Example |
|---    |---    |---      |
| Constant | O(1) | Adding two numbers |
| Logarithmic | O(log n) | Binary Search | 
| Linear | O(n) | Linear Search |
| Super-linear | O(n log n) | Merge Sort |
| Quadratic | O(n<sup>2</sup>) | Selection Sort |
| Exponential | O(2<sup>n</sup>) | Brute force for **n** items |
| Factorial | O(n!) | Generating permutations of **n** items |

### Time and Space

- The **time** complexity of an algorithm is found to determine how long an algorithm would take depending on an arbitrary input of size *N*
- The **space** complexity is found to determine how much memory an algorithm requires

### Complexities and Recurrence Relations

- An algorithm's complexity may be expressed through a **recurrence relation**
- For example, the recurrence relation of merge sort can be defined as `T(1) = a or T(N) = T(N/2) + b`, where `N` is the input size, and `a` & `b` are constants

#### Solving Recurrence Relations

1. Iterate recursively over the given definition
2. Once an iterative version is found, solve for the base case definition
3. Remove constants to convert to Big O notation