# Github + Azure DevOps Setup

This section details the Azure DevOps pipeline setup for the Calculation Tools. The setup works for both the old and modified versions of the project.

This setup assumes you only want to setup a pipeline between a **github or Azure repository and AzureDevops pipeline.**

Your project should be hosted on a github / azure repository for simplicity

All the codes can be managed directly on your localhost and Push to GitHub , or directly edit from github and commiting the changes will automatically trigger Azure DevOps Pipelines to process the update

**Quick references and additional Video learning guides :**

 [GITHUB &amp; AZURE pipeline connection ( Video tutorial )](https://www.youtube.com/watch?v=AE4Q4A0ZVwA)

[AZURE pipeline VS CODE extension ](https://marketplace.visualstudio.com/items?itemName=ms-azure-devops.azure-pipelines)(Reccomended extension to have )

## Prerequisites.

Before starting, ensure you have:

1. **Azure DevOps Account**: For setting up the pipeline and managing CI/CD.
2. **GitHub Repository**: Where your project and configuration files are hosted.
3. **Docker**: Installed locally or on the build machine. ( Optional )

## Step 1: Access Your Azure DevOps Repository

1. **Visit the Repository**: Navigate to your repository on Azure DevOps:
   [Azure DevOps Repository: Calculation Tools](https://dev.azure.com/ITUINT/ConnectivityToolkit/_git/calculation-tools).
2. **Ensure Pipeline Files Are in the Root Directory**:

   - The `azure-pipelines.yml` and `docker-compose.yml` files should be in the root of the repository.
   - Ensure that your project structure is correctly aligned so Azure DevOps can detect the files for automated builds.

## Step 2: Azure DevOps Pipeline Setup

Ensure you have **azure-pipeline.yml** in your files. If not, [check this file and copy the pipeline here](https://ituint.sharepoint.com/:w:/r/sites/UIUXandFrontEnd/_layouts/15/Doc.aspx?sourcedoc=%7BB8FE9875-9103-4FC4-B289-463EBC751C7B%7D&file=Azure%20devops%20setup.docx&action=default&mobileredirect=true)

1. **Go to Pipelines**:

   - On your Azure DevOps project dashboard, go to **Pipelines** > **New Pipeline**.
2. **Select GitHub Repository**:

   - Choose **GitHub** as the source repository.
   - If you have already connected Azure DevOps to GitHub, select your repository (`calculation-tools`) from the list.
3. **Detect `azure-pipelines.yml`**:

   - Azure DevOps will automatically detect the `azure-pipelines.yml` file in your repository root.
   - This file contains the necessary steps to build and push Docker images based on the configuration provided.

## Step 3: Review Your `azure-pipelines.yml`

The `azure-pipelines.yml` file is already configured as you provided, and it will handle the automation of the following:

- **Docker Image Building**: Builds the Docker images using your `docker-compose.yml` file.
- **Environment Setup**: Sets up AWS environment variables required for authentication (assuming AWS is part of the environment).

## Step 4: Review Your `docker-compose.yml`

The `docker-compose.yml` file you shared is also structured to define the services in your Docker container environment.

- **Services**:
  - `mysql`: Runs a MySQL database service.
  - `nginx`: Runs an NGINX web server.
  - `api-frontend2` and `api-backend`: Configures the frontend and backend API services.
  - `rabbitmq`: Configures the RabbitMQ messaging service.

## Step 5: Run the Pipeline

1. **Save and Run**:

   - After setting up the pipeline, Azure DevOps will automatically trigger the pipeline when changes are made to the repository (specifically the `main` branch).
   - You can manually run the pipeline by navigating to **Pipelines** in Azure DevOps and clicking **Run Pipeline**.

   A successful setup should look something like this [( Link )](https://dev.azure.com/ITUINT/ConnectivityToolkit/_build/results?buildId=2152&view=logs&j=12f1170f-54f2-53f3-20dd-22fc7dff55f9)
2. **Monitor Progress**:

   - You can monitor the pipeline execution in real-time on the Azure DevOps dashboard.
   - Logs will be available for each step, showing the build and deployment stages of your pipeline.

#### **Screenshots**

---

[https://prnt.sc/wQfH3T1BgwKl ]()

[https://prnt.sc/5Bk6X7kMIxnZ]()

[https://prnt.sc/iQi9vtyQQKl1]()

[https://prnt.sc/M5CuRUMx7tzP]()

## Conclusion

By following these steps, you’ve now successfully connected your GitHub repository to Azure DevOps and set up a CI/CD pipeline using your `azure-pipelines.yml` and `docker-compose.yml` files. Depending on the setup, Each time you push new changes to the `modified` branch, the pipeline will automatically build and deploy your services using Docker.
