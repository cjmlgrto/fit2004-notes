[← Return to Index](https://github.com/cjmlgrto/fit2004-notes)

# Newton's Method

Another method of finding the roots of a function _f(x)_.

### Algorithm

1. Set n = 0 and make an initial guess, X<sub>0</sub>
2. Compute X<sub>n+1</sub> = X<sub>n</sub> - f(X<sub>n</sub>)/f'(X<sub>n</sub>)
3. If |X<sub>n+1</sub> / X<sub>n</sub> | < threshold
	- Return X<sub>n+1</sub>
4. Else, go to step 2

### Intuition

- h = X<sub>0</sub> - X<sub>1</sub>
- tan(θ) = f(X<sub>0</sub>)/h
- Tangent of a curve f(X) at a point X<sub>0</sub> is f'(X<sub>0</sub>)
- f'(X<sub>0</sub>) = f(X<sub>0</sub>)/h
- h = f(X<sub>0</sub>)/f'(X<sub>0</sub>) = X<sub>0</sub> - X<sub>1</sub>
- Hence, X<sub>1</sub> = X<sub>0</sub> - f(X<sub>0</sub>)/f'(X<sub>0</sub>)

### Limitations

Although Newton's method is a very powerful technique, and it converges on the root much faster than the Interval Bisection method:

- Calculating the derivative may be difficult or expensive
- The derivative may be 0 and will halt due to divison by 0
- May fail to converge
	- e.g. if f(x) = 1 - x<sup>2</sup> and initial guess is 0
