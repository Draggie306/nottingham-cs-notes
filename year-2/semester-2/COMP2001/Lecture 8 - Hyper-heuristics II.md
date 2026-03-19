# Lecture 8 - Hyper-heuristics II



## Graph Colouring Heuristics

- Degree - number of edges connected to a vertex
- Saturation degree - number of differently-coloured nodes connected to a vertex. 

### Examination timetabling


Objective function: measures hard and soft constraints. 

Hard constraints are penalised greater than soft constraints

Neighbourhood operators are perturbation operators: choose an an exam and assign it to a different time period/room/both.


**Clique: subgraph where all vertices are connected.** For example, exams 1, 2 and 4 

**Weight: number of common students**

### Timetabling workshop
Calculate score for every vertex: 
- For each vertex, perform the graph colouring program



## Coursework 
The coursework is about designing a  problem domain using the Hyflex API, plus another interface (representation, objective function, heuristics), with a minimum design (but can go further - e.g low level heuristics, think about the heuristic and if there is a more suitable one to implement). Design a learning-based hyperheuristic approach - we can fine-tune based on parameters of the practical exam (which will run for 5 mins). Tips: when evaluating, we should not minimise the median - as this does not guarantee it works on a single trial. Instead, minimise the standard deviation to guarantee finding a solution in a given range (e.g. 0.15). Think about the tuning approach when designing the selection hyperheuristic.

Submitted at end of April; practical exam uses what is submitted on Moodle alongside other questions (which will not be specified) to separate students.

Regarding the in-lab exam last Friday, 2 people achieved 100%, including 1 person in the room (spoken when there were 10 people in the lecture).






