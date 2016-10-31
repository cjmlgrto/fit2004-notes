[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Edit Distance Problem

### Problem

Given a string `S = GATCAC` and another string `T = GTCACC`, what is the minimum number of additions/deletions/substitutions required to convert `S` to `T`?

### Solution

Build up a bank of solutions based on substrings that eventually increase to both strings. (Dynamic Programming— and a video [here](https://www.youtube.com/watch?v=We3YDTzNXEk).)

|   |   | G | A | T | C | A | C |
|---|---|---|---|---|---|---|---|
|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| G | 1 | 0 | 1 | 2 | 3 | 4 | 5 |
| T | 2 | 1 | 1 | 1 | 2 | 3 | 4 |
| C | 3 | 2 | 2 | 2 | 1 | 2 | 3 | 
| A | 4 | 3 | 2 | 3 | 2 | 1 | 2 |
| C | 5 | 4 | 3 | 3 | 3 | 2 | 1 |
| C | 6 | 5 | 4 | 4 | 3 | 3 | **2** |

### Algorithm

It's very mechanical:

1. Build a table `E` of size |S+1| × |T+1|
2. Fill the first row with the numbers 1 to |S|
3. For every row `i` (skipping the first row):
	- For every column `j`:
		- If `T[i] = S[j]`— that is, if the characters are the same:
			- Set `E[i][j]` = `E[i-1][j-1]`
		- Otherwise, set it to the minimum of either:
			- `E[i-1][j-1]` (one cell up and left)
			- `E[i][j-1]` (one cell left)
			- `E[i-1][j]` (one cell up)
4. Return the bottom-right-most value as the edit distance

The key technique is:

| A | B |
|---|---|
| **C** | `= min(A,B,C)` |

Otherwise, just **A** if the character is the same.

#### Python Implementation

```python
def edit_distance(S,T):
	E = [ [None for char in range(len(S)+1)] ] * (len(T) + 1)
	
	for i in range(len(S)):
		E[0][i] = i
	
	for i in range(1,len(S)):
		for j in range(len(T)):
			if S[i] = T[j]:
				E[i][j] = E[i-1][j-1]
			else:
				a = E[i-1][j-1]
				b = E[i][j-1]
				c = E[i-1][j]
				E[i][j] = min(a,b,c)
	
	return E[len(S)][len(T)]

```