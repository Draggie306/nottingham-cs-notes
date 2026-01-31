
## The Maximum Satisfiability Problem 

Is an NP-hard problem. It is defined as Boolean variables, with a number of disjunctive clauses connected by conjunction. For example:

$$ (\lnot X \lor \lnot Y) \land (Y \lor \lnot Z) $$
$$ (A \lor \lnot B) \land (B \lor C) \land (\lnot A \lor \lnot C) $$

This is *conjunctive normal form*.

For the MSP, we need to find an assignment of truths for each variable that maximises the total number of satisfiable, non-contradictory clauses. 

The objective function is

$\text max z = f(x)$ 

where:
- $x$ is the vector of Boolean variables
- $f(x)$ is counts the number of satisfied clauses according to the variable assignments in $x$. 

The minimisation objective function for the MAX-SAT problem has a goal of minimising the total number of **unsatisfied** clauses.

It is possible for multiple solutions to have the **same objective function** value, even if the problem instance is different.



