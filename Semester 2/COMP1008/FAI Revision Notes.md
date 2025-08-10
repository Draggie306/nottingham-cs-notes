> *This is based on COMP1008 - Fundamentals of Artificial Intelligence - at the University of Nottingham, taught by Professor Rong Qu.*
## Defining AI
The first challenge in AI is defining what is really meant by it. There are a range of definitions and categories. 

- Weak, task-dependent AI includes chatbots, voice assistants and language models. These already exist but are domain-specific.
- Strong AI (known as "artificial general intelligence" - AGI) is broad, general-purpose, human-like and human-level systems that can think, adapt and learn independently. At the moment, these are purely hypothetical.

AI can be (broadly) defined as machines that exhibit a form of intelligence as a result of learning from an environment, and then using this learnt material to take intelligently-perceived actions.

### The Turing Test
This is a test where a human interrogator has a text-based conversation and is blindly given two answers: one from another human, and one from a computer. If the human interrogator cannot distinguish the machine's responses over the human's 30% of the time, then the machine "passes" the test and is deemed to imitate intelligence and considered an intelligent system.

### Chinese Room Experiment
This test asks whether a machine that behaves intelligently is actually intelligent.
A Chinese person inputs a series of Chinese symbols into a "room". Within this room, there is a person with no understanding of Chinese. However, this person has access to a rule book written in English with a series of translations from English to Chinese. They then use these to respond intelligently to another person outside the room. 
This exhibits the dilemma of how understanding is defined. Clearly, the person inside does not understand Chinese, but if the system as a whole behaves like it does, is it still intelligent? It cannot be proven that it is.

# Machine Learning
A computer program is said to learn from experience ($E$) in relation to a series of tasks ($T$) and given performance ($P$) in those tasks, if its performance $P$ in tasks $T$ improves with experience $E$.

The top-down (classic) approach is model all different functions separately and connect these "agents" together, using a programming language to communicate with each agent for a specific task

The bottom-up (machine learning) approach is to give a system lots of data so that it can discover new concepts. Models learn new behaviours and knowledge from a set of data with no hard-wired instructions.

> When translating natural language, it becomes impossible for a top-down approach to create accurate translations: language requires nuance and idiomatic expressions which is only possible with bottom-up approaches.

### Three pillars
There are three "pillars" to improve machine learning techniques:
- models 
	- rapid advancements in the last decade
- computation 
	- historically was more of a bottleneck; caused early AI winters because of lack of resources
- data
	- in 2013 there was more data created than at any point in human history.
	- has led to some major breakthroughs

### The ML Process
To make a model, the dataset should be cleaned, have its missing data handled (*imputation*), and outliers/duplicates removed.
In addition, to test the model, there should be a train/test split of around 70/30% to evaluate its performance on known data.
## Supervised learning
Learns from a labelled dataset, given a sample input points and desired output values. A model can be trained to deduce the output given an input. Examples are classifiers and predictions: linear regression, decision trees, ANNs.
### Regression
A regression model finds the relationship between X and Y variables with minimal (mean squared) error - "given an input X, predict what another data point Y will be". 

The linear regression function is $\ G(x) = b0 + b1 * x$


The benefits of regression models is that they are often very fast to train - up to orders of magnitude faster than ANNs or random forests. They are easy to interpret and implement.
However, they often underfit the data: simple linear regression - a single linear line - does not have the flexibility to account for complicated relationships. It also can be prone to overfitting if there are many outliers/noise in the data.

### Classification - decision trees
Learns how to categorise a new "instance" based on previously classified instances. 

Decision trees are an example of classification. They have various **features** (cloud cover, temperature) which are **partitioned** dependent on a value. For example, if the temperature is less than 5, then it will rain. Otherwise, if it is greater than 5, determine the cloud cover. If the cloud cover is also above 80% then it will rain. Otherwise it will not rain. This process of recursively creating new partitions based on features and values repeats until all values are classified. 
However, this process is more prone to overfitting, as each point has to have an ever-increasing amount of specificity.

These decision trees have reasonable training times and can handle many features. They are easy to interpret and implement - there is a clear decision being made for each partition.
However, they struggle with very complex systems with less predictable/more complex boundaries and relationships

## Unsupervised learning
Learns from unlabelled data points - it is not known what they are or how they match to an output. The objective varies depending on use case. Techniques include K-means clustering, grouping and associating.

This is used to find patterns/structures in unlabelled data, however there is no "truth" for accurate evaluation of performance, so requires more data. Luckily, **the majority of data available is unlabelled**. 
Examples of using unsupervised learning in tech is grouping customers into large groups based on their shopping history, then recommending individuals items based on other users in the group -this touches on big data/data mining too (*if a male between 25 and 35 buys a beer in the evening, they are also likely to buy a nappy*). In finance, this can be inverted: outlier individuals/transactions not categorised in a group can be identified for fraud (*if user $X$ makes a payment of $Y,YYY$ to $Z$ at $AB:CD$, then it is likely a scam*).

