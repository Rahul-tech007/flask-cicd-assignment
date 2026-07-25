# Flask Application CI/CD using Jenkins and GitHub Actions

## Project Overview

This project demonstrates a complete Continuous Integration and Continuous Deployment (CI/CD) pipeline for a Flask application using **Jenkins** and **GitHub Actions**.

The project automates:

- Installing application dependencies
- Running automated unit tests using PyTest
- Building the application
- Deploying to a staging environment
- Deploying to a production environment using Git tags
- Securing deployment credentials using GitHub Secrets

---

# Project Objectives

This project was developed to demonstrate:

- Jenkins Pipeline
- GitHub Actions Workflow
- Continuous Integration (CI)
- Continuous Deployment (CD)
- Automated Testing
- GitHub Webhooks
- GitHub Secrets
- Branch Based Deployment
- Tag Based Production Deployment

---

# Technologies Used

| Technology | Version |
|------------|----------|
| Python | 3.12 |
| Flask | Latest |
| PyTest | Latest |
| Jenkins | Latest LTS |
| GitHub Actions | Latest |
| Git | Latest |
| Ubuntu GitHub Runner | ubuntu-latest |

---

# Repository Structure

```
flask-cicd-assignment
│
├── .github
│   └── workflows
│       └── ci-cd.yml
│
├── Jenkinsfile
├── app.py
├── test_app.py
├── requirements.txt
├── README.md
└── screenshots/
```

---

# Prerequisites

Before running the project ensure the following are installed.

- Python 3.12
- pip
- Git
- Jenkins
- GitHub Account
- GitHub Repository
- PyTest

---

# Jenkins CI/CD Pipeline

The Jenkins pipeline automates the application build, testing and deployment.

## Stage 1 – Checkout

Source code is pulled from the GitHub repository.

```
GitHub Repository
        │
        ▼
Jenkins Checkout
```

---

## Stage 2 – Build

Jenkins installs all required Python packages.

Command executed:

```bash
pip install -r requirements.txt
```

---

## Stage 3 – Test

The application is tested using PyTest.

Command:

```bash
pytest
```

Expected Output

```
Tests Passed
```

---

## Stage 4 – Deploy

If all tests pass, Jenkins deploys the Flask application.

Deployment Output

```
Deploying Flask Application...
Deployment Successful
```

---

# Jenkins Pipeline Flow

```
GitHub Push
      │
      ▼
Webhook Trigger
      │
      ▼
Checkout Code
      │
      ▼
Install Dependencies
      │
      ▼
Run Tests
      │
      ▼
Build
      │
      ▼
Deploy
```

---

# GitHub Webhook

Whenever code is pushed to the **main** branch:

GitHub

↓

Webhook

↓

Jenkins Job

↓

Pipeline Execution

---

# GitHub Actions Workflow

The GitHub Actions workflow automates CI/CD directly from GitHub.

Workflow file

```
.github/workflows/ci-cd.yml
```

---

## Trigger

```yaml
on:
  push:
    branches:
      - main
      - staging
    tags:
      - 'v*'
```

---

# Workflow Stages

## Job 1 – Test & Build

The workflow performs:

- Checkout repository
- Setup Python
- Install Dependencies
- Run Tests
- Build Application

---

## Job 2 – Deploy to Staging

Trigger

```
Push to staging branch
```

Action

```
Deploy to Staging
```

---

## Job 3 – Deploy to Production

Trigger

```
Git Tag (v1.3)
```

Action

```
Deploy to Production
```

---

# GitHub Secrets

Sensitive deployment information is stored securely using GitHub Repository Secrets.

| Secret | Purpose |
|---------|----------|
| STAGING_HOST | Staging Server Address |
| STAGING_USER | Staging Username |
| STAGING_KEY | SSH Private Key |
| PROD_HOST | Production Server Address |
| PROD_USER | Production Username |
| PROD_KEY | SSH Private Key |

No credentials are stored inside the repository.

---

# Branch Strategy

Main Branch

```
Production Ready Code
```

Staging Branch

```
Testing and Staging Deployment
```

Production

```
Git Tags
Example:
v1.3
```

---

# Automated Testing

Testing framework used

```
PyTest
```

Run manually

```bash
pytest
```

Expected Result

```
All Tests Passed
```

---

# Deployment Strategy

## Staging Deployment

Triggered automatically when code is pushed to:

```
staging
```

---

## Production Deployment

