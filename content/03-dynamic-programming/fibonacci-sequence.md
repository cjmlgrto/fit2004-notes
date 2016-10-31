[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Fibonacci Sequence

### Problem

Generate the n-th Fibonacci number.

### Solution 1: Recursively

```python
def fib(n):
	if n == 0 or n == 1:
		return 1
	else:
		return fib(n-1) + fib(n-2)
```

Although the above implemention is elegant, it's a very expensive algorithm. For any n, it will take up to O(2<sup>n</sup>) recursive calls, and at times, may re-compute a recursive call that's already been computed before.

### Solution 2: Using Dynamic Programming

Dynamic Programming is the practice of using the answers of smaller subproblems to build the answer of a much bigger, similar problem. This not only makes an algorithm run _very slightly_ more efficient, but can reduce repeated computations by **storing previously computed answers** and then **accessing them in constant time when needed**.

#### Algorithm

1. Create a list `F = [None] * n` that will store our computational results
2. Iterate through the list, building up to our `n`-th item
3. Access the item at the end to get our answer

#### Python Implementation

```python
def fib(n):
	F[0] = 0
	F[1] = 1
	F[2] = 1
	for i in range(2,n-1):
		F[i] = F[i-1] + F[i-2]
	return F[n-1]
```

