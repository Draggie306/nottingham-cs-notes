

## Infrastructure as Code
Motivation is simple: no human to press buttons. Instead, a script automatically spins up a container/VM and then is deployed, runs, etc.

It includes:
- Defining build scripts so that no human has to right click/add something: it always buids in a consistent, constant way
- Defining deployment pipeline (e.g. yaml using gitlab-ci.yml) so that decisions on build and deploy are automated.
- Defining servers such as Docker with Dockerfiles, so that cloud and test servers are defined by code that always produces the same Linux machine

### Benefits
The advantages of this are **repeatability and consistency** (same every time), **speed and scalability** (automatic), **multiplicity** (can define X version of Y platforms in Z ways), **usability** (devs can use the same local docker containers locally with the same Dockerfile) and **change management** (history of what changed and why, and who did it.)


## Deployments
Dev branch pushes to a test environment: fake databases, preliminary built text files, additional scripts, not real-world tests that try to catch edge cases and reach limits

Staging is a full replica of production, but not accessiblet ot the public. Tests running here work on real data. Alpha/beta testers can access this environment to target and catch more errors.

Production is the actual deployment environment which the public can access.

There is a difference between deploying a live service and creating a software release. If building an online environment: CD is updating that web service, that is deployed to 1 of 20 services, and see if it runs. Creating software releases may be different: not pushing code to a web server but creating ”an exe file”, which is hosted and may be downloaded. Coursework: ymal can create releases and make them available. 

A gitlab runner watches the server, and performs a job when one comes up. It downloads the code, processes it and does whatever the yaml describes.

To create one:
 1. Create an entry for a gitlab-runner  on the gitlab server, and give it a yaml tag for it to look for.
 2. Register a gitlab-runner on the pipeline machine, given the gitlab server address and access token
 3. The gitlab-runner will now monitor the gitlab server 



## YAML


```yml
build: 
	stage: build
	tags:
	- max
	script:
	- mvn test -Dgroups=prod 
```

Will only run tests JUnit tagged with prod. 
![](../../../Images/Pasted%20image%2020251117143825.png)

If the commit branch is main, just run all the tests 

![](../../../Images/Pasted%20image%2020251117143913.png)


### Docker

![](../../../Images/Pasted%20image%2020251117144447.png)

Or, we can write our own docker image with a Dockerfile.

![](../../../Images/Pasted%20image%2020251117144540.png)



- Can define a yaml to define how something is built.
- Can write a script to trigger the launch of a new container (e.g. on git push)
- Script to automatically trigger a new container (e.g. server creates new cloud container as needed)







