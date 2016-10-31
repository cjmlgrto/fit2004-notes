[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Coins Change Problem

### Problem

Given a set of coins, `C = {2,3,5,7}` and a value `V = 10`, what is the minimum number of coins I can form from `C` to make `V`?

### Solution

Use existing solutions to build up an answer! (A really good video explanation [here](https://www.youtube.com/watch?v=NJuKJ8sasGk)).

#### Algorithm

1. Create a list `T = [∞] * V`
2. For every coin `j` in the range `0..len(C)`:
	- For every slot `i` in the range `0..len(T)`:
		- Set the `i`-th item of T to be the minimum of:
			1. What's currently there
			2. OR `1 + T[i - C[j]]`— aka the item that's `C[j]` positions below the current slot, +1
3. The value in position `T[V]` is the minimum number of coins required (but does not report _which_ coins to take!)

#### Python Implementation

```python
C = [2,3,5,7]
V = 10


def coins_change(C, V):
	# Create a list of size V full of infinity
	T = [float('inf')] * V
	
	for j in range(len(C)):
		for i in range(len(T)):
			current = T[i]
			previous = T[i - C[j]]
			T[i] = min(current, 1+previous)
	
	return T[V]
```

