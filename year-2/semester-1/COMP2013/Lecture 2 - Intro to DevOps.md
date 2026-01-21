
## DevOps

In a company: more waste = less product and fewer profits. 

There is an infrastructure behind delivering code and projects: 

DevOps is **the practice of operations and development engineers, participating together, through the entire service lifecycle, from the design and development process all the way to production support.**

It is the intersection of development (from specification to product), quality assurance (ensuring it meets the standards) and IT operations.

It improves IT and business outcomes: high performing teams deploy 973x more frequently than low-performing teams. 

### Core values
It changes people’s behaviour to bring quality to their code, testing and infrastructure. Where it can be done, automation is used throughout. Measurements for success are widespread: metrics include cycle time to deploy new features (if 100 new features, were 50% done more quickly, and as a team, why?), costs and revenues (high quality with lower cost = higher chance of getting a job). The process allows trust to be built, the team to share and be transparent, in a collaborative environment. If something goes wrong, there is no blame culture - it’s about learning from it as a group.


There are 3 ways of developing software:
1. Systems thinking: what are the different components and how can they be implemented, from dev to ops.
	- This makes work ”visible” to the ”value stream” for the customer.
	- Work-in-progress features are limited: if working on something for 4 weeks, it hasn’t been broken down enough
	- Focus should be on the outcome of the entire system.
2. Amplifying feedback: from dev to ops and back around again.
	- This enables fast flows of feedback from right to left at all stages of the “value stream” - if the test is not capturing something, it will be changed for the developer next time.
3. A culture of continuous experiment and learning: 
	- Software engineers want to scrutinise and understand where errors happened and how to recover from this -> a postmortem, to identify code/people mistakes
	- “What was the last thing I did, what can I learn from it, to ensure an obstacle doesn’t happen again?”


Too much data = overload; good data is hard to come by, but worth to add to the data stream.



## Continuous Integration/Continuous Delivery

There are 2 phases to the coursework: 1 is clean up and rewrite the code, 2 is rewriting the pipeline's code to test these new features

### CI
CI is a development practice that requires developers to integrate code into a shared repository, multiple times daily. Each check is verified automatically, which allows teams to detect problems earlier. It does not remove bugs, but it makes them easier to remove.

It allows automatic tests for things like cross-browser and cross-platform tests, allows stress and longevity testing of new features and code paths, though it is hard to protect against security threats. 

### CD

CD is  the ability to get features, changes, fixes and experiments into production/the main git branch and into the hands of users safely & quickly in a suitable way.  There is a trend to “automate where you can”: only automation that adds to the value stream.


The DevOps pipeline involves:
- source control/source code (includes testing code). To manage code, we need code. This is known as **infrastructure as code** - must think about the whole thing, not individually.

### Blue-green deployment
This is a way of having 2 production environments, as identical as possible. The “blue” deployment is the current, live development, and the “green” deployment is the final, new deployment that has passed all tests. There is a “router” which selects which deployment to route new requests to. It allows us to rollback to old deployments with a simple router change. It also facilitates a very small downtime as there is no gap in deployment - both old and new versions are online concurrently.


### Benefits of CI/CD

- Software release is automatic and painless
- There is lower testing costs as all can be run in seconds, automatically
- Bugs are identified much more quickly and with less risk, as CI can find mistakes before it even reaches the ”test” enviromment
- Time to marker is much faster
- Cloud resources are managed more effectively and are more predictable
- Improved customer and developer satisfaction


## Weekly Lab
Submittable on Moodle. 
