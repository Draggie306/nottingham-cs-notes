
## ex6

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

To resolve this


For example, defining in Lean:

`(union, [inl union, inr plus, inl concat])`

becomes;

`(union, [inl concat, inl union']),`
`(union', [inr plus, inl concat, inl union']),`
`(union', [])`

## Turing machines

