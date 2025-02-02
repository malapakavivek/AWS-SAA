- - - 

### AWS Organizations

- Global service
- manages multiple AWS accounts
- main account is management account 
- others are member accounts
- members can be in one org only
- consolidated billing across all accounts
- heavy discounts
- very easy to create accounts

![[Pasted image 20240924213412.png|500]]

advantages
- enable cloudtrail on all accounts, send logs to central s3 account
- send cloudwatch logs to central logging account 
- centralized billing 
- security
	- service control policy (SCP) 
		- applied to OU or accounts to restrict users 
		- they do not apply to the management account

![[Pasted image 20240924214239.png|600]]

---

### IAM Conditions 

- aws:SourceIp - allow only a range of ip addresses (private company) to the resources and deny all other ip addresses making the api call

- aws:RequestedRegion - restrict the region making the api calls/ deny resources to the specific region

- ec2:ResourceTag - restrict access based on tags

- aws:MultiFactorAithPresent - can do anything on ec2 but can only stop or terminate instances if they have multifactor authentication allowed

---
### IAM Roles vs Resource based policy 

- <mark style="background: #BBFABBA6;">IAM role</mark> - when the user assumes an IAM role, they lose their original permissions and take the permissions of the role 

- <mark style="background: #BBFABBA6;">Resource based policy</mark> - the policy is attached to resource, the user need to give up their original policies 

- resource based policy are supported by lambda, SQS, SNS, S3
- IAM roles must be given to the user when using kinesis streams, ECS taks

---

### IAM Policy Evaluation 

**Permission Boundaries

- set for users and roles (not groups)
- sets max permissions an IAM entity can get 

![[Pasted image 20240925215508.png|400]]


 ![[Pasted image 20240925220109.png|400]]

answers
1. NO coz there's a deny on SQS
2. there's a conflict but still it a NO coz it has a explicit deny
3. nothing is mentioned so it's a NO 

---
### AWS IAM Identity Center 

- one login into 
	- aws accounts in an org
	- SAML 2.0 enabled applications
	- ec2 windows instances 

Identity Center: 
- where you store all your users 
- can store in IAM identity center 
- or 3rd party: active directories 

if you have multiple AWS account - use IAM identity center for a single sign in 

![[Pasted image 20240925223300.png|500]]

![[Pasted image 20240925223529.png|500]]

**Fine Grained Permissions and Assignments**
???

---

### AWS Control Tower

- set up and govern a secure and compliant multi account AWS environment 
- Control tower uses aws org to create accounts

Benefits:
- Automate the set up of environment 
- detect policy violations 
- monitor compliance through dashboard
- automate policy management through guardrails

**Guardrails** 

- Preventive  - uses SCP to restrict all accounts to perform an action
- Detective - uses config to check for eg: untagged resources 

![[Pasted image 20240925224323.png|500]]


<mark style="background: #BBFABBA6;">See Directory Service during revision</mark>

---

Data : 25/09/24
Vivek Malapaka

---
