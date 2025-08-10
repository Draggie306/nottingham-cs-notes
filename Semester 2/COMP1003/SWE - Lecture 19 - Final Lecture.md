
There are several techniques used to plan a plan a project. After the tasks are broken down, it becomes easier to estimate how many people are required, in addition to its time and cost requirements.

Activities should produce a measurable outcome so progress can be assessed - such as a requirement doc, database, code frame. These can then be added to a milestone: the end point of an activity. This allows us to more easily split/delegate activities and is ideally placed into e.g. a Jira dashboard. Task identification can be used to calculate the effort, duration, prerequisites for other tasks.


### PERT chart
![[Pasted image 20250502161622.png]]

B can only be done once A has been completed. Once A is completed, then C can also start. Once C and B are completed then D can be completed. This is the final result/product.

“Create a PERT chart and calculate the critical path” - the longest path is the critical path, which lets us cost the effort for the worst case. This is the minimum amount of time required to complete the whole project. 

> We have freedom in terms of how charts and graphs are built with tools - some can be simple, and some can be more detailed - optimistic/pessimistic scenario, most likely.

### Gantt chart
It is easy to see dependencies - task 3 only starts when task 2 is completed. Milestones can be marked as diamonds

Milestones are times to review the progress and plan. Plans are estimates, so slippage must be accounted for - a conservative plan should include time for this. When minor, the project’s later stages can accompany this. It is normal for this to occur, and therefore the start Gantt chart is probably going to look much different than the final, submitted one.

### Staff Allocation Chart
![[Pasted image 20250502163245.png]]

This is very useful to see when people are free, and when e.g. someone is ill, and their work needs to be transferred to someone else.


#### In Agile
These plans assume more traditional development practices. Planning in Agile involves sprints - project reviewing is built-in to sprint reviews and next sprint planning. 


Burndown Charts can be used to see what was/was not achieved each week, and if the team is ahead or behind.

Budgeting can be managed:
- by adding a contingency estimate (50% extra time) from the planning stage to cover risks that happen - deadlines should be pushed ahead so time
- algorithmically - with software or a general formula - A (fixed overheads) x Size (lines of code/functionality)^Multiplier (for larger projects) x M (multiplier for product/people attributes)