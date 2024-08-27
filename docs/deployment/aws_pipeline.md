This section provides details on deploying the Calculation Tools to AWS using the pipeline configured in Azure DevOps.

### AWS Resources Used

* **ECR (Elastic Container Registry)** : Used to store Docker images.
* **IAM Roles** : Used to manage permissions and access between Azure DevOps and AWS.
* **EC2 Instances or ECS** : Depending on your deployment architecture, these services can be used to run the Docker containers.

### Deployment Process

1. **Docker Image Build** : The Docker image for the application is built using the Azure DevOps pipeline.
2. **Authentication** : The pipeline uses IAM roles and identity tokens to authenticate with AWS and assume the necessary permissions.
3. **Push to ECR** : The Docker image is tagged and pushed to AWS ECR.
4. **Deploy to ECS or EC2** : Once in ECR, the image can be deployed to an ECS cluster or directly to EC2 instances.

### Detailed Steps

**Build the Docker Image** :

* The Docker Compose task in the pipeline builds the image as per the instructions in `docker-compose.yml`.


**docker-compose.yml** 

```
version: '2'

services:
  mysql:
    image: mysql:5.7.42
    platform: linux/amd64
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: giga
      MYSQL_USER: giga
      MYSQL_PASSWORD: LbceQM0NE6ZuhW57MExFl6N6b32BCvbG
    ports:
      - "3306:3306"
    volumes:
      - mysql-data:/var/lib/mysql
    networks:
      - app-network
  nginx:
    build:
      context: ./dist
      dockerfile: Dockerfile 
    depends_on:
      - api-frontend2
    ports:
      - "8000:8000"  
    networks:
      - app-network

  api-frontend2:
    build:
      context: ./server/
      dockerfile: Dockerfile.web
   # image: api-frontend2
    ports:
      - "8080:80"
    depends_on:
      - api-backend
    networks:
      - app-network

  api-backend:
    build:
      context: ./server/
      dockerfile: Dockerfile.calc
    depends_on:
      - rabbitmq
    networks:
      - app-network

  rabbitmq:
    image: rabbitmq:3-management
    ports:
      - "5672:5672"
      - "15672:15672"
    volumes:
      - ./rabbitmq_data:/var/lib/rabbitmq
    environment:
      - RABBITMQ_DEFAULT_USER=user
      - RABBITMQ_DEFAULT_PASS=password
    networks:
      - app-network

networks:
  app-network:
    driver: bridge

volumes:
  mysql-data:
```

**Authenticate with AWS** :

* Azure DevOps authenticates with AWS using the `AWSShellScript` task and assumes the necessary IAM role.

**Push the Image to ECR** :

* The image is tagged with the appropriate name and pushed to the specified ECR repository.

**Deploy the Image** :

* Depending on your setup, you can deploy the image manually or automate this step using an additional pipeline or service such as AWS CodeDeploy or ECS.
