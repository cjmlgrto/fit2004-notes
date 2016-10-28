[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Correctness

An algorithm is _correct_ if it:

- It **terminates**
- And always **gives expected results** on termination

We can prove that an algorithm is correct by first checking to see if the algothim _doesn't run into an infinite loop_, and then checking to see if the output is as expected every time it ends.


### Loop Invariants

**Loop Invariants** (LI) are facts that are true _before_ and _after_ a program loop. They can be used in constructing algorithms, or used to prove if an algorithm is correct.

#### Example: Find Minimum

Let's say we already know that the algorithm below always terminates. We just have to prove that, whenever it ends, the algorithm always gives the expected result: to return the smallest item of a list.

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