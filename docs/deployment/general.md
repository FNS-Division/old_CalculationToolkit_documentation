This section provides instructions on how to set up and manage the CI/CD pipeline for the Calculation Tools project. The setup ensures that your code is automatically built, tested, and deployed using Azure DevOps and AWS.

## General Instructions

### Overview

The CI/CD pipeline is designed to automate the process of building, testing, and deploying the Calculation Tools. This process ensures that every change to the codebase is automatically validated and deployed, reducing manual intervention and increasing reliability.

### Prerequisites

Ensure the following before setting up the pipeline:

* Access to the Azure DevOps organization where the pipeline will be configured.
* Access to an AWS account with permissions to manage AWS resources such as ECR (Elastic Container Registry).
* Docker installed and configured on the CI/CD agent or locally for testing.

### CI/CD Workflow

1. **Code Changes** : Developers push code changes to the `main` branch in the Git repository.
2. **Trigger Pipeline** : The Azure DevOps pipeline is triggered automatically by the `main` branch.
3. **Build and Test** : The pipeline builds the Docker images and runs any configured tests.
4. **Deploy** : After successful builds and tests, the Docker images are pushed to AWS ECR, and the application is deployed.
