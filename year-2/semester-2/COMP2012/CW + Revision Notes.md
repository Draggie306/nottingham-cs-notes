
**Determinism**. At every step, there is exactly one possible move.

## Pumping Lemma

Example: *Prove that the language of words that contain the same number of `b`s and `c`s is not regular. Let this be $L_1$.*

1. Suppose that $L_1$ is indeed regular. We can choose the word: $w = b^p c^p$, where $p$ represents the pumping length. $W \in L_1$ as it requires equal numbers of bs and cs.
2. **For any valid split**, $w = xyz$, where $|xy| \le p$ and $|y| > 0$. This means that both $x$ and $y$ must appear within the first $p$ symbols of the word.
3. As an example, we can *pump up* with a pumping length of 2. This creates a new word $xy^2z$. For $k \gt 0$, this word becomes $b^{(p+k)} c^p$. As $p + k$ will always be greater than $p$, this means there will always be greater amounts of $b$s than $c$s, resulting in a contradiction: $xy^2z \notin L_1$ and is thus irregular.

## ex6

GOOD SLIDE: slide 133 on https://web.stanford.edu/class/archive/cs/cs143/cs143.1128/lectures/02/Slides02.pdf


**Grammar**: a way to generate valid strings.

These strings can be strings of regular expressions: `a`, `a + b`, `a + b ⬝ c*`; it is the grammar's job to determine which symbols in the string are valid regular expressions. 

**Terminals**: symbols visible in the output string. `a + b` is entirely terminal symbols.

**Non-terminals**. Symbols that do not appear in the output string. They are placeholders/categories of grammar. `Expression + Term` - these are placeholders that eventually become real terminal symbols such as `a + b` or `(a ⬝ b)*`

**Top-down parsing.** Starting at the start symbol, repeatedly expand non-terminals sequentially.

**Productions**. Rules for expanding non-terminals. Productions are rules for replacing non-terminals. `F -> ( E )` means F can be an opening parenthesis (lpar), followed by an expression (E), followed by a closing parenthesis (rpar). **Unambiguous grammars** are those where each expression has one **parse tree** (how the string can be generated).

> `E` here means the expression. Any expression.

**Specificity**. In a CFG, the right hand side of a production can either have non-terminals or terminals. We use `inl` and `inr` to specify which is which: `inl E` means "the non-terminal `E`", whereas `inr a` means "the terminal `a`". Thus:
- `(E, [inr a])` means `E -> a`
- `(E, [inl E, inr plus, inl E])` means `E -> E + E` 

If all precedence levels are mapped to the same non-terminal, ambiguity occurs, as there are multiple parse trees/ways to generate the same string. To solve this, use different non-terminals for each precedence level. 

By mapping precedence levels as:
- union
	- concatenation
		- star
			- parenthesis


the grammar sees: `a + b ⬝ c` as: `left side + right side`, or: `a + <something else>`. The right side `<something else>` is only parsed at the next level when concatenation is allowed. This means the only possible parse tree is `a + (b ⬝ c)`.

**Parenthesis.** At the lowest level, a parenthesised thing should be allowed to contain a full, independent regular expression.


Remember **ETF**:
- `E -> E + T | T`  - expression handles the union
- `T -> T · F | F`  - term handles concat
- `F -> A * | A` - factor handles Kleene star
- `A -> a | b | c | ε | ∅ | (E)` - atom handles symbols or parentheses

### LL(1) condition

Previously, the productions `E -> E + T`, or `T -> T · F` define the non-terminal being as being the **leftmost symbol on the right-hand side**. This is "**left recursion**". It prevents top-down parsers from terminating: evaluating `E -> E + T`, it immediately reads the leftmost symbol on the right, `E`, and evaluates this, which is (again) `E -> E + T`, causing an endless loop.

To resolve this, we rewrite the production to remove left recursion:

`E -> E + T | T`  becomes:
- `E -> T E'`
- `E' -> + T E' | ε`

For example, defining in Lean:

`(union, [inl union, inr plus, inl concat])`

becomes;

`(union, [inl concat, inl union']),`
`(union', [inr plus, inl concat, inl union']),`
`(union', [])`

## Turing machines

**Decidable**. If there exists a Turing machine that accepts every word in the language, rejects words not in the language, and always halts.

**Semi-decidable (recursively enumerable).** The TM accepts words in the language, but may get stuck (infinitely loop) for words that are not in the language. Halting is not guaranteed.

Therefore, all decidable languages are recursively enumerable, but not the other way around. 

At Level 2 (context-free), pushdown automata add to finite automaton (level 3) by including a stack. A Turing Machine (level 0) adds to this by having a tape 


## Chomsky hierarchy

- Type 3: regular languages; finite state automaton.
	- $L = \{ a^n \space | \space n > 0 \}$
	- Formalism: $G = (N, \sum, P, S)$ - (non-terminals, terminals, production rules, and start symbol
		- Rules: $A \rightarrow a$, $A \rightarrow \epsilon$, $A \rightarrow aB$ for right-regular, or $A \rightarrow Ba$ for left-regular.
	- Examples: empty language; ”any number of $a$’s followed by any number of $b$’s”
- Type 2: context-free languages; non-deterministic pushdown automaton. 
	- Language: $L = \{a^n b^n \space | \space n > 0\}$, also $L = \{a^n ++ b^n | n \ge 1\}$
	- Formalism: $G = (V, \Sigma, R, S)$ - (non-terminals, terminals, production rules, and start symbol(s))
		- Rule: $A \rightarrow \alpha$ 
	- Example: all palindromes, balanced parentheses
- Type 1: context-sensitive languages; linearly-bounded non-deterministic Turing Machines.
	- Language: $L = \{ a^nb^nc^n \space | \space n > 0\}$
	- Formalism: $\alpha \rightarrow \beta$ satisfying $|\alpha| \le |\beta|$ - the rhs is never shorter than the lhs
		- Rule: $aA\beta$ -> $a\gamma\beta$ 
	- Example: $anbncn$ 
		- $anbncn$ is NOT context-free as the stack it contains can only push and pop states. This works for $anbn$ but not for three or more symbols. It requires a tape  
- Type 0: recursively enumerable languages; Turing machines.
	- Language: $L = \{w | w$ describing a terminating turing machine $\}$
	- Formalism: $\alpha \rightarrow \beta$  where both are arbitrary strings of terminals or non-terminals.
	- (Undecidable) Example: the halting problem.

