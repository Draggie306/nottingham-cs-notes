
## ex6

GOOD SLIDE: slide 133 on https://web.stanford.edu/class/archive/cs/cs143/cs143.1128/lectures/02/Slides02.pdf


Grammar: a way to generate valid strings.

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

### LL(1) condition

Previously, the productions `E -> E + T`, or `T -> T * F` define the non-terminal being as being the **leftmost symbol on the right-hand side**. This is "**left recursion**". It prevents parsing from terminating: evaluating `E -> E + T`, it immediately reads the leftmost symbol on the right, `E`, and evaluates this, which is (again) `E -> E + T`, causing an endless loop.

%% To resolve this %%


For example, defining in Lean:

`(union, [inl union, inr plus, inl concat])`

becomes;

`(union, [inl concat, inl union']),`
`(union', [inr plus, inl concat, inl union']),`
`(union', [])`

## Turing machines

At Level 2 (context-free), pushdown automata add to finite automaton (level 3) by including a stack. A Turing Machine (level 0) adds to this by having a tape 


## Chomsky hierarchy

- Type 3: regular languages; finite state automaton.
	- $L = \{ a^n \space | \space n > 0 \}$
	- Formalism: $G = (V, \sum, R, S)$ - (non-terminals, terminals, production rules, and start symbol(s))
		- Rules: $A \rightarrow a$, $A \rightarrow aB$ for right-regular, or $A \rightarrow Ba$ for left-regular.
	- Examples: empty language; ”any number of $a$’s followed by any number of $b$’s”
- Type 2: context-free languages; non-deterministic pushdown automaton. 
	- Language: $L = \{a^n b^n \space | \space n > 0\}$, also $L = \{a^n ++ b^n | n \ge 1\}$
	- Formalism: $G = (V, \Sigma, R, S)$ - (non-terminals, terminals, production rules, and start symbol(s))
		- Rule: $A \rightarrow \alpha$ 
	- Example: all palindromes, balanced parentheses
- Type 1: context-sensitive languages; linearly-bounded non-deterministic Turing Machines.
	- Language: $L = \{ a^nb^nc^n \space | \space n > 0\}$
	- Formalism: $\alpha \rightarrow \beta$ satisfying $|\alpha| \le |\beta|$ - the rhs is never shorter than the lhs.
	- Example: $anbncn$ 
		- $anbncn$ is NOT context-free as the stack it contains can only push and pop states. This works for $anbn$ but not for three or more symbols. It requires a tape  
- Type 0: recursively enumerable langauges; Turing machines.
	- Language: $L = \{w | w$ describing a terminating turing machine $\}$
	- Formalism: $\alpha \rightarrow \beta$  where both are arbitrary strings of terminals or non-terminals.
	- (Undecidable) Example: the halting problem.

