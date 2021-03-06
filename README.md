# CI Pipeline

Automating a full CI pipeline


## Prerequisites

- Ansible
- Vagrant *(to run locally)*
- Virtualbox *(to run locally)*


## Run

You can run locally on Vagrant or on remote hosts


### Locally on Vagrant

```bash
git clone <this-project>
cd <this-project>

vagrant up
```

### On Remote

- no steps yet


## Goals

- Faster continuous delivery
- More jobs run in parallel
- Faster disaster recovery
- Test environment consistency
- Every build is shippable for all deployable configurations
- Increse number of builds per day
- Jobs on all supported test environment combinations
- Track everything and report details on each run
- Create test environments with one command
- Self-service cloud-based engine
- Deploy lastest as close to production as possible for final verification
- build environments defined as Docker containers, owned and maintained as Dockerfiles by the dev teams that use them.
- the ability to pre-generate build pipelines for known technology stacks so teams can maintain continuous delivery build pipelines running the first day they create a code repository.

## How to do it?

- Everything is code:
  - server configuration
  - pipeline jobs
  - test environments
- Jenkins (Open Source Version)
- The Job DSL plugin for Jenkins
- The Build Flow plugin for Jenkins
- Engineering ingenuity to glue our various components together

## Caveats

- No Windows test environments

## Jenkins
- Jenkins master server (Java process)
- Jenkins master data (Plugins, Job Definitions, etc)
- NGINX web proxy (for SSL certs)
- Build slave agents (machines either being SSH’d into, or JNLP)
- run docker:
```bash
# create data volume
docker run --name=jenkins-data myjenkinsdata

# using the data-volume
docker run -p 8080:8080 -p 50000:50000 --name=jenkins-master --volumes-from=jenkins-data -d myjenkins

# read persistent logs
docker exec jenkins-master cat /var/log/jenkins/jenkins.log

# cp logs from volume
docker cp jenkins-data:/var/log/jenkins/jenkins.log jenkins.log
```
