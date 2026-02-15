
## Big-Oh Definition
Given positive functions $f(n)$ and $g(n)$, we can say that $f(n) \text{ is } O(g(n))$ if and only if there exists positive constants $c$ and $n_0$ (we choose these ourselves) such that $f(n) \leq c \cdot g(n), \forall n \geq n_0$.

$f(n) = g(n)$ such that $f(n) <= c . g(n) \forall n >= n_0$  


Prove that 2n + 1 is O(3n):

Start:
1. f(n) <= c . g(n)  f(n) >= n0

Substitute values: 
1. $2n + 1 \ge c . 3n$ and $f(n) \ge n_0$
Remove 2n on both sides:
2. $1 \ge c. 3n - 2n$
Factor out the n:
3. $1 \ge n(C3 - 2)$ 
Choose:
4. $1 \ge n, \forall n \ge n_0$ - $n_0$ can be 1, so this holds.


Prove than $n^2$ is $O(2n^2)$:

Start: 
1. $f(n) \le c . g(n)$ and $f(n) \ge n_0$
Substitute values:
2. $n^2 \le c . 2n ^2$ $\forall$ $n \ge n_0$
3. $0 <= c.2n^2 - n^2$
4. $0 \le n^2(2c - 1)$
Choose c = 1, substitute:
5. $0 \le n^2(1)$
By definition, choose an n0 - here, it can be any value. Choose 1:
6. $0 \le1^2(1)$
This holds!

Prove that $n^2 - 5n$ is $O(n^2)$ 













