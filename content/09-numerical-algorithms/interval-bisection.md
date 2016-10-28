[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Interval Bisection

An algorithm similar to Binary Search that finds the roots of a function _f(x)_.

### Algorithm

1. Assuming _f(x)_ is continous, select a range `[lo,hi]` such that f(`lo`) has an opposite sign to f(`hi`)
2. Get the midpoint as `mid = (lo + hi)/2` and compute f(`mid`)
3. If f(`mid`) = 0, then we've found a root
4. Otherwise, set `mid` as the new `lo` or `hi` and repeat
	- `mid` is `lo` if it has the same sign as `lo`, else `hi`

### Pseudocode

```
loSign = getSign(f(lo))
while (hi-lo)/2 > threshold		# limit iterations to prevent infinite loop
	mid = (lo + hi)/2
	midSign = getSign(f(mid))
	if midSign == 0:
		return mid
	else if midSign == loSign:
		lo = mid
	else:
		hi = mid
```

