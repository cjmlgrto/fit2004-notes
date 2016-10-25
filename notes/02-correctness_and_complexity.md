[← Return to Index](/readme.md)

# Correctness and Complexity

## Correctness

### Proving an algorithm's correctness

- The strategy is to first prove that the algorithm *always terminates*
- Then prove that on termination, the *results are correct*

### Loop Invariants

- Are facts that are true *before* and *after* the execution of a loop
- Can be used to prove the correctness of an algorithm

#### Example: Find Minimum

```python
def find_min(L):
	min = L[0]
	index = 1
	// HERE
	while index <= len(L):
		if L[index] < min:
			min = L[index]
		index += 1
	// HERE
	return min
```

In the above code, the invariants in the places marked `// HERE` are:

- `min` holds the smallest item from `L[0..index]`
- `index` is always increasing

We can use the above facts to show that the program is correct on termination:

- `index` increases until it reaches the length of the list
- `min` holds the smallest item in the sublist `L[0..index]`
- As `index` approaches `len(L)`, we see that the size of the sublist increases to `len(L)`
- Thus, at the end, `min` holds the smallest item in the sublist `L[0..len(L)-1]`, which is essentially the smallest item in `L`

## Complexity

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


