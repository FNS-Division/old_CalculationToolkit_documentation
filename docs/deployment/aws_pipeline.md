This section provides details on deploying the Calculation Tools to AWS using the pipeline configured in Azure DevOps.

This setup assumes you have AWS Setup, AzureDevops Setup,  and a repository ( Github repository or azure repository)

The pipeline runs successfully  from the main branch [(View run tests here).](https://dev.azure.com/ITUINT/ConnectivityToolkit/_git/calculation-tools?path=/azure-pipelines.yml&version=GBmain&_a=history) This guide is to setup  from a modified branch

**Quick references and additional Video learning guides :**

[Old calculation toolkit deployment via AWS CLI  Documentation ( Setup by original developer on how to deploy on aws- Reccomended )](https://ituint.sharepoint.com/:w:/r/sites/ConnectivityModelling-Internship/_layouts/15/Doc.aspx?sourcedoc=%7B05EDF5A0-768B-475E-9DCC-A40C6623B153%7D&file=Calculationtools%20AWS%20Deployment%20Guide.docx&action=default&mobileredirect=true)

[Connect Azure DevOps Pipeline to AWS Cloud  ( VIDEO DEMO GUIDE )](https://www.youtube.com/watch?v=Vywmy5FFzoM)

[Setting up a continous  development pipeline between github and AWS (VIDEO DEMO GUIDE )](https://youtu.be/biYVW1TMYAU?t=373)

[VS CODE Extension to assist with pipeline deployment to AWS (Reccomended  )](https://marketplace.visualstudio.com/items?itemName=AmazonWebServices.aws-vsts-tools) - Requires Admin rights

## Prerequisites.

Before starting, ensure you have the following:

1. **Azure DevOps Account**: For setting up pipelines and service connections.
2. **AWS Account**: With permissions to access ECR and IAM roles for authentication.
3. **Docker**: Installed locally or in the build environment.
4. **AWS CLI**: Installed and configured for AWS access.

Guide to set this up: (https://ituint.sharepoint.com/:w:/r/sites/UIUXandFrontEnd/Shared%20Documents/General/Old%20Connectivity%20toolkit/Additionals/AWS%20SETUP.docx?d=wb2ec7e198d09499d9e574966665b2ad2&csf=1&web=1&e=yhla19 ) 

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
2. ### **Create the `azure-pipelines.yml` File**: ( [You can also find it in this link: This is the azure-pipeline from the main branch, but you can copy it to the modified branch  ](https://dev.azure.com/ITUINT/ConnectivityToolkit/_apps/hub/ms.vss-build-web.ci-designer-hub?pipelineId=79&branch=main))

   In the root directory of your repository, create the file `azure-pipelines.yml`.

 
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