Triggered automatically when a Git tag is pushed.

Example

```bash
git tag v1.3
git push origin v1.3
```

---

# GitHub Actions Flow

```
Push to Main
      │
      ▼
Install Dependencies
      │
      ▼
Run Tests
      │
      ▼
Build
```

For Staging

```
Push to Staging
      │
      ▼
Deploy to Staging
```

For Production

```
Create Git Tag
      │
      ▼
Deploy to Production
```

---

# Jenkins Screenshots

Add the following screenshots inside:

```
screenshots/
```

Example

```
screenshots/
│
├── jenkins-dashboard.png
├── pipeline-success.png
├── console-output.png
├── build-stage.png
├── deploy-stage.png
```

Example in README

```markdown
## Jenkins Dashboard

![Jenkins Dashboard](screenshots/jenkins-dashboard.png)

## Successful Pipeline

![Pipeline](screenshots/pipeline-success.png)
```

---

# GitHub Actions Screenshots

```
screenshots/github-actions-success.png
screenshots/staging-deployment.png
screenshots/production-deployment.png
screenshots/github-secrets.png
```

Example

```markdown
## GitHub Actions Workflow

![Workflow](screenshots/github-actions-success.png)

## Staging Deployment

![Staging](screenshots/staging-deployment.png)

## Production Deployment

![Production](screenshots/production-deployment.png)
```

---

# Jenkinsfile

The Jenkins pipeline performs

- Checkout
- Install Dependencies
- Run Tests
- Build
- Deploy

---

# GitHub Workflow

The GitHub workflow performs

- Checkout
- Setup Python
- Install Dependencies
- Run Tests
- Build
- Deploy to Staging
- Deploy to Production

---

# Future Improvements

- Docker Container Deployment
- Kubernetes Deployment
- SonarQube Integration
- Trivy Image Scanning
- Slack Notifications
- Email Notifications
- AWS EC2 Deployment

---

# Author

Rahul Bansal

GitHub

https://github.com/Rahul-tech007

Repository

# GitHub Secrets

## Overview

GitHub Secrets provide a secure mechanism to store sensitive information such as server credentials, SSH private keys, API tokens, and deployment credentials. Secrets are encrypted by GitHub and are only accessible during workflow execution.

This project uses GitHub Secrets to simulate secure deployment to staging and production environments without exposing sensitive information in the source code.

> **Note:** No credentials are hardcoded in this repository. All deployment-related information is stored securely using GitHub Repository Secrets.

---

# Configured Secrets

The following repository secrets have been configured under:

```
Repository
→ Settings
→ Secrets and variables
→ Actions
```

| Secret Name | Description | Used For |
|-------------|-------------|----------|
| STAGING_HOST | Hostname or IP address of the staging server | Staging deployment |
| STAGING_USER | SSH username for the staging server | Staging deployment |
| STAGING_KEY | SSH private key used to authenticate with the staging server | Secure staging deployment |
| PROD_HOST | Hostname or IP address of the production server | Production deployment |
| PROD_USER | SSH username for the production server | Production deployment |
| PROD_KEY | SSH private key used to authenticate with the production server | Secure production deployment |

---

# Why GitHub Secrets are Required

Using GitHub Secrets provides several advantages:

- Prevents sensitive credentials from being exposed in the source code.
- Ensures secure authentication during automated deployments.
- Protects SSH keys and server credentials.
- Enables safe collaboration without sharing confidential information.
- Follows DevSecOps best practices for CI/CD pipelines.

---

# Workflow Integration

The GitHub Actions workflow accesses these secrets during deployment.

Example:

```yaml
env:
  STAGING_HOST: ${{ secrets.STAGING_HOST }}
  STAGING_USER: ${{ secrets.STAGING_USER }}
```

Similarly, production deployment accesses:

```yaml
env:
  PROD_HOST: ${{ secrets.PROD_HOST }}
  PROD_USER: ${{ secrets.PROD_USER }}
```

---

# Deployment Process

## Staging Deployment

When code is pushed to the **staging** branch:

1. GitHub Actions starts the workflow.
2. The application is built and tested.
3. GitHub retrieves the staging secrets securely.
4. The deployment job uses the stored credentials to connect to the staging environment.
5. The application is deployed successfully.

---

## Production Deployment

When a Git tag (for example **v1.3**) is pushed:

