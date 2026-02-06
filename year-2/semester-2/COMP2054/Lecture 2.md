Counting steps (primitive operations) is inaccurate. We may get different values, depending on the compiler and hardware. 

Computer Science needs a way to group functions by their scaling behaviour as $n$ increases. Therefore, classifications should:
- Remove unnecessary details 
- Be relatively quick and easy
- Handle ”weird” functions that can happen for runtimes
- Still be mathematically well-defined. 

**This is best done by the Big-Oh notation and family.**
- O (big-Oh)
- (big-omega)
- (Big-Theta)
- o (little-oh)
- (little-omega)

Stirling’s approximation: $l \space n( n! ) = n \space ln \space n - n + O( ln \space n )$ , where ln is the natural logarithm (log base e). **There is no reference to an algorithm.**

- It is possible to say ”the best case of algorithm X is O(n log n)”

We are just talking about functions $f(n)$ of a single parameter $n$. 

### Definitions
Big-Oh is intended for functions of positive integers (size) that are positive real values. 

$$f \space is \space O(g) \iff \exists c . \space \exists n_0 \space [ \space \forall n \ge n_0. (f(n) \lt c g (n))\space] $$

The quantifier must be in order $\exists \exists \forall$: pick $c$, then pick $n0$. 


### Examples

Showing f(n) = 1 is O(1):
1. Pick $c$ - *the reasonable smallest one to make life easy.*
2. Pick $n0$ such that 1 <= c 1 for all n >= n0:
	- c = 1
	- n0 = 1
- This works 

Showing that f(n) = 1 is O(n):
1. Picking $c, n0$ such that 1 <= c n forall n >= n0
2. n0 = 1, c = 1 - need $1 \le n \space \forall n \ge 1$
3. Done: 1 is O(n)

















