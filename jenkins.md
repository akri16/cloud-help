- CI/CD Tool
- Master/Slave 
- Master node controls the slave nodes, that help offload tasks from master

- Terminology
  1. Workspace: A working directory where the code, builds and other temp files are stored during a build
  2. Build trigger
  3. Build step
  4. Artifact: Immutable file generated after the build

- Sparse checkout: Pull only the code you need

![image](https://user-images.githubusercontent.com/54491362/205369708-ee1caed5-4dd1-4d93-bad2-0226a564b91b.png)

![image](https://user-images.githubusercontent.com/54491362/205369596-cf1b662a-41b3-4ac8-9ee8-3398a0ecda38.png)

## Testing Workflow
- Forces developers to write better code
- Self docs

![image](https://user-images.githubusercontent.com/54491362/205370191-8d0803e4-a90a-49fa-b845-48054dad918a.png)

- XML Build Report

## Notifications

- You can use Slack/Teams to alert developers about build notifications

## Pipelines

1. CI/CD
2. ETL Pipelines
3. Event Driven Workflows
4. Build promotions
5. Conditional processing

- Pipeline plugin
- jenkins file
- DSL with Groovy
- Can use declarative or scripted syntax
- Stage views

Types of pipelines:
1. Scripted Pipeline: For complex requirements
2. Declarative Pipeline: For regular requirements

## Blueocean

- GUI tool for creating pipelines
- Native integration with PRs, GitHub
- Multibranch pipeline


## Declarative Pipeline
- Strings in single quote won't unmarshall the environment variables directly but it will use the value in the execution
- But if you ue a double quote it will directly unmarshall and embed the value in the output (Not good for secrets)
- 