1. GitHub Actions starts the production workflow.
2. The application is tested again.
3. Production secrets are retrieved securely.
4. The deployment job authenticates using the production SSH key.
5. The application is deployed to the production environment.

---

# Security Best Practices

This project follows these security practices:

- No passwords or private keys are stored in the repository.
- Sensitive information is encrypted using GitHub Secrets.
- Secrets are available only during workflow execution.
- Repository contributors cannot view secret values after they are created.
- Secret values remain hidden in workflow logs unless explicitly exposed.

---

# Repository Secrets Screenshot

The following screenshot shows the configured repository secrets.

```
screenshots/github-secrets.png
```

```markdown
![GitHub Repository Secrets](screenshots/github-secrets.png)
```

---

# Summary

GitHub Secrets enable secure and automated deployments by protecting sensitive credentials while allowing GitHub Actions workflows to authenticate with staging and production environments. This approach follows industry-standard CI/CD security practices and eliminates the need to store confidential information within the project source code.

# GitHub Actions Workflow

## Overview

GitHub Actions is used to automate the Continuous Integration and Continuous Deployment (CI/CD) process for the Flask application. The workflow is defined in the following file:

```
.github/workflows/ci-cd.yml
```

Whenever changes are pushed to the repository, GitHub automatically executes the workflow and performs the required build, testing, and deployment tasks.

---

# Workflow Objectives

The workflow automates the following activities:

- Source code checkout
- Python environment setup
- Installation of project dependencies
- Execution of unit tests using PyTest
- Application build verification
- Automatic deployment to the staging environment
- Automatic deployment to the production environment using Git tags

---

# Workflow Triggers

The workflow is configured to execute under different conditions.

## Main Branch

When code is pushed to the **main** branch, the workflow performs Continuous Integration by:

- Checking out the source code
- Installing dependencies
- Running automated tests
- Building the application

```
Push → main branch
```

---

## Staging Branch

When code is pushed to the **staging** branch, GitHub Actions performs:

- Build
- Test
- Deploy to Staging

```
Push → staging branch
```

This simulates deploying the latest tested version of the application into a staging environment before production.

---

## Production Deployment

Production deployment is triggered whenever a Git tag matching the pattern `v*` is pushed.

Example:

```bash
git tag v1.3
git push origin v1.3
```

This automatically starts the production deployment workflow.

---

# Workflow Architecture

```
                Developer
                    │
                    ▼
             Push Code to GitHub
                    │
                    ▼
           GitHub Actions Trigger
                    │
      ┌─────────────┴─────────────┐
      │                           │
      ▼                           ▼
 Main Branch                 Staging Branch
      │                           │
      ▼                           ▼
 Install Dependencies      Install Dependencies
      │                           │
      ▼                           ▼
   Run Tests                 Run Tests
      │                           │
      ▼                           ▼
 Build Application         Build Application
                                  │
                                  ▼
                         Deploy to Staging

                    Git Tag (v1.3)
                           │
                           ▼
                  Deploy to Production
```

---

# Workflow Jobs

The workflow consists of three primary jobs.

## Job 1 – Build and Test

Purpose:

Perform Continuous Integration by validating the source code.

### Steps

- Checkout repository
- Setup Python
- Install dependencies
- Execute PyTest
- Verify successful build

Example commands:

```bash
pip install -r requirements.txt
pytest
```

Expected Result

```
All unit tests passed.
Build completed successfully.
```

---

## Job 2 – Deploy to Staging

Purpose:

Automatically deploy the application after successful testing when changes are pushed to the **staging** branch.

Deployment Conditions

- Build successful
- Tests successful
- Branch = staging

The workflow retrieves the following GitHub Secrets:

- STAGING_HOST
- STAGING_USER
- STAGING_KEY

These credentials are used to authenticate securely with the staging environment.

Expected Result

```
Deployment to Staging Successful
```

---

## Job 3 – Deploy to Production

Purpose:

Deploy the tested application into the production environment.

Deployment Conditions

- Git tag created
- All previous jobs successful

Example

```bash
git tag v1.3
git push origin v1.3
```

The workflow securely retrieves:

- PROD_HOST
- PROD_USER
- PROD_KEY

These credentials are used for secure production deployment.

Expected Result

```
Production Deployment Successful
```

---

# Workflow Sequence

The complete workflow follows this sequence:

```
Developer Pushes Code
          │
          ▼
GitHub Detects Change
          │
          ▼
Checkout Repository
          │
          ▼
Setup Python Environment
          │
          ▼
Install Dependencies
          │
          ▼
Run Unit Tests
          │
          ▼
Build Application
          │
          ├───────────────┐
          ▼               ▼
Main Branch         Staging Branch
    │                    │
    ▼                    ▼
CI Complete      Deploy to Staging

           Git Tag Created
                  │
                  ▼
        Deploy to Production
```

---

# Error Handling

The workflow includes built-in validation to ensure that deployment occurs only when the application has passed all tests.

If any stage fails:

- Dependency installation fails
- Unit tests fail
- Build fails

then:

- The workflow stops immediately.
- Deployment jobs are skipped.
- GitHub Actions reports the failure in the workflow logs.

This prevents untested or unstable code from being deployed.

---

# Benefits of the Workflow

The implemented GitHub Actions workflow provides the following benefits:

- Automated Continuous Integration
- Automated Continuous Deployment
- Early detection of code issues
- Consistent build process
- Secure deployment using GitHub Secrets
- Branch-based deployment strategy
- Tag-based production release
- Reduced manual effort
- Improved software quality

---

# Workflow Screenshots

The following screenshots demonstrate successful execution of the workflow.

## GitHub Actions Workflow

```markdown
![GitHub Actions](screenshots/github-actions-success.png)
```

---

## Staging Deployment

```markdown
![Staging Deployment](screenshots/staging-deployment.png)
```

---

## Production Deployment

```markdown
![Production Deployment](screenshots/production-deployment.png)
```

---

# Summary

The GitHub Actions workflow automates the complete CI/CD lifecycle of the Flask application. Every code change is automatically validated through dependency installation, automated testing, and build verification. Successful builds are deployed to the staging environment when changes are pushed to the **staging** branch, while production deployments are controlled through version tags, ensuring that only validated releases reach the production environment.

# Jenkins Pipeline

## Overview

Jenkins is used as the Continuous Integration and Continuous Deployment (CI/CD) server for this project. It automatically builds, tests, and deploys the Flask application whenever changes are pushed to the GitHub repository.

The pipeline is defined in the `Jenkinsfile` located in the root directory of the project.

```
Jenkinsfile
```

The pipeline follows the **Pipeline as Code** approach, where the complete build process is maintained in source control and executed automatically by Jenkins.

---

# Pipeline Objectives

The Jenkins pipeline automates the following tasks:

- Retrieve the latest source code from GitHub
- Install all required Python dependencies
- Execute automated unit tests using PyTest
- Deploy the Flask application after successful testing
- Display the build status in Jenkins
- Send email notifications after pipeline completion (if SMTP is configured)

---

# Jenkins Pipeline Architecture

```
               GitHub Repository
                       │
                       ▼
               GitHub Webhook
                       │
                       ▼
                  Jenkins Job
                       │
                       ▼
                Checkout Source
                       │
                       ▼
             Install Dependencies
                       │
                       ▼
                 Execute Tests
                       │
              Tests Successful?
                │             │
               No            Yes
                │             │
          Build Failed        ▼
                       Deploy Application
                              │
                              ▼
                      Pipeline Completed
```

---

# Pipeline Stages

The Jenkins pipeline consists of four main stages.

---

## Stage 1 – Checkout

### Purpose

The Checkout stage downloads the latest version of the source code from the GitHub repository into the Jenkins workspace.

This ensures that every build uses the most recent code available in the repository.

Example command executed internally:

```bash
git clone https://github.com/<username>/flask-cicd-assignment.git
```

Expected Outcome

- Latest source code is available in the Jenkins workspace.
- Build process begins with the current application version.

---

## Stage 2 – Build

### Purpose

The Build stage prepares the application by installing all required Python packages listed in the `requirements.txt` file.

Example command:

```bash
pip install -r requirements.txt
```

Packages installed include:

- Flask
- Werkzeug
- Click
- Jinja2
- PyTest
- Other project dependencies

Expected Outcome

- All dependencies are installed successfully.
- Application environment is ready for testing.

---

## Stage 3 – Test

### Purpose

The Test stage verifies that the application is functioning correctly by running automated unit tests using **PyTest**.

Command executed:

```bash
pytest
```

Expected Output

```
==========================
1 passed
==========================
```

If any test fails:

- Pipeline execution stops immediately.
- Deployment stage is skipped.
- Jenkins marks the build as **Failed**.

This ensures that only tested code is deployed.