## Reinforcement learning
Learns in an environment with a problem to solve. The agent takes in feedback from the environment and, depending on its actions taken, is rewarded or punished. Over time, it learns what it should do in the environment. Examples include deep neural networks for self-driving cars and game playing.


## Artificial Neural Networks
ANNs are designed to simulate how neural networks work in the brain. The first neural networks were based on the idea that if simple inputs combined met or exceeded a threshold, the neuron would "fire" - and this changes automatically. Long-term and many neurones could thus simulate basic learning.
This is known as the **perceptron**. However, it brought a challenge: the perceptron could not account for certain types of important functions, known as non-linearly separable functions. Multi-layered networks were discovered a few decades later.

> Linearly separable functions are those that can be separated by a linear boundary, such as a straight line or plane. In neural networks, these can be represented by a single-layer network like the perceptron.

If the sum **O** of all excitatory (positive) inputs and inhibitory (negative) inputs reach the neuron's threshold **t** then the neurone fires:
$$O = x1 * value + x2 * value + x3 * value $$
For simple functions, like an OR gate, a single perceptron is adequate: any input that meets a threshold value of 1 fires the neuron.

For more complex ones like an XOR gate, it is non-linearly separable: there is not one single threshold value (if it's 1 then fire, but if below OR above then do not). Therefore, multiple layers in the "hidden layer" section of such a network are required: these can model NAND gates, and give the output to the output layer, which only fires if both hidden layers output 2, so the sum of all inputs is thus 4. *ANN weights cannot determine the importance of input features, so inputs should be scaled/normalised e.g. with a min-max scale.*
ANN models can solve both regression and classification tasks.

Deep learning models involve a huge number of hidden layers in an attempt to more accurately simulate the brain. These are "black boxes" - it is very hard to understand exactly what it is doing as there are so many hidden layers.

As ANN models are hard to interpret, we can use a confusion matrix to determine the performance and accuracy of the model by using true positives, negatives and false positives/negatives.

# Intelligent Techniques

## Bayes' Theorem
This is the foundation for conditional probability: there is an hypothesis ***$H$*** AND prior evidence $E$, written as:
$$P(H|E)$$ (said "*P of H being true, given E.*")

Likewise:
- $P(E|H)$  is the probability that the evidence $E$ will be observed given $H$ is true;
- $P(H)$ is the *a priori* probability that $H$ is true - without any previous knowledge/evidence $E$;
- $P(E)$ is the probability that $E$ will be observed.

$$ P(H|E) = \frac{P(E|H) \cdot P(H)}{P(E)}$$
meaning:
"The new probability (based on the prior event) is equal to the chance that E given H occurs, times the prior probability that H is true, divided by the overall probability that E will just randomly happen"

Given a question:
- P(H1) is the chance that something X happens (e.g. struck by lightning = 10%) 
- P(H2) is the chance that something X does NOT happen (not struck by lightning = 90%) 
- P(E|HY) is the chance that, of those that HY happens to, a given event E also happens (50% survival rate of being struck by lightning = overall 50%)

## Knowledge Representation and Reasoning
The vast majority of data is vague, uncertain and is not easily interpretable by a machine. Therefore, experts used to manually hard code information into a system. But, the question "can all tasks be formally represented?" has been answered as "no".

A knowledge base is a collection of knowledge taken from a human and stored so that it can be reasoned with by the system. This allows experts' knowledge to be integrated into the system to make the same decisions as the experts without need of them - but only for a narrow, limited use case. For example:
- Case A includes a customer buying a house for 250k led to a profit of 25k
- Case B includes a customer buying a house in the same area for 275k led to a profit of 27k
- therefore: model of the reasoning can assume that a 260k sale would give a profit of about 26k

The acquisition of this knowledge, even if it isn't subjective or conflicting, is a bottleneck - it may not encompass everything, adding more takes time to add and to maintain, etc. 


Predicate logic is used to represent data in a KBS. 

clause 1. `∀X: dog(X) -> hastail(X)`
clause 2. `dog(spot)`
goal: `hastail(spot)`.

To use the resolution role, we do the following:
1. Translate the statements into Conjunctive Normal Form
	- this is done by turning implications (`X -> Y`) into `¬X OR Y`
2. Add a negated goal to the knowledge base
	- clause 3: `¬hastail(spot)`
3. Perform unification
	- Substitute/unify spot in: `¬dog(x) ∨ hastail(x)` becomes `¬dog(spot) ∨ hastail(spot)`
	- resolving `¬dog(spot)`  with clause 2 (`dog(spot)`) results in them cancelling out
	- therefore we are left with clause 4: `hastail(spot)`
4. Resolution of `¬dog(spot) V hastail(spot)`
	- clause 3: `¬hastail(spot)` and clause 4: `hastail(spot)` = cancelling out; empty clause 
	- Therefore, the clause 2 `dog(spot)` contradicts the resolved `NOT dog(spot)`
- Proof: `hastail(spot)` must be true due to resolving the contradiction

## Natural Language Processing
Convolutional neural networks are great on images due to a hierarchical structure of hidden layers.
Recurrent neural networks are great on text due to their sequential structure.
Transformers are a specific type of ANN that capture long-range dependencies in text, revolutionary for language processing.

These are all types of deep learning models. (AI -> ML -> NN -> DL)
### Large Language Models
All modern LLMs are built with transformers. They're trained on huge amounts of high-quality data with many parameters (weights trained) and output the most likely word to follow.

- To train, licensed data from the internet was used, and then cleaned: harmful information removed, duplicates removed. This is generally done with unsupervised pretraining to identify huge patterns in text. Then, supervised fine tuning can be carried out on specific tasks. 
- Reinforcement learning uses rewards/ranking (human feedback) to optimise the output.
- Pre-processing can include normalisation and tokenisation, alongside stopwords, stemming (stem of the word e.g.. running -> run).
- When generating the final output, the temperature can be adjusted to give more weight to less likely tokens.

To improve GenAI, algorithms (reduce bias, more fairness), models (diverse real world examples) and data (get equal )


# Tree Search Techniques
The search space is the set of all solutions to a problem. In a tree, this would be all the nodes (states). An operator refers to the branches: a set of actions that move between states. Additionally:
- a neighbourhood is all the possible states reachable from a given state
- a goal test is a state that tests if the search reaches a state that solves the problem
- the path cost is the cost to take a given path
- the branching factor is the average number of branches of all nodes in a tree: in a binary tree, the factor is 2 with depth ***d***

The general search algorithm can be defined thus:

```js

function GeneralSearch(p: state, Queueing_Function) returns Solution or Failure
	nodes = Make_Queue(Make_Node(Initial_State[p]))
	do
		if is_empty(nodes) return failure;

		node = Remove_Front(nodes);
		if Goal_Test[p] on State(node) == success return node;

		nodes = Queuing_Function(nodes, Expand(node, Operators[p]))
```


All tree search techniques can be evaluated with the following criteria:
1. Completeness
	- If a solution exists, is it guaranteed to be found?
2. Time complexity
	- How long will it take to find a solution?
3. Space complexity
	- How much memory will it take to search?
4. Optimality
	- Will it find the best solution if there are multiple?
The worst-case scenario is used to compare benchmarks, as this dominates other cases.

## Combinatorial explosion
The feature that the number of solutions for a problem increases exponentially with the size of the problem. The Travelling Salesman Problem is an example of this: the number of solutions grows hideously large for even a moderate number of cities.
 
To improve problems like the TSP or 8-queen problem, we can make the search tree smaller (change the model) or improve search efficiency (change techniques).

## Breadth-first search
This expands the root node, and expands, by adding all nodes to the end of the queue, at level **d*** before expanding the nodes at ***d+1***.

Its time and space complexity is O (b^d), where b is the branching factor and d is the depth. It is complete and optimal.

- It is only applied to problems where the costs are the same for each branch/operator.
## Depth-first search
This expands the root node, then explores the first branch before another. It adds each node to the front of the queue.

Its time complexity is O(b^m)and space is O(bm) where m is the maximum depth of the tree. It is neither complete nor optimal

- Used when adapted for specific problems like games, or when tree depth is minimal.
## Uniform cost search
Uses the total cost of the path from the root node, adding each node depending on distance, recursively removing the smallest cost node next, adding this cost to the total path to that node.

Is complete and optimal, and has an O(b^d) time and space complexity

- It can be applied to all problems, providing that costs never decrease along the tree. Branches rapidly get "cut off" so is generally efficient.

## A* Algorithm
A blind search is one that randomly chooses which child node to visit without prior knowledge - like breadth-first or depth-first. This is not good for large problems or search spaces so a heuristic, "educated guess", is applied.

f(n) = g(n) + h(n); where:
- g is the path cost from the initial to current state n
- h is the heuristic cost from the current to goal state n
- f is the estimated cost of the cheapest path to solution n

If the heuristic (h(n)) is zero, then A* becomes the UCS search.
If h is too large it dominates g and becomes greedy, losing optimality.

The algorithm is only optimal and complete if the heuristic is admissible: it must never overestimate the cost to reach the goal. For example, it could be the straight line distance from one city to another - it's a lower bound.

It calculates the distance so far to all nodes adding on the heuristic estimate for each. It then goes to the node with the lowest total distance so far.

## Game Playing
Games have a finite number of states that do not require huge bases of knowledge, are intelligent activities, and have easy rules to follow for winning/losing.

### MiniMax
This is a way of an opponent trying to prevent another agent winning for every move. It is a tree search that attempts to maximise our board position whilst minimising the opponent's - using a utility function to measure how good a position is.


### Alpha-beta pruning