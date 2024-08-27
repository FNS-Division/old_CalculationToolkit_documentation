This guide provides instructions for deploying the Dockerized Calculation Tools project to AWS.

## 1. Prerequisites

Before deploying to AWS, ensure you have the following:

* **AWS Account** : An AWS account with appropriate permissions.
* **AWS CLI** : Install and configure the AWS CLI on your local machine.
* **Docker Installed** : Ensure Docker is installed and running on your local machine.

## 2. Pushing Docker Images to AWS ECR

### 2.1 Set Up Amazon ECR

1. **Create an ECR Repository** :

* Navigate to the Amazon ECR console.
* Create a new repository for your Docker images (e.g., `calculation-tools-repo`).

### 2.2 Authenticate and Push Docker Images

1. **Authenticate Docker to ECR** :

* Run the following command to authenticate Docker with ECR:
  <pre><div class="dark bg-gray-950 rounded-md border-[0.5px] border-token-border-medium"><div class="flex items-center relative text-token-text-secondary bg-token-main-surface-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md"><span>bash</span><div class="flex items-center"><span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button></span></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-bash">aws ecr get-login-password --region <region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<region>.amazonaws.com
  </code></div></div></pre>

1. **Tag and Push Your Docker Image** :

* Tag the Docker image for your project:
  <pre><div class="dark bg-gray-950 rounded-md border-[0.5px] border-token-border-medium"><div class="flex items-center relative text-token-text-secondary bg-token-main-surface-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md"><span>bash</span><div class="flex items-center"><span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button></span></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-bash">docker tag calculationtools_api-backend <aws_account_id>.dkr.ecr.<region>.amazonaws.com/calculation-tools-repo:latest
  </code></div></div></pre>
* Push the Docker image to the ECR repository:
  <pre><div class="dark bg-gray-950 rounded-md border-[0.5px] border-token-border-medium"><div class="flex items-center relative text-token-text-secondary bg-token-main-surface-secondary px-4 py-2 text-xs font-sans justify-between rounded-t-md"><span>bash</span><div class="flex items-center"><span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button></span></div></div><div class="overflow-y-auto p-4" dir="ltr"><code class="!whitespace-pre hljs language-bash">docker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/calculation-tools-repo:latest
  </code></div></div></pre>

## 3. Deploying Docker Containers on AWS

### 3.1 Using Amazon ECS

1. **Create an ECS Cluster** :

* Go to the Amazon ECS console and create a new cluster.

1. **Define a Task Definition** :

* Create a new task definition specifying the container image from ECR, along with CPU, memory, and networking configurations.

1. **Run the Task** :

* Deploy the container by running the task in the ECS cluster.

### 3.2 Auto-Scaling and Load Balancing

1. **Configure Auto Scaling** :

* Set up auto-scaling for your ECS service based on CPU and memory usage.

1. **Set Up a Load Balancer** :

* Use an Application Load Balancer (ALB) to distribute traffic across multiple containers.

## 4. Post-Deployment Tasks

### 4.1 Monitoring and Logging

* Use Amazon CloudWatch to monitor your ECS cluster and containers.
* Set up CloudWatch Logs to capture and analyze container logs.

### 4.2 Security Configuration

* Use AWS IAM roles to ensure containers have the least privilege necessary.
* Configure security groups and network ACLs to control inbound and outbound traffic.

## 5. Maintenance and Updates

### 5.1 Updating Containers

* **Rebuild and Push** : When updates are made, rebuild the Docker image and push it to ECR.
* **Rolling Updates** : Deploy updates using ECS with minimal downtime.

### 5.2 Backup and Recovery

* Regularly back up any persistent data stored in AWS services.
* Document and test recovery procedures.
