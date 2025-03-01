# Containerized Sports API Management System

![image](https://github.com/user-attachments/assets/bfb10401-6356-41ab-9203-bfdcbee4efa2)



## **🔷 Project Highlights 🔷**

🏀 This project builds a containerized API management system for querying real-time sports data.

🏀 It leverages **Amazon ECS (Fargate)**, **Amazon API Gateway**, **Docker**, and an external **Sports API** to manage and query sports data securely and efficiently.

🏀 Demonstrates how to use **AWS Cloud** to deploy a containerized backend and expose a REST API for seamless user interaction with real-time data.

---

## **🔧 Capabilities 🔧**

🔹 Exposes a REST API for querying live sports data.

🔹 Runs a containerized backend using **Amazon ECS with Fargate** for scalable and serverless architecture.

🔹 Manages and routes API requests securely through **Amazon API Gateway**.

🔹 Uses Docker for containerization, simplifying the deployment process.

🔹 Built with IAM security practices, following the principle of least privilege for ECS task execution and API Gateway.

---

## **🚨 Technologies 🚨**

🔹 **Cloud Provider**: AWS

🔹 **Core Services**: Amazon ECS (Fargate), API Gateway, CloudWatch

🔹 **Containerization**: Docker

🔹 **Programming Language**: Python 3.x

🔹 **IAM Security**: Custom least privilege policies for ECS task execution and API Gateway

---

## **👀 Instructions 👀**

**🔹 Prerequisites 🔹**

🔹 **Sports API Key**: Sign up for a free account and subscription & obtain your API Key at [serpapi.com](https://serpapi.com)

🔹 **AWS Account**: Create an AWS account & have basic understanding of ECS, API Gateway, Docker & Python

🔹 **AWS CLI Installed and Configured**: Install & configure AWS CLI to interact programmatically with AWS.

🔹 **Serpapi Library**: Install Serpapi library in the local environment: `pip install google-search-results`

🔹 **Docker CLI and Desktop Installed**: To build & push container images.

### **Steps:** ➡️❗ [Click Here To View Detailed Visual Steps](https://github.com/MJaloui/Containerized-Sports-API/blob/main/VisualStepsHere.md) ❗⬅️
   
**Set Up ECS Cluster with Fargate**

1. Clone the Repository.

2. Create ECR Repo.

3. Authenticate Build and Push the Docker Image.

4. Create an ECS Cluster

5. Create a Task definition

6. Define Environment Variables

7. Run the Service with an ALB.

8. Test the ALB.


**Configure API Gateway**

1. Create a New REST API.

2. Set Up Integration.

3. Deploy the API.

4. Use curl or a browser to test the system.


---

✔️ Keynotes ✔️

🔹 Deploying a containerized backend using Amazon ECS (Fargate) for scalability.

🔹 Managing and routing API requests securely with Amazon API Gateway.

🔹 Utilizing Docker to simplify containerized deployments.

🔹 Implementing IAM least privilege policies for ECS task execution and API Gateway security.

🔹 Querying real-time sports data through an external Sports API.


🌱 Opportunities for Growth 🌱

🔹 Implement API rate limiting to prevent abuse and optimize performance.

🔹 Add Amazon ElastiCache for caching frequent API requests and reducing response time.

🔹 Integrate DynamoDB to store user-specific queries and preferences for personalized experiences.

🔹 Secure API Gateway with API keys or IAM-based authentication for controlled access.

