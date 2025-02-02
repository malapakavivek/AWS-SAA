- - - 
### CloudWatch Metrics

- provides metrics for AWS services 
- metric is a variable which is monitored
	- dimension is an attribute to the metric
	- can have <mark style="background: #BBFABBA6;">30 dimensions</mark> per metric
- have timestamps
- can create a dashboard of metrics

**CloudWatch Metric Streams**

- can send all the cloudwatch metrics to a destination with low latency and near real time delivery 
	- Send it to kinesis firehose
	- or to any 3rd party service provider

- option to send all the metrics or filter metrics to only stream a subset 

![[Pasted image 20240924093610.png|200]]

---
### CloudWatch Logs

- Log Groups: name, representing an application
- Log Stream: instance within application/container 
- can define log expiration policy (1 day to 10 yrs)
- 
- Can send data to:
	- s3
	- kinesis firehose
	- kinesis data streams
	- lambda
	- opensearch
- encrypted at default.

**CloudWatch Logs Insights**
- search for a log stored in cloudwatch logs
- Query a log in cloudwatch logs
- specify time frame 
- can save multiple queries and add them to a dashboard

- provides a purpose built query language 
- it's a <mark style="background: #BBFABBA6;">query engine</mark> not a real time engine 

**CloudWatch Logs Subscription**
- get real time log events from cloudwatch logs for processing 
- send data to kinesis data firehose , data streams or lambda function.

- Subscription Filter - filter logs which you want to be delivered at your destination.

![[Pasted image 20240924094933.png|500]]

can send logs from multiple accounts and multiple regions into a single bucket/ service using subscription filter

![[Pasted image 20240924095154.png|500]]

Cross Account subscription : send log events to recourse in different AWS account 

![[Pasted image 20240924095234.png|400]]

---
### CloudWatch Logs for EC2

- default --> no logs from EC2 will go to cloudwatch 
- need a cloudwatch agent for EC2 to send log files
- Correct IAM permissions must be given 
- can be set up on on-premise servers too. 

![[Pasted image 20240924100036.png|200]]

**CloudWatch Log Agent & Unified Agent**

- Cloudwatch Log Agent 
	- Older version 
	- can only send to cloudwatch logs

- Cloudwatch Unified Agent 
	- newer version
	- collects additional metrics and also logs 
	- collects logs and send to cloudwatch logs
	- can be configured using SSM parameter store 
	- Metrics it can log 
		- CPU
		- Disk Metrics
		- RAM
		- Netstat
		- Processes
		- Swap Space
	- if you need more granular level data - think unified agent 

---

### CloudWatch Alarms 

- use alarm to trigger notifications for any metric
- options - sampling, %, Min, Max
- Alarm State:
	- OK - not triggered
	- insufficient data
	- ALARM - triggered
- Period - length of time you want to evaluate the metric

**CloudWatch Alarm Targets**
- Stop, terminate, reboot or recover EC2 
- trigger auto scaling action
- send notification to SNS 

**Composite Alarms**
- cloudwatch alarms are on a single metric
- composite alarms monitor states of multiple other alarms
- AND and OR conditions - we have to define
- create complex composite alarms and reduce "alarm noise"

![[Pasted image 20240924103556.png|400]]

**EC2 instance recovery**
- Status checks
	- Instance status - Check EC2 VM
	- system status - check underlying hardware
	- EBS check - check attached EBS volume 

If status checks are breached - we do instance recovery 
- same private, public, elastic IP, placement groups are assigned with recovery happens 

![[Pasted image 20240924104105.png|400]]

---
### Amazon EventsBridge (CloudWatch Events)

- Schedule : Corn jobs

![[Pasted image 20240924104701.png|400]]

- Event Pattern : react to a service doing something

![[Pasted image 20240924104738.png|400]]

- Trigger lambda functions, send SNS, SQS messages etc

![[Pasted image 20240924105031.png|500]]


---
### CloudWatch Insight 


**CloudWatch Container Insights**

- collect, aggregate, summarize metrics and logs from container 
	- ECS
	- EKS
	- kubernetes platform on EC2
	- fargate
- make dashboards from the data 

**CloudWatch Lambda Insight**

- monitor and troubleshoot serverless applications running on lambda
- collect system level metrics  - CPU Time, memory and network 
- collects summarize and aggregate info such as cold starts and lambda worker shutdowns
- create dashboards 

**CloudWatch Contributor Insight**

- analyze log data and display contributor data 
	- see metrics about top N contributors 
	- total number of unique contributors
- identify heaviest network users or URL's that generate most errors

![[Pasted image 20240924121226.png|200]]

**CloudWatch Application Insight** 
- automatic dashboards to troubleshoot your application and related AWS service 

---
### AWS CloudTrail

- provide governance, compliance for aws account 
- enabled by default
- get a history of events/API calls made within your AWS account
- can put from cloudtrail to cloudwatch logs or s3
- can be applied to all regions or single region 

![[Pasted image 20240924163404.png|400]]


**CloudTrail Events** 

- Management events 
	- operations that are performed on resources in your aws account 
		- configure security
		- setting up logging 
		- configure rules for routing data
	- Can separate read events (don't modify resources) and write events (modifies resources)

- Data Events
	- By default, data events are not logged (high volume of operations)
	- S3 object level activity (get obj, create obj, delete obj) can separate read from write
	- lambda function execution activity

- CloudTrail Insight Events
	- analyze cloudtrail insights and detect unusual activity
	- first analyze normal management events to create a reference
	- then continuously analyze write events to detect unusual patterns


**CloudTrail Events Retention**

- events are stored for 90 days in cloudtrail
- to keep beyond 90, log them in s3, use athena for analysis 

![[Pasted image 20240924164427.png|400]]

---

Date - 24/09/2024
Vivek Malapaka

---

