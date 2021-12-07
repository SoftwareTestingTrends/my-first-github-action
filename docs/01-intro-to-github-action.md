# What is Github Action?
* GitHub Actions is a continuous integration and continuous delivery (CI/CD) platform that allows you to automate your build, test, and deployment pipeline. 
* You can create workflows that build and test every pull request to your repository, or deploy merged pull requests to production.
* GitHub provides Linux, Windows, and macOS virtual machines to run your workflows, or you can host your own self-hosted runners in your own data center or cloud infrastructure.
* GitHub Actions uses YAML syntax to define the workflow.
* Each workflow is stored as a separate YAML file in your code repository, in a directory called .github/workflows.

# Github Actions Components

## Workflow:
* A workflow is a configurable automated process that will run one or more jobs.
* Workflows are defined by a YAML file checked in to your repository.
* A workflow is triggered when an event occurs in the repository, or they can be triggered manually, or at a defined schedule.
* Workflow contains one or more jobs which can run in sequential order or in parallel. For Examples:
    * A workflow that will build and test pull requests
    * A workflow to deploy your application every time a release is created.
    * Automatically add the appropriate labels whenever someone creates a new issue in your repository.
* Each job will run inside its own virtual machine runner, or inside a container, and has one or more steps that either run a script that you define or run an action.
* You can reference a workflow within another workflow

## Event: 
* An event is a specific activity in a repository that triggers a workflow run. Examples of events are:
    * A pull request opened by someone in the repository.
    * An issue created by someone in the repository.
    * Someone pushes the commit to a repository.

## Jobs:
* A job is a set of steps in a workflow that execute on the same runner.  
* Each step is either a shell script that will be executed, or an action that will be run. 
* Steps are executed in order and are dependent on each other. 
* Each step is executed on the same runner, therefore, you can share data from one step to another. 
* Example: you can have a step that builds your application followed by a step that tests the application that was built.  
* By default, jobs have no dependencies and run in parallel with each other. 
* You can configure a job's dependencies with other jobs; 
* For example, you may have multiple build jobs for different architectures that have no dependencies, and a packaging job that is dependent on those jobs. The build jobs will run in parallel, and when they have all completed successfully, the packaging job will run.

## Actions:
* An action is a custom application for the GitHub Actions platform that performs a complex but frequently repeated task. 
* Use an action to help reduce the amount of repetitive code that you write in your workflow files. 
* An action can pull your git repository from GitHub, set up the correct toolchain for your build environment, or set up the authentication to your cloud provider.
* You can write your own actions, or find actions in the GitHub Marketplace

## Runners:
* A runner is a server that runs your workflows when they're triggered.
* Each runner can run a single job at a time. 
* GitHub provides Ubuntu Linux, Microsoft Windows, and macOS runners to run your workflows.
* Each workflow run executes in a fresh, newly-provisioned virtual machine. 
* If you need a different operating system or require a specific hardware configuration, you can host your own runners.

# How to create your first workflow?
1. Create a .github/workflows directory in your main project folder.
2. In the .github/workflows directory, create a file named `github-actions.yml` (or any name of your choice)
3. Add content to `yml` file. Here's some sample content
```yml
name: GitHub Actions Demo
on: [push]
jobs:
  Explore-GitHub-Actions:
    runs-on: ubuntu-latest
    steps:
      - run: echo "🎉 The job was automatically triggered by a ${{ github.event_name }} event."
      - run: echo "🐧 This job is now running on a ${{ runner.os }} server hosted by GitHub!"
      - run: echo "🔎 The name of your branch is ${{ github.ref }} and your repository is ${{ github.repository }}."
      - name: Check out repository code
        uses: actions/checkout@v2
      - run: echo "💡 The ${{ github.repository }} repository has been cloned to the runner."
      - run: echo "🖥️ The workflow is now ready to test your code on the runner."
      - name: List files in the repository
        run: |
          ls ${{ github.workspace }}
      - run: echo "🍏 This job's status is ${{ job.status }}."
```
4. Push content to Github repository.

# Reference: 
https://docs.github.com/en/actions/learn-github-actions/understanding-github-actions