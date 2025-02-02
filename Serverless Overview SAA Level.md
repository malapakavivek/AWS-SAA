- - -
### Introduction

- serverless doesn't mean there are no servers, it means we won't manage the servers anymore

serverless in aws
	- AWS lambda
	- DynamoDB
	- AWS Cognito
	- AWS API Gateway
	- Amazon S3
	- AWS SNS and SQS
	- Kinesis Data Firehose
	- Aurora Serverless
	- Fargate

---

### AWS Lambda

Difference between Amazon Ec2 and Amazon Lambda

| Amazon EC2                                | Amazon Lambda                  |
| ----------------------------------------- | ------------------------------ |
| Virutal servers in cloud                  | Virtual functions - no servers |
| Limited by RAM and CPU                    | Limited by time                |
| Runs Continuously                         | Runs on demand                 |
| Scaling means intervention to add servers | scaling is automated           |

**Benefits of AWS lambda**

- Easy pricing
	- Pay per request and compute time
	- free tire: 1,000,000 requests and 400,000 GBs of compute time
- Integrated with many programming languages
- Easy monitoring through cloudwatch
- easy to get more resources per function
- RAM (++) CPU and network also (++)

![[Pasted image 20240920101328.png|400]]

AWS lambda is very cheap to so it's very popular 

---
### AWS Lambda Limits

- Execution 
	- memory : 128 MB - 10 GB (1MB Increment)
	- max time : 900 Seconds (15 mins)
	- Environment variable : 4kb
	- concurrent executions : 1000
- Deployment
	- lambda function deployment size: (compressed) 50MB
	- lambda function deployment size: (uncompressed) 250MB

---
### Lambda SnapStart

- Improves lambda function performance up to 10x for java 11 and above

![[Pasted image 20240920103453.png|200]]

---
### Lambda@Edge and CloudFront Functions 

- many modern apps executes some form of logic at the edge 
- edge function
	- code that you write and attach to cloudfront application
	- runs close to users for minimal latency
- you don't have to manage any servers, deployed globally 
- pay per use
- fully serverless


**CloudFront Functions** 

- lightweight functions written in javascript
- high scale, latency sensitive 
- millions of requests per second
- change: 
	- Viewer request - after cloudfront receives request from viewer
	- viewer response - before cloudfront sends response to viewer
- max memory - 2MB

![[Pasted image 20240920104406.png|150]]

**Lambda@Edge Function**

- written in nodejs and python 
- 1000s of requests/sec
- change 
	- viewer request
	- origin request
	- origin response
	- viewer response
- max memory - 10GB

![[Pasted image 20240929213222.png|500]]

---
### Amazon DynamoDB 

- fully managed db, highly available, available across multiple AZ's
- NoSQL database
- scales to massive workloads
- <mark style="background: #BBFABBA6;">millions of requests</mark> per second
- fast and consistent 
- integrated with IAM 
- low cost and auto scaling 
- no maintenance, highly available 


- Dynamo DB is made of tables
- each table has primary key (partition key+ sort key)
- can have infinite number of rows
- each item has attributes (can be added over time)
- max item size is <mark style="background: #BBFABBA6;">400KB</mark>
- best for rapidly evolve schemas 

**Read/Write Capacity Modes** 

- Provisional Mode (default)
	- specify number of reads/writes per second
	- plan capacity beforehand
	- pay for provisioned RCU and WCU (CU- Capacity Units)
	- possible to add autoscaling mode
- On - Demand Mode
	- Read/write scales automatically according to workload
	- pay for what you use, more expensive 
	- great for unpredictable workloads and sudden spikes  

---
### DynamoDB - Advance Features 

**DynamoDB Accelerator (DAX)**

- Cache for DynamoDB
- solves read congestion by caching 
- <mark style="background: #BBFABBA6;">microsecond latency</mark> for cached data
- TTL is 5 mins by default (can change)
![[Pasted image 20240920124525.png|150]]

**DynamoDB - Stream Processing**

- Ordered stream of modifications in a table 
- Use case
	- welcome email to new customers
	- real time usage analytics
	- invoke lambda on changes to your dynamoDB 
- 24 hour retention 
- Limited # consumers

![[Pasted image 20240920124952.png|400]]

**DynamoDB Global Tables** 

![[Pasted image 20240920125117.png|300]]

- make tables accessible with low latency in multiple regions 
- active - active replication 
- can read and write to table in any region 
- must enable dynamoDB streams as a pre requisite

**DynamoDB - Time To Live (TTL)**

- items in the table are deleted after a while (TTL)
- use case: Delete data after 2 yrs, web session handling

![[Pasted image 20240920125416.png|200]]

**DynamoDB - Backups for Disaster Recovery** 

- continuous backups using point in time recovery (PITR)
- PITR to any time within the backup window
- enabled for 35 days 
- recovery process creates a new table 

- On demand backups - backups for long term retention 

**Integration with S3**

![[Pasted image 20240920125838.png|200]]

- Export to S3 - perform analysis on top of DynamoDB
	- does not affect any read capacity
- Import from S3
	- does not affect any write capacity

---

### API Gateway 

- AWS lambda + API Gateway = No infrastructure
- Handle API versioning 
- Handle different environments (prod,test,dev)
- Cache API responses
- authentication and authorization
- transform and validate requests and responses

API Gateway - Integrations
- lambda functions 
- HTTP -eg: ALB
- AWS service 

API Gateway - Endpoint Types:
- Edge Optimised - For Global clients
- Regional - clients in the same region
- Private - from within the VPC using VPC endpoint 

API Gateway - Security 
- User authentication through 
	- IAM Roles - (for internal applications)
	- Cognito - (for external users - mobile users)
	- Custom authorizer
- Custom Domain Name HTTPS
	- for edge optimized - certificate must be in us-east-1
	- for regional, the certificate must be in API gateway region 

---
### Amazon Cognito 

- gives users an identity to interact with web or mobile application 
- Cognito user pools:
	- sign in functionality
- Cognito identity pools (federated identity)
	- provide temp aws creds to users so they can access aws services 

**Cognito User Pool - (CUP)**

- serverless database of user for your web and mobile apps
	- sign in through user id and password 
	- MFA
- CUP integrates with API gateways and application load balancers 

![[Pasted image 20240920171735.png|500]]

**Cognito identity pools (federated identity)**

- users obtain temporary AWS credentials 
- users can access aws services through these credentials 
- the IAM policies applied to the credentials are defined in cognito
- Default IAM roles for authenticated users 

![[Pasted image 20240920172202.png|500]]

---

Date: 20/09/2024
Vivek Malapaka

---