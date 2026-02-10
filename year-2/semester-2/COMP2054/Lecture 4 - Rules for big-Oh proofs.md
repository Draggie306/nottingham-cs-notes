
REMINDER:

![[../../../Images/Pasted image 20260209130432.png]]



## Multiplication Rule

Supposing:
- f1(n) is O( g1n) )
- f2(n)

If we have 2 functions, multiplying them together results in a big-O of the product of the functions. f1(n) f2(n) is O( g1(n) g2(n) )


## Drop smaller terms

When h(n) goes to 0 as n becomes large, then f(n) is O(1).

### Examples

Big-Oh of $f(n) = n^2 + n$:

- $f(n) = n^2 * ( 1 + \frac{1}n )$ 
- $1 + 1/n$ is $O(1)$ by "drop small terms". $N^2$ is trivially $O(n^2)$
- When n becomes massive, 1 does not matter.
- Using the multiplication rule, $F(n) = O(n^2 * 1 ) = O(n^2)$


After some thought, it should become clear that if $f(n)$ is a polynomial of degree $d$, then $f(n)$ is $O(n^d)$. This firstly drops lower-order terms, then drops constant terms. The degree of a polynomial is the highest power, e.g. $5 n^4 + 3 n^2$ is degree 4, so will be $O(n^4)$

### Exponents vs powers vs logs

Exponents grow faster than any power law: $\frac{b^n} {n^k}$ will go to infinity; $\frac{n^k} {b^n}$ goes to zero. 

Equally, powers grow faster than any power of a log:

- n / (log n) -> infinity
- (log n) / n -> zero