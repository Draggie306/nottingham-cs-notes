**Objectives:**
- Software risks
- Project risks

If we build software with some failures/design inadequacies, it can cause mass panic/whole populations to suffer.

Requirements and specifications include “should” and “shall” — but not ”should not”. We should actively think about **both** - as we plan requirements - to determine what we should and should not reach. For example: “Moodle should not shut down 20 minutes before coursework is due”.

New ”shall-not” requirements may include things like what should not happen, what should happen for non-correct usage or errors, beyond reliability and scalability. These requirements should be made part of our collective design decisions, designed to be risk adverse and not just the inverse of the goals.

A risk can occur in several ways: the best solution to solve a problem may be the best for a range of problems. 


In software, we can create 

Hazard avoidance - so it cannot occur
Hazard detection and removal

- health check/monitoring system to automatically restart misbehaving components. 

Security concerns (high risks) have to be approached differently - we identify routes to access this information (especially relevant for APIs), which purposefully give access.

Strategies in a project include:
- minimisation strategies - reducing a risk’s impact (e.g. everyone understands others’ work and jobs)
- avoidance strategies - actions taken to reduce chances of risk happening (e.g. replacing defective components with a backup of known reliability)
- contingency plans - what you will do/change if risk happens (investigate use )