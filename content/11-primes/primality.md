[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Primality

Prime numbers, yo.

### Primality Test:

- Given a number (arbitarily long) as input, is this number a prime?
- Reliance on primes by modern crypto-systems (e.g. RSA) makes primality testing an important problem

### Naive Primality Test

```
for i = 2 to N-1:
	if N % i == 0:
		return False
return True
```

- The above costs O(N) division operations.
- Assuming the input is N, which is M digits long, the complexity would be:
	- M = log N, which then becomes N = 2<sup>M</sup>. Thus, the cost is O(2<sup>M</sup>)
- This means we can change `for i = 2 to N-1` to `for i=2 to sqrt(N)`

```
for i = 2 to sqrt(N):
	if N % i == 0:
		return False
return True
```