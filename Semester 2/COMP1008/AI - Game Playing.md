- Alpha/Beta Pruning
 - MiniMax

Why AI playing games?
- Games are intelligent activities - there are a range of activities, sometimes conflicting
- Do not require huge amounts of knowledge - more specialised, smaller
- Can measure success or failure with a set of simple rules

1997 - Chess grandmaster Kasparov loses to Deep Blue (IBM Research)

### Go
2015 - AlphaGo program beats professional human Go player. By 2017, it beat the best human player.
It was impossible for knowledge-based systems to deduce if each move was successful; a material advantage may just be a short-term gain. 

The problem was so challenging as there are over 10^120 unique states, larger than the number of atoms in the universe, taking 10^100 years to cover the whole search space.

It achieved this through Alpha-Beta search (based on [Minimax](#Minimax)) or  throguh deep learning (with 2 CNNs) based on all human games played & reinforcement learning (more advanced explanations).

### Minimax
MiniMax is a technique based on a tree search that attempts to **maximise our position of winning whilst minimising the opponent’s.** It uses a utility function to measure how ’good’ a position is. 

#### Mechanism
Assuming we can generate the full search tree.

Starting from the initial state…



### Alpha-Beta Pruning
When doing the MiniMax technique, we can cut off and remove entire branches if it can be determined that a branch will 


- Max branch: alpha cutoff
- Min branch: beta cutoff



# Course Summary

## Fundamental Issues
- Combinatorial exlosion, experiments

## Machine learning
- ANNs
- Regression (classification and regression), Decision Tree (classification)

## Intelligent Systems
- KRR, Bayes’ Rule - from statistics 
- NLP, LLMs

## Search techniques
- DFS, BFS, A* Algorithm
- Game Playing (MiniMax, Alpha-Beta)

![[Pasted image 20250327103144.png]]
- Human/computer interaction: LLMs

Exam