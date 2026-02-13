## Big-Omega

> For 2 positive functions, f(n) and g(n) of a single variable (n), then f is Big-Omega of g if and only if there exists a constant c > 0 and $n_0 >= 1$ such that:
> forall n $\ge$ $n_0$. f(n) $\ge$ c g (n)

Compared to big-Oh, this is greater than or equal, rather than less than or equal. 

It is important that c must be constant, and not depend on `n`. 

Need to show there is a constant c and an n0 such that $n \ge c \space n$ forall n $\ge n_0$ 

> Is it true that 1 is $\Omega (n)$  ? Exercise.

Big-Omega expresses "grows as least fast as", whereas O expresses "grows as most as fast as".

$n^3 - n$ is $\Omega (n^3)$ means $n^3-n$ grows as least as fast as $\Omega (n^3)$ 

### Uses
If the worst case is hard to determined, we can say it is no better than $\Omega(n^3)$ and no better than $O(n^4)$. Nothing to do with the best case - only to do with functions. It is more flexible than ratios. 


## Big-Theta
To remember these: the theta has a bar across the middle, which looks like the bar in the equals sign.

$f is \Theta$ of $g$ if there exist constants $c1$ and $c2 > 0$, and $n_0 \ge 1$ such that $\forall n \ge n_0$. $f(n \le c1 \space g(n))$ AND $f(n) \ge c2 \space g(n)$ 

It is nothing other than saying it is Big-Oh and Big-$\Omega$. It expresses "grows 'exactly' as fast as". **The caveat is that exactly ignores constants**. 

It allows flexibility to express growth rate but does not sandwich the specific values - very useful. **Many people mean Big-Theta when they say Big-Oh.**

It is reflexive and transitive as the others, and also symmetric. It is an equivalence relation. 

## Little-Oh
"definitely grows not as fast as"


