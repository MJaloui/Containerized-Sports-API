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

    - Verify it was created in "Amazon ECR > Private registry > Repositories".
    
![image](https://github.com/user-attachments/assets/53fa314c-ec2d-4fe9-b06b-66860fa8c918)

![image](https://github.com/user-attachments/assets/7a0c421c-8f82-4553-86ef-abbaf3fb7aa1)




### **Authenticate Build, and Push the Docker Image**

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


### **Set Up ECS Cluster with Fargate**
1. Create an ECS Cluster:
- Go to the ECS Console → Clusters → Create Cluster
- Name your Cluster (sports-api-cluster)
- For Infrastructure, select Fargate, then create Cluster

2. Create a Task Definition:
- Go to Task Definitions → Create New Task Definition
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
