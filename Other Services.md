- - - 
### CloudFormation 

- declarative way of outlining AWS infrastructure 
	- i want a security group
	- i want 2 ec2 instances using the security group
	- i want an s3 bucket 
	- want a load balancer in front of these machines 
- cloudformation will create these for you in the exact order and configuration specified 

**Benefits of CloudFormation** 

- infrastructure as a code: 
	- never create resources manually 
	- changes to infra are through code 

- cost
	- can estimate the cost of your resources using cloudformation template 
	- savings : automatically delete templates at 5PM and recreate at 8AM next day 

 - productivity 
	 - ability to destroy and recreate an infra on the cloud 
	 - automated generation of diagram for your templates

---
### CloudFormation - Service Role 

- IAM role that allows cloudformation to delete/update/create stack resources on your behalf 
- gives users permissions to makes changes in the stack resource even if they don't have permission to work directly with the resource in the stack

---
### Amazon Simple Email Service (SES)

- send emails, securely, globally and at scale 
- allows inbound/outbound emails 
- reputation dashboard, performance insights 
- provides statistics such as email delivery, email open
- send emails using aws console, API or SMTP

use case: transactional, marketing and bulk email communication 

--- 
### Amazon Pinpoint
- 2 way (inbound and outbound) marketing communication service
- supports email, SMS, voice and in app messaging 
- personalize messages with right content to customers
- possibility to receive replies 
- used to run campaigns by sending bulk transactional SMS messages

difference with Amazon SNS and SES
- in SNS and SES we manage each message's audience, content and delivery 
- in pinpoint, a template is created and delivery schedules 

![[Pasted image 20241001011628.png|200]]

--- 
### Cost Explorer and Cost Anomaly Detection 


Cost Explorer 

- **Purpose**: It helps users visualize, understand, and manage AWS costs and usage.

- **Features**:
    - **Historical Data**: Users can explore data for up to the past 13 months and forecast up to 12 months into the future.
    - **Custom Reports**: It allows for the creation of custom reports, where users can break down their spending by service, linked account, tag, or region.
    - **Usage Trends**: It helps identify usage patterns and provides insights into how resources are being consumed.
    - **Forecasting**: Provides cost forecasts based on historical data to help with future budgeting.

Cost Anomaly Detection

- **Purpose**: It automatically detects unusual spending patterns, enabling users to take timely action on unexpected costs

- **Features**:
    - **Anomaly Detection**: It uses machine learning algorithms to continuously monitor your AWS costs and usage, identifying any spending anomalies.
    - **Notification Alerts**: Users are alerted in real-time if there's a sudden spike or drop in usage that could lead to unexpected costs.
    - **Customizable**: Users can define what constitutes an anomaly based on certain thresholds, such as specific services or cost centers.

---
