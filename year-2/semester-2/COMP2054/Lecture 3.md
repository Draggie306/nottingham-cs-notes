f(n) is O ( g(n)) if and only if there exist constants c >= 1 and n0 >= 1 such that forall n >= n0 .
f(n) <= c g (n)

f(n) = 1 is O(n) - we have 1 is O(n) and 1 is O(1)

$L \exists \forall N$

### Examples 

Despite two cases "even and odd", the definition requires one $c$ and one $n_0$. 

Consider: 

f2(n) = n    if n is even, 4 if n is odd

if n $\ge$ 4 then f2(n) $\le$ n - therefore, we can take $c = 1$ and $n_0 = 4$ 


### Exercises
- (3n-6) is O( (4n+5) )
- (3n-6) is O( n )
- (4n+5) is O( n )

- Q1: Show 7n-2 is O(n) 
- Q2: Show 3n3 + 20n2 + 5 is O(n3 ) 
- Q3: Show 3 log n + 5 is O(log n)


Plotting Big-Oh on a log-log plot can be more useful with n squared being straight 


n is a member of a set which has the name O(n). O(n) is a set of functions, and f(O(n)) then f is in the set of O(n)

> Any function bounded by a constant is bounded by n.

Many texts use f = O(n) but this is not liked: if 1 = O(1) and 1 = O(n) then O(1) = O(n) - **but this is wrong**.







