

- Use lesser-compatible JDK releases - JDK 23/21




## CI/CD

- When doing a project, changes will be pushed (to keep track, latest verison)
- Each commit represents a change to the codebase
- Each commit should benefit the project: fix a bug, implement a feature or make something cleaner


However, some commits can introduce bugs, break features or reduce code quality, creating technical debt. Working code has value: for devs, the company, and users. All bugs, issues, poor quality code, fragile code all amass technical debt. It is the primary reason why things fail.

After each commit, we want to check that existing code and features remain working, and the new code does what it is expected. It is therefore important that commits are small but frequent - reducing the impact of each commit. 

CI/CD can implement and enforce checks. They are automatic, consistent (the same every time) and thorough. This brings in scrutiny: managers and other devs must know this is up to standard.

### Jobs
A job runs on a server to do one thing:
- run a set of tests
- run code quality analysis
- build/compile code
- create an executable

Pipelines are multiple jobs carried out in a specific order. They by default are triggered on every commit made to the repository. Other triggers can be configured: on every PR, scheduled “nightly” builds, webhooks, etc.

Stages are jobs in the pipeline. A pipeline can have multiple stages, and each stage having multiple jobs.

### Dependencies:
Jobs may depend on each other. 

For example, building must be done before testing it (as otherwise it will not compile), and test before release (as failing tests should not be released)


To implement this:


- a repository of source code
 - pipeline configuration (`.gitlab-ci.yml`) - a list of jobs to execute
	 - The YAML file contains a description of the pipeline and its associated jobs https://docs.gitlab.com/ci/yaml/
- runner - to run the jobs on the code
	- GitLab is not running the jobs. You have to specify somewhere else to run thm
		- A build job runs the `maven build` command, getting the jarfile
		- A test job runs the test with `maven test`
		- The release job uploads the .jar back to the repository
	- The gitlab-runner package is installed on a machine, and gitlab communicates with this to feed it jobs.
- Runners are registered to work on a specific repository as a project runner (LAB: this is how it will be done) or group runners. Instance runners are all projects in a gitlab environment

A runner can be registered via Settigns -> CI/CD -> Runners -> Create project/group runner. A token will be provided, and the runner registered with `gitlab-runner register`, with the token entered. Finally, an executor should be selected in the shell or within a Docker container - which will be destroyed on finishing. 


Each job needs to specify a runner. Runners are tagged with a name to register it. Jobs in the .gitlab-ci.ml specify tags too. **Jobs will only run on a runner with the same tag.** 

More than one tag can be put on a runner and job: ARM machines can be tagged with “arm”, “linux”, “java” versus an x86 Windows machine tagged with “windows”, “.net”, “x86” etc.

GitLab cannot access the work - they are completed in isolation. Instead, anything produced needs to be sent back to GitLab as an **artifact**: the result of a job. Another job (or users) can access the artifact of another job, if set up correctly. 

- When a pipeline is triggered, Gitlab checks for the gitlab-ci.yml
- Jobs are tagged with the name of a runner
- GitLab assigns the job to the runner
- The runner executes the job 
- Jobs may publish artifacts to GitLab for other jobs within the same pipeline. 


### Docker

When running in shell, the server can be clogged with remnants of many jobs. RUnners can be configured to exec jobs in docker containers: 
- an image can be provided in the .gitlab-ci.yml 
- each job is executed in the same environment, without contamination left over from other jobs, which are completely separated in ephemeral containers. 



## Coursework pipeline and Task 6


![](Pasted%20image%2020251124133020.png)


```yml
stages:
	- Test # the job
	  
Test: # job name
	stage: Test # job stage
	
	script:
	 - test.sh # the test shell script to run
	   
	artifacts:
		when: always # always run this
		reports: #gitlab-specific, provide nice gui to show
			junit: something
		paths:
		- target/reports # upload to here on gitlab
```


Code quality check

> Coursework: The job needs tagging with: “comp2013_2025_production”.  The checks are implemented in the “quality.sh” script.  The script generates a code quality artifact report. This should be imported into GitLab’s “codequality” report. https://docs.gitlab.com/ci/yaml/artifacts_reports/#artifactsreportscodequality


![](Pasted%20image%2020251124133547.png)

![](Pasted%20image%2020251124133532.png)

![](Pasted%20image%2020251124133600.png)










