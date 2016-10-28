[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Calculating Integrals

## Rectangle Rule

- Divide the range `[a,b]` in N equal width rectangles
- Let m be the midpoint along the width of a rectangle
- Its height is then f(m)
	- This height can be negative, and as such, results in a negative area
- Add the areas of all rectangles
- Larger N results in better approximation

### Pseudocode

```
width = (b-a)/N
area = 0
for i = 0 to N-1:
	mid = a + (i+0.5)*width
	height = f(mid)
	area += height*width
return area
```

## Trapezoidal Rule

- Use trapezoids instead of rectangles
- Are of trapezoid with width `w` and side lengths `u` and `v`:
	- = `wv + 0.5w(u-v)`
	- = `wv + 0.5wu - 0.5wv`
	- = `0.5wv + 0.5wu`
	- = `0.5w(u+v)`

### Pseudocode

```
width = (b-a)/N
area = 0
for i = 0 to N-1:
	start = a + i*width
	u = f(start)
	v = f(start + width)
	area += 0.5*w*(u+v)
return area
```