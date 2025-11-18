Talk by Oliver Hathaway - 17/11/2025 University of Nottingham

”The best language is the one you already know how to use”. There is no expectation more unrealistic than a developer being more careful and tactical. 

If you work solo, the project lives in your head. In the real world, the project lives in 40 people’s heads, and their laptops. Code must work on multiple devices. If your process relies on someone remembering to do one thing, the process has already failed.

It is not working until it is deployed and working. Devops is the solution to “it works on my machine” - if it is not run, it is not working fine.

Deploy often, integrate often, test as we do. In the same way we terminate a line with a ;, we terminate the period of coding with a deployment

Branching strategy mirrors the release strategy. If you do not need a complex branching strategy, do not have one.

> The easiest way to not forget things is to automate them.

Test as you deploy. Push -> pipeline runs test script -> returns fail/success. This can be very helpful if e.g. your code works fine but break someone else’s code. 

Deploy code to shared environments - that others have written. 

Post deployment - now in prod (or dev env). Just because it hasn’t doesn’t mean it won’t. Does it seem to work and passes test data, but as soon as real data is obtained it crashes. Memory leaks after 20 minutes? 

Deployment, testing pipelines, merge all happens when you finish work on a tiny piece of code. When it is checked in, it can receive a lot of test traffic before we can say “I’m happy with that code”. 


Merge
- Continuous integration - runs through integration tests on your own private branch
- Checking in regularly was not standard practice 
- Merging with other code often causes merge conflicts

Continuous integration tests
- Build tests running in the build pipeline.
- Run full test suite when merged to main
- Check whether or not it even builds

Continuous deployment
- Automated process to push code into an environment
- Tests that it does not break the system or service
- Could be code registry, can be deploying to a “test machine 12”

Interation environment
- Ensure it does what it should do when deployed along others’ code
- Does it display on the screen, work on hardware, call the correct internet service?

Canary deployment
- Ensuring it receives traffic and see what it does when it gets that traffic


Build all infra as yaml files versus manually changing a config in Azure etc. This means we can containerise the application for a webserver or Docker container.

Branching matches coding strategy. Push to main for personal projects. As soon as it involves two people. If working on same area, then work out a branching strategy. If working in completely different folders, can just push to main.

Ephemeral environments: spin up a server that is isolated from every other dev environment that is only on for when it is needed to be on. 

> You are not a developer of code. You use a way of thinking that includes testing, deploying, making sure it doesn’t break in a production environment, and seeing it go from concept to used by everyone.


Taken the time to:
- Make all code, 90% completed.
- The last 10% is what is difficult - someone who has tried and has learnt from their attempts.
	- Do not bite of more than you can chew, as this will mean you never get to experience the valuable DevOps 10%. 

- Comments explain why something is done, not what it is doing.
- Getting the team to work together is just as important as doing all the code.
- Paired programming: preached in textbooks, never used in real life.
	- 2 people at a desk working on a problem is faster than someone doing it alone. 
- Do not be the one expert who knows one thing - you will get stuck into a corner 

Saying “infrastructure as code”:
- Every platform engineer would know Terraform - this can be pointed to any environment for AWS/Azure/GCP etc. 
- This is anything that is not the code or tests that controls the infrastructure 


















