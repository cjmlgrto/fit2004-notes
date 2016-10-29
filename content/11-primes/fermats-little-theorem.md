[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Fermat's Little Theorem

- If p is a prime, then for any integer 1 < a < p, a<sup>p-1</sup>-1 is an integer multiple of p
	- a<sup>p-1</sup>-1 mod p = 0
- This, we can guarantee that N is composite if a<sup>N-1</sup>-1 mod N ≠ 0
- However, if it = 0, we cannot guarantee that N is prime

### Pseudocode

```
repeat k times:
	a = any random number between 2 and N-1
		if a^(N-1) mod N != 0:
			return False
return Maybe
```

