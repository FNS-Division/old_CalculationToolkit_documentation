# Azure DevOps Setup

This section details the Azure DevOps pipeline setup for the Calculation Tools. The setup works for both the old and modified versions of the project.

### Starter Pipeline Configuration

Below is the Azure DevOps pipeline configuration used for the Calculation Tools project. This configuration builds Docker images, handles authentication with AWS, and pushes the Docker images to AWS ECR.

###  Pipeline.yaml code


```
# Starter pipeline
# Start with a minimal pipeline that you can customize to build and deploy your code.
# Add steps that build, run tests, deploy, and more:
# https://aka.ms/yaml

trigger:
- main

pool:
  vmImage: ubuntu-latest

steps:
- task: DockerCompose@1
  inputs:
    containerregistrytype: 'Container Registry'
    dockerComposeFile: 'docker-compose.yml'
    action: 'Build services'
- task: AzureCLI@2
  inputs:
    addSpnToEnvironment: true
    azureSubscription: 'ADO-ConnectivityToolkit-AWS' # service connection name
    scriptType: bash
    scriptLocation: inlineScript
    inlineScript: |
      # Retrieve the ID_TOKEN using 'ADO-ConnectivityToolkit-AWS' service connection to Azure App and set it as WEB_IDENTITY_TOKEN to be used in step 2
      echo "##vso[task.setvariable variable=WEB_IDENTITY_TOKEN]${idToken}"
- task: AWSShellScript@1
  displayName: 'second-step-after-Azure-Cli'
  inputs:
    regionName: 'eu-central-1'
    scriptType: inline
    inlineScript: |
      # assume the role using with web identity
      CREDS=$( aws sts assume-role-with-web-identity --role-arn "arn:aws:iam::238974323615:role/ado-ADO-ConnectivityToolkit-AWS-Role" --role-session-name "ADO-ConnectivityToolkit-AWS-PIPELINE" --web-identity-token "${WEB_IDENTITY_TOKEN}" --duration-seconds 3600 );
      export AWS_ACCESS_KEY_ID=$(echo $CREDS | jq -r '.Credentials''.AccessKeyId');
      export AWS_SECRET_ACCESS_KEY=$(echo $CREDS | jq -r '.Credentials''.SecretAccessKey');
      export AWS_SESSION_TOKEN=$(echo $CREDS | jq -r '.Credentials''.SessionToken');
      echo "##vso[task.setvariable variable=AWS_ACCESS_KEY_ID]${AWS_ACCESS_KEY_ID}";
      echo "##vso[task.setvariable variable=AWS_SECRET_ACCESS_KEY]${AWS_SECRET_ACCESS_KEY}";
      echo "##vso[task.setvariable variable=AWS_SESSION_TOKEN]${AWS_SESSION_TOKEN}";
- task: AWSShellScript@1
  displayName: 'ECR'
  inputs:
    regionName: 'eu-central-1'
    scriptType: inline
    inlineScript: |
      aws ecr list-images --repository-name connectivitytools --region eu-central-1
      aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 238974323615.dkr.ecr.eu-central-1.amazonaws.com
      docker tag calculationtools_api-backend 238974323615.dkr.ecr.eu-central-1.amazonaws.com/connectivitytools:giga-test-ado
      docker push 238974323615.dkr.ecr.eu-central-1.amazonaws.com/connectivitytools:giga-test-ado

```


### Key Components

* **Trigger** : The pipeline is triggered by changes to the `main` branch.
* **Build Services** : Docker Compose is used to build the services defined in the `docker-compose.yml` file.
* **Azure CLI** : The Azure CLI task authenticates with Azure using a service connection.
* **AWS Shell Script** : AWS commands are executed to assume roles and push Docker images to ECR.

### Setting Up the Pipeline

1. **Create a New Pipeline** : In your Azure DevOps project, go to Pipelines and create a new pipeline.
2. **Connect to Your Repository** : Choose your Git repository where the code resides.
3. **Configure the YAML** : Copy and paste the YAML configuration provided above.
4. **Save and Run** : Save the pipeline and trigger a run to ensure it works as expected.