---

## Stage 4 – Deploy

### Purpose

The Deploy stage executes only if the Build and Test stages complete successfully.

The deployment process starts the Flask application and confirms that it is ready to serve requests.

Example deployment message:

```
Deployment Successful
```

Expected Outcome

- Application starts successfully.
- Flask application becomes accessible through the configured URL.
- Jenkins marks the build as **Success**.

---

# Jenkinsfile Explanation

The `Jenkinsfile` is divided into several sections.

## Agent

```groovy
agent any
```

This instructs Jenkins to execute the pipeline on any available Jenkins agent.

---

## Stages

The `stages` block defines the sequence of tasks executed during the pipeline.

```groovy
stages {
    stage('Build') { ... }
    stage('Test') { ... }
    stage('Deploy') { ... }
}
```

Each stage performs a specific part of the CI/CD process.

---

## Build Stage

Responsible for installing project dependencies.

Typical command:

```groovy
bat 'pip install -r requirements.txt'
```

---

## Test Stage

Executes automated tests.

```groovy
bat 'pytest'
```

If tests fail, Jenkins stops the pipeline.

---

## Deploy Stage

Runs only after successful completion of all previous stages.

Typical deployment command:

```groovy
echo "Deployment Successful"
```

---

## Post Section

The `post` block executes after the pipeline finishes.

It can be used to:

- Display build status
- Send email notifications
- Archive build artifacts
- Perform cleanup tasks

Example:

```groovy
post {
    success {
        echo 'Pipeline completed successfully'
    }

    failure {
        echo 'Pipeline failed'
    }
}
```

---

# Pipeline Execution Flow

```
Developer Pushes Code
          │
          ▼
GitHub Repository
          │
          ▼
GitHub Webhook
          │
          ▼
Jenkins Triggered
          │
          ▼
Checkout Repository
          │
          ▼
Install Dependencies
          │
          ▼
Run PyTest
          │
      Tests Passed?
      │         │
     No        Yes
      │         ▼
 Build Failed  Deploy Application
                │
                ▼
        Pipeline Completed
```

---

# Error Handling

The Jenkins pipeline automatically validates every stage.

If any stage fails:

- Source code checkout fails
- Dependency installation fails
- Unit tests fail

then:

- Remaining stages are skipped.
- Jenkins marks the build as **Failed**.
- The failure is displayed in the Jenkins Dashboard.
- Email notification is sent if SMTP is configured.

This prevents defective code from being deployed.

---

# Jenkins Dashboard

The Jenkins Dashboard provides an overview of:

- Pipeline jobs
- Build history
- Build status
- Console output
- Pipeline stages
- Execution duration

Example screenshot:

```markdown
## Jenkins Dashboard

![Jenkins Dashboard](screenshots/jenkins-dashboard.png)
```

---

# Jenkins Console Output

The Console Output displays detailed logs for every stage executed during the pipeline, including:

- Git checkout
- Dependency installation
- PyTest execution
- Deployment status
- Final pipeline result

Example screenshot:

```markdown
## Console Output

![Console Output](screenshots/console-output.png)
```

---

# Jenkins Pipeline Screenshots

Include the following screenshots in the `screenshots` folder:

| Screenshot | Description |
|------------|-------------|
| `jenkins-dashboard.png` | Jenkins Dashboard showing the pipeline job |
| `pipeline-success.png` | Successful execution of Build, Test, and Deploy stages |
| `console-output.png` | Complete Jenkins console output |
| `build-history.png` | Jenkins build history |
| `pytest-success.png` | Successful execution of unit tests |
| `flask-running.png` | Flask application running after deployment |

---

# Benefits of Using Jenkins

This Jenkins pipeline provides the following advantages:

- Automated Continuous Integration
- Automated Continuous Deployment
- Faster feedback on code changes
- Consistent build process
- Automated testing with PyTest
- Reduced manual intervention
- Easy monitoring through the Jenkins Dashboard
- Scalable and reusable pipeline configuration

---

# Summary

The Jenkins pipeline automates the complete build, test, and deployment lifecycle of the Flask application. Every code change is automatically processed through dependency installation, automated testing, and deployment, ensuring that only validated code is deployed. By defining the process in a `Jenkinsfile`, the project follows the **Pipeline as Code** approach, making the CI/CD workflow version-controlled, reproducible, and easy to maintain.

https://github.com/Rahul-tech007/flask-cicd-assignment
