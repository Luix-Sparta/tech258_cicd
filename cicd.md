# CICD Pipeline Documentation

## Task: Implementing Continuous Integration/Continuous Deployment (CICD) Pipeline

### What is a CICD Pipeline?

A CICD pipeline is a set of automated processes that facilitate the integration of code changes into a shared repository, along with automated testing and deployment. It ensures that code changes are efficiently and consistently built, tested, and deployed to production environments.

### Why Implement a CICD Pipeline?

Implementing a CICD pipeline offers several benefits:
- **Streamlined Development:** Developers can focus on writing code while the pipeline automates building, testing, and deployment processes.
- **Faster Feedback:** Automated testing provides rapid feedback on code changes, enabling faster identification and resolution of issues.
- **Consistency:** CICD pipelines ensure consistency in the deployment process, reducing the risk of errors and inconsistencies across environments.
- **Continuous Delivery:** Enables the continuous delivery of software, allowing for rapid and reliable release cycles.

## Continuous Integration (CI)

### What is Continuous Integration (CI)?

Continuous Integration (CI) is the practice of frequently integrating code changes into a shared repository, where automated build and test processes verify the changes. It aims to detect and address integration errors early in the development cycle.

### When to Use Continuous Integration (CI)?

CI is crucial in scenarios where:
- There are multiple developers working on the same codebase.
- Code changes are frequent and need to be integrated quickly.
- Ensuring code quality and early bug detection are priorities.

### How to Implement Continuous Integration (CI)?

#### Step 1: Source Control
- Set up a version control system (e.g., Git) to manage code changes.

#### Step 2: Automated Builds
- Configure automated build processes using build tools like Jenkins, Travis CI, or GitLab CI.

#### Step 3: Automated Testing
- Implement automated testing suites for unit tests, integration tests, and end-to-end tests.

## Continuous Deployment (CD)

### What is Continuous Deployment (CD)?

Continuous Deployment (CD) is the practice of automatically deploying code changes to production or other environments after passing through the CI process. It aims to automate the deployment process and ensure rapid delivery of software.

### When to Use Continuous Deployment (CD)?

CD is essential in scenarios where:
- Rapid and frequent deployment of code changes is required.
- Ensuring minimal manual intervention in the deployment process is a priority.
- Continuous delivery of features and updates to end-users is desired.

### How to Implement Continuous Deployment (CD)?

#### Step 4: Deployment Automation
- Define deployment scripts and automation workflows for deploying applications to various environments (development, staging, production).

#### Step 5: Monitoring and Feedback
- Integrate monitoring and alerting tools to monitor the health and performance of deployed applications.
- Collect feedback from users and system metrics to continuously improve the pipeline.

### CICD Pipeline Diagram


![CICD Pipeline Diagram](images/CICD.png)

The diagram illustrates the flow of code changes through various stages of the CICD pipeline, including source control, automated builds, testing, and deployment.

Master Server - Jenkins

## Setting up a CI/CD Job in Jenkins

### Introduction

This guide outlines the steps to create a Continuous Integration/Continuous Deployment (CI/CD) job in Jenkins and configure GitHub webhooks for automated builds.

## CICD Job

### Steps to Create the Jenkins Job

1. **Click 'New Item'**: Create a new item in Jenkins for the CI/CD job.
   ![img.png](cicd_images/img.png)

2. **Enter name**: Provide a name for the job.
   ![img_1.png](cicd_images/img_1.png)

3. **Select Freestyle project**: Choose the type of project, in this case, a Freestyle project.
   ![img_2.png](cicd_images/img_2.png)

4. **Enter description**: Optionally, provide a description for the job.
   ![img_3.png](cicd_images/img_3.png)

5. **Enable GitHub and input URL**: Enable GitHub integration for the job and input the URL of the GitHub repository.
   ![img_4.png](cicd_images/img_4.png)

6. **Enable Restrict where this project can be run and input "sparta-ubuntu-node"**: Configure the job to run on a specific node, in this case, "sparta-ubuntu-node".
   ![img_5.png](cicd_images/img_5.png)

7. **Enable Git for Source Code Management and input Repository URL**: Configure Git as the source code management system and input the URL of the Git repository.
   ![img_6.png](cicd_images/img_6.png)

8. **Input Private Key**: Provide the private key for authentication with the Git repository.
   ![img_7.png](cicd_images/img_7.png)

9. **Change to */main branch**: Specify the branch of the repository to build, typically the main branch.
   ![img_8.png](cicd_images/img_8.png)

10. **In Build Environment, Enable Provide Node & npm bin/ folder to PATH**: Configure the environment to include the Node.js and npm binary folders in the PATH.
    ![img_9.png](cicd_images/img_9.png)

11. **Click Add build step in Build**: Add a build step to the job.
    ![img_10.png](cicd_images/img_10.png)

12. **Then Click "Execute shell"**: Select the "Execute shell" build step.
    ![img_11.png](cicd_images/img_11.png)

13. **Input the Command Into the execute shell**: Enter the shell commands to be executed as part of the build process.
    ![img_12.png](cicd_images/img_12.png)

    **Commands:**
```bash
cd app
npm install
npm test
```
14. **Then click Save and Apply**: Save the job configuration changes.

    ![img_13.png](cicd_images/img_13.png)

15. **Run Build and check console output**: Run the build job and review the console output for any errors or issues.
    ![img_23.png](cicd_images/img_23.png)

### Adding A Web Hook

1. **First, Go to "Build Triggers" in Jenkins and enable "GitHub hook trigger for GITScm polling"**: Configure Jenkins to trigger builds automatically whenever changes are pushed to the GitHub repository.
    ![img_14.png](cicd_images/img_14.png)

2. **Navigate to the GitHub Repo**.

3. **Click "Settings"**: Enter the repository settings.
    ![img_15.png](cicd_images/img_15.png)

4. **Click Webhooks**: Navigate to the Webhooks section.
    ![img_16.png](cicd_images/img_16.png)

5. **Click "Add webhook"**: Add a new webhook for the repository.
    ![img_17.png](cicd_images/img_17.png)

6. **For Payload URL input `http://3.9.14.9:8080/github-webhook/`**: Specify the Jenkins webhook URL for GitHub to send payload data.
    ![img_18.png](cicd_images/img_18.png)

7. **Change Content Type to "application/json"**: Configure the webhook to send payload data in JSON format.
    ![img_19.png](cicd_images/img_19.png)

8. **Enable "Let me select individual events"**: Choose specific events to trigger the webhook.
    ![img_20.png](cicd_images/img_20.png)

9. **Enable Pull requests and Pushes**: Select the events that should trigger the webhook, such as pull requests and pushes.
    ![img_21.png](cicd_images/img_21.png)

10. **Make sure Active is enabled and click Add webhook**: Activate the webhook and save the configuration.
    ![img_22.png](cicd_images/img_22.png)

11. **Make a change and push the change to the Github Repo**.

12. **Check the build history on Jenkins for a new build**: Verify that Jenkins triggers a new build in response to the webhook event.
    ![img_24.png](cicd_images/img_24.png)
