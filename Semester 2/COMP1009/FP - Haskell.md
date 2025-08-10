
## About functional programming
Functional programming is declarative. It declares what we want to achieve, rather than how to achieve it. Explicit data is given to functions, with no implicit data, which means there is more predictability and reliability.

No worries about speed and efficiency. The values of data don’t change, but may create new copies rather than changing existing ones like with recursion. 

> It’s not a natural way of thinking about problems

## About Haskell
Many ideas from functional programming go back to the early days of computers.

Generally, a functional programming is a style of programming in which the basic method of computation is the application of functions to arguments. A functional language is one that supports and encourages the functional style.

Summing the integers 1 to 10 in Haskell:
```haskell
sum [1..10]
```

Turing machines: imperative/state-based machines
Lambda calculus: Alonzo Church

1960: ISWIM - no variable assignments, the first pure functional language

The Haskell Report, after 15 years after created, was made in 2003 to ensure it remains a beautiful language with standards.

## Syntax
Square brackets in Haskell are lists of things


`[1,2,3,4]` - same type inside separated by commas
`[]` - empty list
`[1]` - singleton list

`++` - append/concatenation from list:
- `[1,2,3] ++ [4,5]` = `[1,2,3,4,5]`

`:` - takes a single element and adds it to the start
`::` - has type

`<-` - drawn from a list, i.e. 

#### Standard Prelude
Haskell comes with a large number of standard library (the "Standard Prelude").

> Many of the standard functions operate on lists (values of the same type enclosed in square brackets).

**head** selects the first element from the list:
`head [1,2]` = 1

`last [1,2]` = 2

**tail** removes the first element from the list - and returns the rest.
`tail [1,2,3]` - returns `[2,3]`

To select an element at an index, we use the **double bang** `!!`
`[1,2,3,4,5] !! 2` - outputs `3`.


**take** will return the first N elements of a list.
`take 3 [1,2,3,4,5]` - outputs `[1,2,3]`

**drop** removes the first n elements from a list:
`drop 3 [1,2,3,4,5]` = `[4,5]`

**length** returns the length of a list.
`length [1,2,3,4,5]` = `5`

`sum` adds all elements in a list (of an empty list, it is zero)

`product` gives the product of a list of numbers (of empty, is 1).

To append two lists, we can do: `[1,2,3] ++ [4,5]`

`init` removes the last element from a list (the **init**ial segment)

### Function application
In maths, function application is denoted with round brackets, with commas separating the arguments.

In Haskell, function application is denoted using a space, with function arguments separated by spaces, and multiplication with `*`.
`f a b + c*d` means `f(a+b) + cd`

Function application has higher priority than all other operators - `f a + b` means `(fa) + b`.


![[Pasted image 20250131141651.png]]


#### Naming requirements
Capital letters are reserved for types, so starting with lower case are reserved for function and argument/variable names.
By convention, list arguments usually have an `s` suffix on their name, so if the argument is `x` then the list arg would be `xs`. If it has 2 s on the end then it will likely be a list of lists e.g. `xss`.

#### The layout rule
The layout rule avoids the need for explicit syntax to indicate the grouping of definitions with curly brackets. Similar to Python:.

has type of:

`False :: Bool`


### Types and classes
A type is a name for a collection of related values. The basic type `Bool` contains the two logical values `False` and `True`.

The point of types largely is to detect errors in programs. Applying a to arguments of a wrong type is called a type error.

#### Type safety
All **type errors are found at compile time**, meaning Haskell is a strongly-typed language. These types of languages are safer and faster: there is no need for type checks at runtime as there are no type errors at runtime. 

The `:type` command calculates the type of an expression without evaluating it.

`:type not False`
`not False :: bool`
This does not evaluate the expression `not False`, but will work out through the type inference system that it is a boolean. 

#### Type Notation
If the expression `e` produces a value of type `t`, then `e` has type `t`. This is written as `e :: t`.

