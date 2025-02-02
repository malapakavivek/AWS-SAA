- - - 
### Encryption 101

**Encryption in flight** (TLS/SSL)
- data is encrypted before sending and decrypted after receiving 
- TLS certification is used 
- ensures no Man In The Middle Attack can happen 

![[Pasted image 20240926103115.png|500]]

**Server side encryption at rest**
- data encrypted after received by server
- decrypted before being sent
- stored in encrypted form (using key)

![[Pasted image 20240926103318.png|500]]

**Client side encryption**
- both encrypted and decrypted at the client side 
- server shouldn't interfere 

![[Pasted image 20240926103433.png|500]]

---
### AWS KMS (Key Management Service)

- encryption for AWS service - think KMS
- AWS manages the keys for us 
- integrated with IAM
- able to audit KMS keys using cloudTrail
- never store secrets in plain text 
	- encrypt using KMS
	- then store in code/env variables 

**KMS Key Types**

- Symmetric (AES - 256)
	- single key used for encryption and decryption
	- AWS servers which use KMS use symmetric 
	- can never get access to they KMS key (must use KMS API)

- Asymmetric (RSA and ECC)
	- public (encryption) and private (decryption)
	- public key is downloadable, private is not
	- used when encryption is done outside of AWS by users who can't use KMS API 

how EBS volume with encryption is copied to another region

![[Pasted image 20240926104454.png|500]]

**KMS Key Policies**

- Default KMS key Policy : 
	- Created if you don't provide KMS key policy
	- entire AWS account can have access to the key 
- Custom KMS key Policy: 
	- define users, roles who can access the KMS keys
	- useful for cross account access of KMS keys

Copying Snapshots across accounts: 
- create snapshot and encrypt it with own KMS key (custom KMS)
- attach KMS policy to authorize cross account access
- share encrypted snapshot
- create a copy of snapshot, encrypt it with CMK in your account 
- create volume from that snapshot

---
### KMS Multi Region Keys

![[Pasted image 20240926105812.png|400]]

- identical KMS keys in different AWS regions 
- multi region keys have same key ID, automatic rotation

- encrypt in one region and decrypt in other regions
- by doing this we are eliminating the need for re-encrypting and making cross region API calls 

- each multi region key is managed independently 
- KMS MRK are not global 

**DynamoDB Global Table and KMS - MRK Client side encryption**

- can encrypt specific attributes at client side in dynamoDB 
- combined with global tables, the data is replicated to another region
- after replication is done the client in another region can make low latency API calls to KMS in their region to decrypt data at client side 

![[Pasted image 20240926110700.png|300]]

---
### S3 Replication with encryption 

- unencrypted and encrypted using SSE - S3 are replicated by default
- objects encrypted using SSE - C can be replicated

- For objects encrypted using KMS - you need to enable the option
	- specify KMS key you want to use to encrypt the objects in target
	- IAM role with kms: to decrypt the obj in source and re-encrypt the data in target bucket 
	- too much decryption and encryption : KMS throttling errors: ask for quota increase

--- 
### AMI Sharing Process Encrypted via KMS

![[Pasted image 20240926112822.png|200]]

- modify launch permissions : enable sharing AMI with another AWS account 
- share the KMS key used to encrypt the AMI at source
- IAM role/user in the target must have permissions to describekey, ReEncrypted, CreateGrant, Decrypt
- launch ec2 instances from the AMI 

---
### SSM Parameter Store 

- secure storage for configurations and secrets
- seamless encryption using KMS
- serverless, scalable, durable 
- version tracking if you change your configurations
- security through IAM 

![[Pasted image 20240926143353.png|200]]

**Parameter store hierarchy** 

- /mydept/
	- my-app/
		- dev/
			- db-url
			- dbpassword
		- prod/
			- db-url
			- dbpassword
	- other-app/
- otherdept/

![[Pasted image 20240926143709.png|400]]

**parameter policy**
- allow to assign a TTL to a parameter
- force update, delete sensitive data 
- can assign multiple policies at a time 

![[Pasted image 20240926143943.png|700]]

---
### AWS Secrets Manager

 - newer service, meant for storing secrets
 - forces rotation of secrets every X days 
 - automated generation of secrets on rotation (using Lambda)
 - integration with <mark style="background: #BBFABBA6;">amazon rds</mark> (mysql, postgreSQL, aurora)

**Multi Region Secrets** 
- replicate secrets across multiple aws regions
- secrets manger keep read replicas in sync with the primary secret
- use case: multi region apps, disaster recovery strategies etc 

![[Pasted image 20240926145840.png|400]]

---
### AWS Certification Manager (ACM)

- provide, manage and deploy TLS certificates
- provides inflight encryption for websites
- supports public and private TLS certificates
- public is free
- automatic TLS certification renewal 
- integrates with 
	- ELB
	- CloudFront Distrubutions
	- API's 
- cannot use ACM with EC2 

==INCOMPLETE==

--- 

### AWS WAF - Web Application Firewall 

- protects web application from common web exploits (layer 7)
- layer 7 is HTTP 

- deployed on 
	- ALB
	- API gateway 
	- CloudFront
	- AppSync GraphQL API 
	- Congnito User Pool 

- define web ACL Rules: 
	- filter based on IP addresses: IP Set: up to 10,000 IP addresses can be restricted 
	- Search in HTTP headers, HTTP body, protects from common attacks such as SQL injections 
	- geo-match (block countries)
	- rate based rules - no of requests from an IP - prevents DDoS

- web ACL are regional except cloudFront


![[Pasted image 20240926172413.png|400]]

---
### AWS Shield 

- protects from DDoS attacks 

- AWS Shield Standard: 
	- free service activated on all AWS customers
	- Provides protection from attacks such as SYN/UDP floods, and other layer 3/4 attacks 

- AWS Shield Advanced: 
	- optional DDoS mitigation ($3000 per month)
	- protection against applications running Amazon Ec2, ELB, CloudFront, Global Accelerator and Route 53
	- 24/7 access to AWS DDoS Response Team (DRP)

---
### AWS Firewall Manager 

- manages all firewall rules in all accounts in AWS organization 
- set security policy : common set of security rules
	- WAF rules
	- AWS Shield 
	- Security Groups
	- AWS Network Firewall 

- firewall manager allows you to manage all your firewalls at once place

- rules are applied to new resources as they are created

![[Pasted image 20240926223404.png]]

---
### Amazon Guard Duty 

- intelligent threat discovery 
- uses ML algorithms, anomaly detection, 3rd party data
- can set up eventbridge rule to be notified in case of findings
- eventbridge can send data to SNS or AWS lambda
- can protect against cryptocurrency targets

input data includes:
- VPC flow logs
- Cloudtrail logs
- DNS Logs

![[Pasted image 20240926224157.png|400]]

---
### Amazon Inspector 

- automated security assessments

- ec2 instances
	- analyze against unintended network accessibility
	- analyze against running OS against known vulnerabilities
- for container images push to Amazon ECR
- for lambda functions 
	- assessments are done as they are deployed
	- identify software vulnerabilities 
- can report to AWS security hub 
- send findings to amazon events bridge


Note: only for ec2, ecr and lambda functions 
package vulnerabilities (ec2, ecr and lambda)
network reacability - ec2

---
### Amazon Macie

- find personal identifiable information (PII) and alerts you 
- uses ML and pattern matching to discover sensitive data 

![[Pasted image 20240926224901.png|400]]

---

Date : 26/09/2024
Vivek Malapaka

---
