### Bayes’ Rule
Conditional probability: 
- **P(H|E)**
The probability of a hypothesis H being true based on evidence E.

**P(E|H)**: the probability that we will observe evidence E given that hypothesis H is true.
**P(H)**: the *a priori* probability that hypothesis H is true.
**P(E)**: the probability of observing E

Bayes’ rule is used in everyday learning — using knowledge we absorb daily, we update our existing knowledge.

Naive Bayes’ Classifier:

## Knowledge Representation and Reasoning
Humans not only use methods, but also domain knowledge in person. This uses:
- Facts, concepts, procedure, models, examples about the world
- Hand-coded manually by experts
- The ultimate question was: “in knowledge-based systems, can all tasks be formalised?” — the answer is **No**.
This method dominated AI methods until the 90s. 

The chatacteristics of knowledge interpretable (can explain the reasons why the machine took those decisions).

In intelligent machines, we can deal with vague and uncertain knowledge with fuzzy logic and probability (with Bayes’ theorem). *modules with these in them can be taken in Year 3 and 4*

### Knowledge-based systems
Knowledge-based systems are built from experts around a **knowledge base**, taken from humans and stored in a way that a system can reason with it. 

The first step is to acquire knowledge - transer expertice from a knowledge source 

There is a bottleneck of acquisition in a knowledge-based system: human knowledge is very complex, unstructured and poorly formatted and formuated. Experts’ knowledge is frequently subjective, conflicting or even may be missing. 

`This is similar to a decision tree,` 

> `If e.g. some doctors do not agree on something,` 

#### Representation
In natural language: “spot is a dog. all dogs have tails”, then we can deduce that “spot has a tail:/ The problems with natural language here is that it is ambiguous

To solve this, we can use **predicate logic** which is more objective: it is a symboilic, formal language to represent knowledge. Through mathematical deduction we can derive new knowledge from old. “spot is a dog” can be represented as `dog(spot)`. The above natural language expression can be represented as:

$\text{Given that: }\forall x \ (\text{dog}(x) \rightarrow \text{hastail}(x))$
$\text{Therefore: }\text{dog}(\text{spot}) \rightarrow \text{hastail}(\text{spot})$


#### Resolution rule
This is a method to infer new knowledge. We show the counter-example leads to a conflict in the knowledge base



