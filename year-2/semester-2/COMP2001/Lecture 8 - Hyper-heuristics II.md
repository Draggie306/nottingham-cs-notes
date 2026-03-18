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
Design problem domain vs Hyflex API, and another interface (representation, objective function, heuristics), with a minimum design (but can go further - e.g low level heuristics, think about the heuristic and if there is a more suitable one to implement). Design learning-based hyperheuristic approach - can fine-tune based on parameters of the practical exam (Which will run for 5 mins). DO not minimise median - this does not guarantee it works on a single trial, instead, minimise the standard deviation to guarantee to find a solution in a given range (0.15). Think about tuning approach when designing selection hyperheuristic approach.

Submitted at end of April; practical exam uses what is submitted on Moodle alongside other questions to separate students. 






