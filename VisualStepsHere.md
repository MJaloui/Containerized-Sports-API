![github-header-image (1)](https://github.com/user-attachments/assets/fb42157b-093a-420d-8b69-372b0c74496f)

&nbsp;

&nbsp;

&nbsp;

&nbsp;




## **Setup Instructions**

### **Prerequisites**

### **1. Sign up for a free account and subcription with Serpapi to get an API key.**

  - **Go to [Serpapi](https://serpapi.com/)  website and register, confirm registartion.**

![image](https://github.com/user-attachments/assets/993a785e-d035-427e-9f29-4c3e3862ad02)

![image](https://github.com/user-attachments/assets/bf5b68a2-b0f3-4f04-9ec7-63e21b9e8515)

  - **Confirm registration in email and verify phone number.**

![image](https://github.com/user-attachments/assets/adfc7c58-2259-4e6a-97ff-20410c78704e)

  - **Click "Verify phone number" and enter your phone number.**

![image](https://github.com/user-attachments/assets/dc4b3d83-e47d-4e55-bbbd-0c35eca88a8e)

  - **Enter verification number sent to your phone. You will be notified a successfull confirmation.**

![image](https://github.com/user-attachments/assets/81abe92e-890b-4156-8535-e5d3cbe547dd)

![image](https://github.com/user-attachments/assets/d8de2e89-79ed-4db7-b924-d03990fa26b0)

**2. Must have an AWS Account & have basic understanding of ECS, API Gateway, Docker & Python.**

  - **Verfiy if you have AWS CLI installed using the "version" command**

![image](https://github.com/user-attachments/assets/d1dc16e9-d75c-4615-92fb-1c56f3cba5c4)



  - **If AWS CLI is not installed, you will not see any output. Use the "Pip install" command to install AWS CLI.**


```bash
pip install aws cli
```

  - **Configure AWS**

    - The information needed can be found in your AWS account, you may need to create a Secret Access Key if you don't already have one. Input "json" for your format.

```bash
aws configure
```

![image](https://github.com/user-attachments/assets/974a2958-7609-4e61-84e7-ecf249a8b55d)


**3. Install Serpapi library in local environment.**

```bash
pip install google-search-results
```

![image](https://github.com/user-attachments/assets/c4a8f41c-1758-4765-b2b1-aa90aead0634)


**4. Docker CLI and Desktop Installed: To build & push container images.**


  - Verify Docker is installed. If docker is not installed, no output will be returned.

```bash
docker --version
``

  - If not output was returnted, Docker is not installed. Enter these commands below to install.

  - First, update system to ensure everything is up to date. 

```bash
sudo apt-get update
```

![image](https://github.com/user-attachments/assets/e1746c65-39b4-4cb1-a1f1-ce820c2f5218)


  - **Install Docker.**

```bash
sudo apt install docker.io
```

![image](https://github.com/user-attachments/assets/bc4c64c1-ba16-4064-b115-05d80ca1bf04)



  - **Enable Docker.**

```bash
sudo systemctl enable docker
```

![image](https://github.com/user-attachments/assets/aacb8840-10cf-463c-aa7b-05e2af68e730)



  - **Verify Docker is enabled.**

```bash
systemctl status docker
```

![image](https://github.com/user-attachments/assets/00d29a33-354b-4321-8383-884bfe2fb92f)


  - **Start Docker, enter password.**

```bash
systemctl start docker
```

![image](https://github.com/user-attachments/assets/fef786df-5efc-4dd6-9ee0-68b7940a2511)



  - **Run Docker to verify everthing is working correctly. A message will display it's working coreclty if it's functioning correctly.**

    ```bash
    sudo docker run hello-world
    ```

![image](https://github.com/user-attachments/assets/90828797-069c-47c1-85ee-3dc298e9f402)



&nbsp;

&nbsp;

---

&nbsp;

&nbsp;

### **Steps:*

&nbsp;

&nbsp;

### **1. Clone this Repository**
```bash
git clone https://github.com/MJaloui/Containerized-Sports-API.git
cd containerized-sports-api
```



### **2. Create ECR Repository**

```bash
aws ecr create-repository --repository-name sports-api --region us-east-1
```

![image](https://github.com/user-attachments/assets/3f995caa-531c-4b2b-a6f5-42c26af25a03)

    - Verify the repository was created in "Amazon ECR > Private registry > Repositories".
    
![image](https://github.com/user-attachments/assets/53fa314c-ec2d-4fe9-b06b-66860fa8c918)

![image](https://github.com/user-attachments/assets/7a0c421c-8f82-4553-86ef-abbaf3fb7aa1)




### **3. Authenticate Build, and Push the Docker Image**

```bash
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com
```

![image](https://github.com/user-attachments/assets/281df540-477a-45d7-8011-06d3b14cade4)


```bash
sudo docker build --platform linux/amd64 -t sports-api .
```

![image](https://github.com/user-attachments/assets/1b2a5aa0-9a45-4310-a9ae-bf0b142a5cb7)


```bash
docker tag sports-api:latest <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/sports-api:sports-api-latest
```

![image](https://github.com/user-attachments/assets/e06caec4-1559-4d30-a46a-54963424014d)


```bash
docker push <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/sports-api:sports-api-latest
```

![image](https://github.com/user-attachments/assets/c71d48b3-e449-4e3a-a966-22a61ff2b011)

  - **Verify the image was created, go to Elastic Container Registry > Images > Sports-API.**

![image](https://github.com/user-attachments/assets/2e137f55-a784-4b4c-a73b-2683888d6250)

![image](https://github.com/user-attachments/assets/639ace6f-25c0-4a97-9ded-e059a5ccbe4d)



### **4. Set Up ECS Cluster with Fargate**

1. Create an ECS Cluster:
   
- Go to the ECS Console → Clusters → Create Cluster

![image](https://github.com/user-attachments/assets/5150bc63-2ebf-4ec3-8e74-39ceaad135b8)

![image](https://github.com/user-attachments/assets/f63673c6-ab07-41a2-a663-7a3d15729ef3)

![image](https://github.com/user-attachments/assets/e7afb0f9-e747-45f9-88fc-fcf2352cb740)

- Name your Cluster (sports-api-cluster)

![image](https://github.com/user-attachments/assets/1f60bfd6-77f5-4e11-a2d0-2c7d2b9bd295)


  
- For Infrastructure, select Fargate, then create Cluster. It it was succesfull, a green successfull banner will be displayed.

![image](https://github.com/user-attachments/assets/82de2cb4-481f-4ac8-8c48-5c06bd50ef4c)

![image](https://github.com/user-attachments/assets/a566f0a4-3926-4aa1-956f-714b72a33341)

![image](https://github.com/user-attachments/assets/33ef31e7-03a8-4a55-9e3b-1b711b41f20f)


2. Create a Task Definition:

- Go to Task Definitions → Create New Task Definition.

![image](https://github.com/user-attachments/assets/c4e04d81-d0fc-4500-8568-44d6d636908d)

![image](https://github.com/user-attachments/assets/efa613d4-d2b7-476f-b8d2-3774d24c1fa3)


- Name your task definition (sports-api-task)
- For Infrastructure, select Fargate
- Add the container:
  - Name your container (sports-api-container)
  - Image URI: <AWS_ACCOUNT_ID>.dkr.ecr.us-east-1.amazonaws.com/sports-api:sports-api-latest
  - Container Port: 8080
  - Protocol: TCP
  - Port Name: Leave Blank
  - App Protocol: HTTP
- Define Environment Eariables:
  - Key: SPORTS_API_KEY
  - Value: <YOUR_SPORTSDATA.IO_API_KEY>
  - Create task definition
3. Run the Service with an ALB
- Go to Clusters → Select Cluster → Service → Create.
- Capacity provider: Fargate
- Select Deployment configuration family (sports-api-task)
- Name your service (sports-api-service)
- Desired tasks: 2
- Networking: Create new security group
- Networking Configuration:
  - Type: All TCP
  - Source: Anywhere
- Load Balancing: Select Application Load Balancer (ALB).
- ALB Configuration:
 - Create a new ALB:
 - Name: sports-api-alb
 - Target Group health check path: "/sports"
 - Create service
4. Test the ALB:
- After deploying the ECS service, note the DNS name of the ALB (e.g., sports-api-alb-<AWS_ACCOUNT_ID>.us-east-1.elb.amazonaws.com)
- Confirm the API is accessible by visiting the ALB DNS name in your browser and adding /sports at end (e.g, http://sports-api-alb-<AWS_ACCOUNT_ID>.us-east-1.elb.amazonaws.com/sports)

### **Configure API Gateway**
1. Create a New REST API:
- Go to API Gateway Console → Create API → REST API
- Name the API (e.g., Sports API Gateway)

2. Set Up Integration:
- Create a resource /sports
- Create a GET method
- Choose HTTP Proxy as the integration type
- Enter the DNS name of the ALB that includes "/sports" (e.g. http://sports-api-alb-<AWS_ACCOUNT_ID>.us-east-1.elb.amazonaws.com/sports

3. Deploy the API:
- Deploy the API to a stage (e.g., prod)
- Note the endpoint URL

### **Test the System**
- Use curl or a browser to test:
```bash
curl https://<api-gateway-id>.execute-api.us-east-1.amazonaws.com/prod/sports
```
