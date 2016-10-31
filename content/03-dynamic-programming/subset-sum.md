[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Subset Sum Problem

### Problem

Given a set, `S = {2,3,5}` and a value `V = 7`, is there a subset of `S` whose sum equals `V`?

### Solution

Dynamic Programming. Here is a [good video explanation](https://www.youtube.com/watch?v=s6FhG--P7z0).

|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 |
|---|---|---|---|---|---|---|---|---|
| 2 | T | F | T | F | F | F | F | F |
| 3 | T | F | T | T | F | T | F | F |
| 5 | T | F | T | T | F | T | F | **T** |

Every item in the row answers the question: _“given myself and the rows before me, can I build up a sum equal to the **column** above?”_

For example, the second-last row considers if it's possible to build up the sums from 1 through to 7, if the set was just `S = {2,3}`. Every new row adds an item to the set.

**Key idea**: instead of checking every cell if the sum is possible every time, we just use pre-existing values. We can just say that _a sum is possible (True) **if** the item 1 row back and `sum` columns back is also True_. That is:

`Table[i][j] = Table[i-1][j-sum]`


#### Algorithm

1. Initialise a table `P` of size `len(S) * V`
2. Set the entire first column to **True** (this just means that a 0 sum is always possible)
3. For every row (for every `item` in the set `S`):
	- For every column (`sum`):
		- For the very first row only: If the `sum` < `item`, set it to **False**
		- Check the value of the cell directly above it, and directly above it with `sum` rows back
			- If either is true, set it to **True**— else **False***
4. The item in the bottom-right-most position will say if the subset sum is possible or not.

#### Python Implementation

```python
def subset_sum(S,V):
	P = [[None for sum in range(V)]] * len(S)
	
	for i in range(len(S)):
		P[i][0] = True
		
	for i in range(V):
		for j in range(len(S)):
			sum = S[j]
			if P[i-sum][j-1] is True or P[i][j-1] is True:
				P[i][j] = True
			else:
				P[i][j] = False
				
	return P[len(S)][V]
```