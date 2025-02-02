- - - 
Docker
- apps are packaged in containers that can run on any OS
	- runs on any machine
	- predictable behavior
	- less work
	- easy to maintain and deploy
	- runs on any OS, any technology

Docker images are stored in docker repositories
- Docker hub 
	- Public repo 
	- base images for many technologies
- Amazon ECR
	- Private repository

![[Pasted image 20240919155659.png|400]]

Docker Container Management on AWS

1. Amazon ECS - Elastic Container Service
2. Amazon EKS - Elastic Kubernetes Service
3. AWS Fargate
4. Amazon ECR - stores container images

---
### Amazon ECS

###### **EC2 Launch Type**

ECS - Elastic Container Service 

- launch ECS tasks on ECS Clusters
- EC2 launch type - for maintaining the infrastructure 
- each ec2 instance runs the ECS agent to register in the ECS cluster

![[Pasted image 20240919160430.png|300]]

###### Fargate Launch Type

- No EC2 instances to manage i.e No infrastructure is provided
- it's serverless
- AWS runs ECS tasks for you based on CUP/RAM needed
- To scale, just increase the number of tasks

![[Pasted image 20240919160855.png|200]]

**Amazon ECS - Load Balancer Integrations** 

Objective: Expose ECS Tasks to HTTP/HTTPS endpoint 
Solution: use load balancer 

- Application Load Balancer - supports most use cases
- Network Load Balancer - High throughput/ High performance 
- Classic load balancer - not recommended, doesn't work with fargate

![[Pasted image 20240919161423.png|300]]

**Amazon ECS - Data Volumes (EFS)**

- mount EFS file systems onto ECS tasks
- works for both EC2 and Fargate launch types
- Fargate + EFS = Serverless
- ECS tasks in different regions can share data from same EFS

![[Pasted image 20240919161702.png|200]]

UseCase : persistent MultiAZ shared storage for containers  

---
### ECS Service Auto Scaling 

**AWS Application auto scaling** - increases or decreases no of tasks

- Automatically increase/decrease the number of ECS tasks
- Amazon ECS auto scaling uses <mark style="background: #BBFABBA6;">AWS application auto scaling</mark> 
	- ECS avg CPU utilization
	- ECS avg memory utilization
	- ALB request count per target

Three ways of scaling 
- Target Tracking 
- Step scaling 
- scheduled scaling

**EC2 Launch Type - Auto Scaling EC2 Instances** - inc/dec EC2 instances

- Auto Scaling Group Scaling 
	- Scale ASG based on CPU utilization 
- ECS cluster capacity provider
	- automatically provision and scale infrastructure for ECS tasks

![[Pasted image 20240919183252.png|500]]

---
### Amazon ECR 

- ECR - Elastic Container Registry
- Store and manage docker images on AWS
- integrated with ECS backed up by Amazon S3
- Access is controlled through IAM Roles

![[Pasted image 20240919185521.png|200]]

---
### Amazon EKS

EKS - Elastic Kubernetes Service 

- launch managed kubernetes clusters on AWS
- Alternative to ECS, similar goal but different API
- usecase: when you have running kubernetes on premise or on any other cloud platform and your want to migrate to aws

- Supports 2 launch modes : EC2 and fargate
- <mark style="background: #BBFABBA6;">EKS pods</mark> = ECS tasks 

**Amazon EKS - Node Types**

- Managed Node Groups - Nodes are created and managed by EKS
- Self Managed Nodes - Nodes are created and managed by you, and you'll register it with EKS cluster 
- AWS fargate - No nodes managed (serverless)

---

Date: 19/09/2024
Vivek Malapaka

---
