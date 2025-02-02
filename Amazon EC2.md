- - - 
### **EC2 - Elastic Compute Cloud**

- Infrastructure as a service

- Capable of 
	- Renting virtual machines (`EC2`)
	- Storing data on virtual drive (`EBS`)
	- Distributing data (`ELB`)
	- Scaling services using (`ASG`)

**EC2 Sizing and configurations options**

- can choose OS : `linux, windows, macOS`
- can choose compute power & cores (CPU)
- can choose RAM
- storage space
	- network attached (`EBS & EFS`)
	- hardware (`EC2 Instance Store`)
- Firewall rules - security group
- Bootstrap Script : EC2 user data
	- bootstrapping : launching commands when machine starts
	- runs only once and the instance first start 
		- installing updates
		- install software 
		- download common files from the internet

**Note**
- if you stop and instance and start it again, the `public IPv4` changes.
- the `private IPv4` remains the same 

--- 

### **EC2 Instance Types**

Example : `m5.2xlarge`
- `m` : instance class
- `5 `: generation
- `2xlarge` : size within the instance class

##### **General Purpose**
- great for diversity of workloads
- Balance between 
	- Compute
	- Memory
	- Network
- example : `t2.micro`

##### **Compute Optimized**
- great for compute-intensive tasks 
	- batch processing
	- media 
	- high performance computing
	- machine learning 
	- gaming servers

##### **Memory Optimized**
- Fast performance, process large data sets 
	- high performance relational/non relational databases
	- in memory databases for BI
	- applications performing processing of unstructured data

---

### **Security Groups**

- fundamentals of network security 
- control traffic in and out of EC2 instances 

![[Pasted image 20240808143909.png|300]]
- control of inbound - from www to instance
- control of outbound - from instance to www
- can also authorize IPv4 and IPv6 

![[Pasted image 20240808144511.png|500]]

- Can be attached to multiple instances and vice versa 
- locked down to a particular region 
- By default, all inbound traffic is `blocked` and all outbound traffic is `authorised`

![[Pasted image 20240808145019.png|500]]

**Classic Ports to know** 
	`22 = SSH (Secure Shell)` - log into a Linux instance
	`21 = FTP (File Transfer Protocol)` - upload files into a file share
	`22 = SFTP (Secure File Transfer Protocol)` - upload files using SSH
	`80 = HTTP` access unsecured ' websites
	`443 = HTTPS` access secured websites
	`3389 = RDP (Remote Desktop Protocol)` - log into a Windows instance

--- 
### **EC2 Instance Purchase Options**

- **On-Demand Instances**
	- short workload, predictable pricing, pay per use
	- highest cost but no upfront payment 
	- no long term commitment 
	- billing per second - linux or windows 
	- billing per hour - other OS

- **Reserved (1 & 3 years)**
	- reserve a specific instance attributes (Type, Region, OS)
	- Period :
		- 1 year(+discount) 
		- 3 year(+++discount)
	- Payment Options: 
		- No upfront (+)
		- partial upfront (++)
		- fully upfront (+++)
	- Reversed Instances  - long workloads
	- Convertible Reserved Instances  - long workloads with flexible instances (--)

- **Savings Plan (1 & 3 years)**
	- Commitment to an amount of usage, long workload
	- Commit to type of usage ($10/hour for 1 or 3 years)
	- Usage beyond EC2 plan will be billed on on-demand price
	- locked to specific instance family and AWS region

- **Spot Instances** 
	- short workloads, cheap, less reliable 
	- 90% discount compared to on-demand
	- use case - anything which is resilient to failure 

- **Dedicated Hosts** - book an entire physical server

- **Dedicated Instances** - no other customers will share your hardware

- **Capacity Reservations** - reserve capacity in specific AZ for any duration

![[Pasted image 20240808160657.png|500]]

--- 
### **EC2 Spot Instance Requests**

- heavy discounts  - upto 90% compared to on-demand 

- define `max spot price` and we get to keep the instance until `max spot prince > current spot price`

- if `current spot price` exceeds `max spot price`
	- stop the instance
	- terminate the instance 


- How to terminate a spot instance ?? ==(IMPORTANT)==
![[Pasted image 20240808161533.png|500]]

- Cancelling a Spot Request does not terminate instances 
- You must first cancel a Spot Request, and then terminate the associated Spot Instances 
- Cancelling the spot instances first also doesn't terminate all the instance because the spot request is still active. 

- **Spot Fleet** = Spot Fleet is a set of Spot Instances and optionally On-demand Instances. It allows you to automatically request Spot Instances with the lowest price.

---

Date : 08/08/2024
Vivek Malapaka

---

