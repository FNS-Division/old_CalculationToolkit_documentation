# This guide provides instructions for deploying the Dockerized Calculation Tools project to Azure.

## 1. Prerequisites

Before deploying to Azure, ensure you have the following:

* **Azure Account**: An Azure account with appropriate permissions.
* **Azure CLI**: Install and configure the Azure CLI on your local machine.
* **Docker Installed**: Ensure Docker is installed and running on your local machine.

## 2. Pushing Docker Images to Azure Container Registry (ACR)

### 2.1 Set Up Azure Container Registry

1. **Create an ACR**:

   * Navigate to the Azure portal.
   * Create a new Azure Container Registry (ACR) for your Docker images.

### 2.2 Authenticate and Push Docker Images

1. **Login to Azure Container Registry**:

   * Run the following command to authenticate Docker with ACR:

     ```
     az acr login --name <registry_name>
     ```

1. **Tag and Push Your Docker Image**:

   * Tag the Docker image for your project:

     ```
     docker tag calculationtools_api-backend <registry_name>.azurecr.io/calculation-tools-repo:latest
     ```

   * Push the Docker image to the ACR repository:

     ```
     docker push <registry_name>.azurecr.io/calculation-tools-repo:latest
     ```

## 3. Deploying Docker Containers on Azure

### 3.1 Using Azure Container Instances (ACI)

1. **Create a Container Group**:

   * In the Azure portal, create a new container group.
   * Specify the image from ACR and configure CPU, memory, and networking settings.

1. **Run the Container**:

   * Deploy the container by starting the container group.

### 3.2 Scaling and Load Balancing

1. **Configure Auto-Scaling**:

   * Set up auto-scaling for your container instances using Azure Monitor.

1. **Set Up a Load Balancer**:

   * Use an Azure Load Balancer to distribute traffic across multiple containers.

## 4. Post-Deployment Tasks

### 4.1 Monitoring and Logging

* Use Azure Monitor to track the performance of your container instances.
* Set up Azure Log Analytics to capture and analyze container logs.

### 4.2 Security Configuration

* Use Azure Role-Based Access Control (RBAC) to manage access to resources.
* Configure network security groups (NSGs) to manage inbound and outbound traffic.

## 5. Maintenance and Updates

### 5.1 Updating Containers

* **Rebuild and Push**: Rebuild the Docker image and push it to ACR when updates are made.
* **Rolling Updates**: Use Azure Kubernetes Service (AKS) or similar to deploy updates with minimal downtime.

### 5.2 Backup and Recovery

* Regularly back up any persistent data stored in Azure services.
* Document and test recovery procedures.