#### Basic types
- Bool - logical values
- Char - single characters; enclosed in 'single quotes' 
- String - strings of characters
- Int - 64-bit integer numbers
- Float - floating-point numbers

### Forming new types
#### List Types
> A list is a sequence of values of the same type.

`[False, True, False] :: [Bool]`
> (this is saying: the array "False, True and False" has type of "List of Bool".)

```['a', 'b', 'c', 'd', 'e'] :: [Char]```
> The array has type list of characters.

Generically, `[t]` is the type of lists with elements of type `t` - be it a list of lists, tuples, functions, characters, etc.

`[['a'], ['b','c']] :: [[char]]`
> a nested character list - a list of lists! This can be nested as many times as needed

**The type of a list says nothing about its length**, i.e. there can be a list with 5 True/False values and another with 200 and they both `:: [Bool]`.

#### Tuple Types
Tuple is a sequence of values of (optionally) different types that uses round brackets (not square brackets for lists).

`(False,True) :: (Bool,Bool)`
```(False,'a',True) :: (Bool,Char,Bool)```
```('a',(False,'b')) :: (Char,(Bool,Char))```
```(True,['a','b']) :: (Bool,[Char])```
> These are all valid

The type of a tuple **does** encode its size, unlike a list.

### Function types
A function is a mapping from values of one type to values of another type.

`not :: Bool -> Bool`
`even :: Int -> Bool`
> not has type Bool and outputs Bool.
> even has type Int and gives back True if is even and False if odd.


```haskeLL
zeroto :: Int -> [Int]
zeroto n = [0..n]
```
> The `zeroto` function has type `Int` and produces a list of integers.

### Curried functions
Functions with multiple arguments can be achieved by returning functions as results.

This is an example of addition.
```haSkEll
add' :: Int -> (Int -> Int)
add' x y = x+y
```
> Takes a single integer as input. The return type is a function, which takes the second integer as input and gives back the final result - of performing the addition.

It takes an integer `X` and returns a function `add' X`. Under the hood, this called function is waiting on the second input (the 2nd integer) - `Y` - and cannot do anything until it is passed this value. This function then takes in `Y` and then is able to return the result `X + Y`.


```HASkell
mult :: Int -> (Int -> (Int -> Int))
mult x y z = x*y*z
```


### Guarded equations
Can be used to make definitions involving multiple conditions easier to read. This solves the dangling else problem:


```haskell
signum n | n
```


### Pattern matching
Many functions have a particularly clear definition using pattern matching on their arguments

```haskell
not :: Bool -> True
not False = True
not True  = False
```

Instead of writing for && the 4 possible True/False tables and their definitons, we can use

```haskell
True && True = True
_    && _    = False
```
Patterns are evaluated in top to bottom order (in order). If we have a wildcard (\_) match in the first line, then this will be the path that is chosen.


We cannot repeat variables in Haskell, e.g. `b && b = True`


### List Patterns
Internally, lists are built up with the **cons**(truct) operator: `:`, so \[1,2,3,4] means `1(:`


### Lambda functions
The lambda funciton is a nameless function denoted with the `\` symbol

![[Pasted image 20250207142530.png]][https://youtu.be/psmu_VAuiag](https://youtu.be/psmu_VAuiag "https://youtu.be/psmu_vauiag")

### Lazy Evaluation
Functions will return e.g. 




## Recursion
Function in terms of itself

```hasKell
fac 0 = 1
fac n = n * fac(n-1)
```

Useful because a) some functions are easier to define in terms of other functions, b) many can be naturally defined in terms of themselves, and c) function properties can be defined with mathematical induction (???)

We can use recursion on lists

```

reverse :: [a] -> [a]


