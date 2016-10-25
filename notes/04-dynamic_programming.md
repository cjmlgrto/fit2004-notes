[← Return to Index](/readme.md)

# Dynamic Programming

- Algorithms that break a large problem into smaller, solveable sub-problems
- And then combining the solutions of those sub-problems to solve the larger problem
- Combines recursion and divide-and-conquer strategies by working backwards:

### Strategy

1. Assume you already know the solutions to all the sub-problems
2. Observe how you can solve the original problem with the solutions of the sub-problems
3. Use the observations and iteratively solve the sub-problems and store the solutions

## Example: Fibonacci

Recursively, an algorithm to generate the Fibonacci sequence can be:

```python
def fib(N):
	if N == 0 or N == 1:
		return N
	else:
		return fib(N-1) + fib(N-2)
```

The problem with the above is that a lot of the sub-problems are duplicated. This causes the algorithm to run in O(2<sup>n</sup>) time. To save time, we can build a list of known solutions and store them. The following takes O(n) time:

```python
def fib(N):
	sequence = [-1] * N
	sequence[0], sequence[1] = 0, 1
	return fib_aux(sequence, N)

def fib_aux(sequence, N):
	if sequence[N] != -1:
		return sequence[N]
	else:
		sequence[N] = fib_aux(sequence, N-1) + fib_aux(sequence, N-2)
		return sequence[N]
```

## Example: Coins Change

A country uses `n` coins with denominations `{a1, a2, ... , aN}`. Given a value `V`, find the minimum number of coins that add up to `V`.

Suppose the coins are `{1, 5, 10, 50}` and the value `V` is `110`. The solution is two 50 coins and one 10 coin.

```python
def min_coins(V, coins):
	memo = [float('inf')] * V
	for v in range(1, V):
		minCoins = float('inf')
		for i in range(1, V):
			if coins[i] <= v:
				c = 1 + memo[v - coins[i]
				if c < minCoins:
					minCoins = c
		memo[v] = minCoins
```

## Example: Subset Sum Problem

Given a set of numbers `N = {a1, a2, ..., aN}` and a value `V`, is there a subset of numbers in `N` that equals `V`? And if so, what is it?

```python
def subset_sum(N, T):
	results = [ [0] * (T + 1) for _ in range(len(N) + 1) ]
	for i, l in enumerate(N):
		i += 1
		for d in range(T + 1):
			if l > d:
				results[i][d] = results[i - 1][d]
			else:
				a = results[i - 1][d]
				b = results[i - 1][d - l] + l
				results[i][d] = max(a, b)
	sum = results[len(N)][T]
	subset = []
	i, j = len(N), T
	while i > 0:
		if results[i][j] != results[i - 1][j]:
			meta = (i, N[i - 1])
			subset.append(meta)
			j -= N[i - 1]
		i -= 1
	subset.reverse()
	return subset, sum
```

## Example: Edit Distance

Given two strings, `s1` and `s2`, what is the minimum number of 'edits' to turn `s1` into `s2`?

A 2-dimensional matrix, `m`, that's `|s1|` in length and `|s2|` in height can be used to store the edit distance from the `i`-th character of `s1` to the `j`-th character of `s2`. Thus, we can construct the table as follows:

- `m[0,0] = 0`
- `m[i,0] = i,  i=1..|s1|`
- `m[0,j] = j,  j=1..|s2|`
- `m[i,j] = min(m[i-1,j-1]
             + if s1[i]=s2[j] then 0 else 1 fi,
             m[i-1, j] + 1,
             m[i, j-1] + 1 ),  i=1..|s1|, j=1..|s2|`
             
And `m[i,j]` can be computed row-by-row. Overall, this takes O(nm) complexity.

## Hirschberg's Algorithm (Edit Distance in O(n + m) time)

Given two strings, `s1` and `s2`:

1. Split `s1` into half. Call it `s1A` and `s1B`
2. Call edit distance algorithm on `s1A` and `S2` maintaining only last two rows
3. Call edit distance algorithm on `reverse(s1B)` and `reverse(s2)`, maintaining only last two rows
4. Sum up the elements of the last rows for both edit distance calls and choose the cell with minimum sum as the cut point
5. Divide `s2` into `s2A` and `s2B` based on this cell
6. Recursively call this algorithm given paramters (s1A, s2A) and (s1B, s2B)


	


	
	