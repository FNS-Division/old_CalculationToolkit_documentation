This section provides details on deploying the Calculation Tools to AWS using the pipeline configured in Azure DevOps.

This setup assumes you have AWS Setup, AzureDevops Setup,  and a repository ( Github repository or azure repository)

The pipeline runs successfully  from the main branch [(View run tests here).](https://dev.azure.com/ITUINT/ConnectivityToolkit/_git/calculation-tools?path=/azure-pipelines.yml&version=GBmain&_a=history) This guide is to setup  from a modified branch

**Quick references and additional Video learning guides :**

[Old calculation toolkit deployment via AWS CLI  Documentation ( Setup by original developer on how to deploy on aws- Reccomended )](https://ituint.sharepoint.com/:w:/r/sites/ConnectivityModelling-Internship/_layouts/15/Doc.aspx?sourcedoc=%7B05EDF5A0-768B-475E-9DCC-A40C6623B153%7D&file=Calculationtools%20AWS%20Deployment%20Guide.docx&action=default&mobileredirect=true)

[Connect Azure DevOps Pipeline to AWS Cloud  ( VIDEO DEMO GUIDE - Reccomended)](https://www.youtube.com/watch?v=Vywmy5FFzoM)

[Setting up a continous  development pipeline between github and AWS (VIDEO DEMO GUIDE )](https://youtu.be/biYVW1TMYAU?t=373)

[VS CODE Extension to assist with pipeline deployment to AWS (Reccomended  )](https://marketplace.visualstudio.com/items?itemName=AmazonWebServices.aws-vsts-tools) - Requires Admin rights

## Prerequisites.

Before starting, ensure you have the following:

1. **Azure DevOps Account**: For setting up pipelines and service connections.
2. **AWS Account**: With permissions to access ECR and IAM roles for authentication.
3. **Docker**: Installed locally or in the build environment.
4. **AWS CLI**: Installed and configured for AWS access.

## Step 1: Create AWS IAM Role for Azure DevOps

1. **Create an IAM User** in AWS:

   - Go to the **AWS Management Console** and navigate to **IAM**.
   - Click **Users** and create a new user (e.g., `azure-devops-user`).
   - Select **Programmatic Access**.
   - Attach the following permissions:
     - **AmazonS3FullAccess** (or any other necessary permissions for your project).
   - Save the **Access Key** and **Secret Access Key**. You’ll need these later.
2. **Create a Role for Web Identity Federation**:

   - Navigate to **IAM Roles** in AWS and create a new role for Web Identity.
   - Attach the necessary permissions (e.g., **AmazonS3FullAccess**).
   - Save the **Role ARN** for later.

## Step 2: Set Up Azure DevOps Pipeline

1. **Create a Service Connection in Azure DevOps**:

   - Navigate to your project in **Azure DevOps**.
   - Go to **Project Settings** > **Service Connections**.
   - Click **New Service Connection** and choose **AWS**.
   - Provide the **AWS Access Key** and **Secret Access Key** saved earlier.
   - Name the service connection (e.g., `ADO-ConnectivityToolkit-AWS`).
2. ### **Create the `azure-pipelines.yml` File**: ( [You can also find it in this link ](https://dev.azure.com/ITUINT/ConnectivityToolkit/_apps/hub/ms.vss-build-web.ci-designer-hub?pipelineId=79&branch=modified))

   In the root directory of your repository, create the file `azure-pipelines.yml`.


   ```yaml
   trigger:
   - main

   pool:
     vmImage: ubuntu-latest

   steps:

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
         aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 238974323615.dkr.ecr.eu-central-1.amazonaws.com

   # build container images with docker commands
   - task: Bash@3
     displayName: 'Build and push docker image'
     inputs:
       targetType: 'inline'
       script: |
         gulp build
         # set common vars
         aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 238974323615.dkr.ecr.eu-central-1.amazonaws.com
         aws ecr list-images --repository-name connectivitytools --region eu-central-1

         image="238974323615.dkr.ecr.eu-central-1.amazonaws.com/connectivitytools"
         docker buildx create --driver=docker-container --name=container-builder

         # build giga image
         imageTag=giga
         newimage="238974323615.dkr.ecr.eu-central-1.amazonaws.com/connectivitytools/${imageTag}"
         cacheTag=cache-${imageTag}
         cd ./dist
         docker build          --cache-to=type=registry,ref=${newimage}:${cacheTag},mode=max,image-manifest=true,oci-mediatypes=true          --cache-from=type=registry,ref=${newimage}:${cacheTag}          --builder container-builder          -t ${newimage}:${imageTag}-build-$(Build.BuildId)          -t ${newimage}:${imageTag}          -t ${newimage}:dev          --push          -f Dockerfile.aws          --progress=plain          ./
         docker image ls
         aws ecr list-images --repository-name connectivitytools --region eu-central-1

         cd ../server

         # build giga-api image
         imageTag=giga-api
         newimage="238974323615.dkr.ecr.eu-central-1.amazonaws.com/connectivitytools/${imageTag}"
         cacheTag=cache-${imageTag}
         docker build          --cache-to type=registry,ref=${newimage}:${cacheTag},mode=max,image-manifest=true,oci-mediatypes=true          --cache-from type=registry,ref=${newimage}:${cacheTag}          --builder container-builder          -t ${newimage}:${imageTag}-build-$(Build.BuildId)          -t ${newimage}:${imageTag}          -t ${newimage}:dev          --push          -f Dockerfile.web          --progress=plain          ./

         # build giga-calc-worker image
         imageTag=giga-calc-worker
         newimage="238974323615.dkr.ecr.eu-central-1.amazonaws.com/connectivitytools/${imageTag}"
         cacheTag=cache-${imageTag}
         docker build          --cache-to type=registry,ref=${newimage}:${cacheTag},mode=max,image-manifest=true,oci-mediatypes=true          --cache-from type=registry,ref=${newimage}:${cacheTag}          --builder container-builder          -t ${newimage}:${imageTag}-build-$(Build.BuildId)          -t ${newimage}:${imageTag}          -t ${newimage}:dev          --push          -f Dockerfile.calc          --progress=plain          ./

   - task: AWSShellScript@1
     displayName: 'ECR'
     inputs:
       regionName: 'eu-central-1'
       scriptType: inline
       inlineScript: |
         aws ecr list-images --repository-name connectivitytools --region eu-central-1
         aws ecr get-login-password --region eu-central-1 | docker login --username AWS --password-stdin 238974323615.dkr.ecr.eu-central-1.amazonaws.com
   ```

## Step 3: Push the Pipeline to GitHub/Azuredevops

- Add the `azure-pipelines.yml` file to the root of your project repository.
- Push the changes to your GitHub / Azure devops repository.

## Step 4: Run the Pipeline :

**Please note:** 

The pipeline works on the main branch. The guide below is if you want to run from the modified branch

1. **Trigger the Pipeline**:

   - Navigate to **Pipelines** in Azure DevOps and click **Run Pipeline**.
   - Ensure the pipeline runs on the latest `modified` branch and starts building and pushing Docker images to AWS ECR.
2. **Monitor Progress**:

   - Watch the logs in Azure DevOps to ensure the pipeline completes successfully.
   - Confirm that the Docker images have been pushed to AWS ECR by checking the AWS Management Console under **ECR**.

## Step 5: Verify in AWS ECR

1. **Login to AWS**:
   - Open the AWS Management Console and navigate to **ECR**.
   - Ensure that the repository `connectivitytools` has the newly built Docker images tagged and available.

## Conclusion

You have now successfully set up an Azure DevOps pipeline that builds Docker images and deploys them to AWS ECR. This automated pipeline ensures that any changes pushed to your GitHub repository are automatically built and deployed to your AWS infrastructure.

---