reverse (x:xs) 
```


Rewatch L6 and do merge/insertion sort as this is the hardest

>"quite straight forward simple function"



## Higher order 
A function is higher order if it takes a function as an argument or returns a function as a result.

> "extremely intuitive... and simple... nice easy exercise"

Given a predicate, the library function `all` will return True if everything in a list satisfies that predicate/property.


## Thinking recursively
A recursive function is a function defined in terms of itself

Recursive functions is mathematically useful for reasoning and induction.


1. Name the function simply
2. Write the function type - e.g. `:: [Int] -> Int` ***before thinking about how to define it.***
	- a good strategy is writing a simple type first and making it more complex later on
3. Enumerate the cases
	- writing down the "skeleton" from the function
4. Define the simple cases
	- can be very easy to decide what to do with e.g. an empty list. 
	- These are very often (*but not always*) **base cases**.
5. List the "ingredients"
6. Define the other cases
	- typically (*but not always*) the **recursive cases**.
	- Can be the tricky part
	- Try the simple patterns of recursion first (primitive)
7. Think about the result
	- i.e. generalising the type (from `int`s to `Num` for any numeric type )
	- 


`[Int] -> Int`
`Num a => [a] -> a`



### Data Declarations
`data Bool = False | True`

Read as "Declaring a new type called Bool which has two values, False or True". The two values False and True are called the constructors for the type Bool.


```hAsKeLL
data Answer = Yes | No | Unknown

answers :: [Answer]
answers = [Yes, No, Unknown]

flip :: Answer -> Answer
flip Yes = No
flip No = Yes
flip Unknown = Unknown
```
 
 'type' declarations are just abbreviations for a type that already exists, where 'data' declarations define a completely new type.  Only the latter can be recursive.

## Side effects
Haskell programs have no side effects; they are mathematical functions: they have all their inputs at the start and produce all the outputs at the end, it does not do anything else. 
This is a problem as reading from the keyboard/writing to the screen/networking are interactive - they are side effects.

Interactive programs in Haskell are done by using types - they distinguish pure expressions from actions (actions may involve side effects)

```hASKElL
IO a
--The type of actions that return a value of type a

IO Char
--The type of actions that return a character

IO ()
--The type of purely side effecting actions with no (void) result value
-- this is the type of tuples with no components (an empty tuple)
```

Haskell provides a number of basic actions to use/combine to write interactive programs simply.

The action `getChar` reads a character from the keyboard and return the character as its result value.

```haskeLl
getChar :: IO Char

-- this program would not be able to interact with the outside world if it did not have the IO (of char) type
```

Its complementary function, `putChar c` builds an interactive program that writes it to the screen that has a void return value:
```haskElL
putChar :: Char -> IO ()
```

The action `return v` simply returns the value `v` without performing any interaction.
```HaskELL
return :: a -> IO a
```

A sequence of actions can be combined as a single composite action using the keyword `do`

```HaSkeLL
act :: IO (Char,Char)
act = do x <- getChar
		 getChar
		 y <- getChar
		 return (x,y)
```

> A sequence of impure actions needs to be all done in the same column, as shown here. The layout tells the system what things mean.


### Primitives 
These are defined in the standard library/prelude:

Reading a string from a keyboard

```HAskeLl
getLine = do x <- getChar
			 if x == '\n' then -- this is immediately return
				 return []
			 else -- if not return then get the whole line
				do xs <- getLine
					return (x:xs)

-- We are RETURNing as everything in 'do' blocks must be actions
```

```haskell
putStr :: String -> IO ()
putStr []  = return ()
putStr (x:xs) = do putChar x
				   putChar xs
```

![[Pasted image 20250313112341.png]]



## Evaluation strategies
There are two strategies for deciding which reducible expression (redex) to consider



Innermost:

```hASkElL
infinity = 1 + infinity

fst (0, infinity)
= fst (0, 1 + infinity)
= fst (0, 1, 1 + infinity)
```


Outermost:
- May fail to give a result when innermost evaluation fails to terminate
- If any evaluation sequence terminated, then so does outermost, with the same result

Lazy evaluation is the combination of outermost evaluation and sharing of arguments. It ensures termination