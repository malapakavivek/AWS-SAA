- - - 
### **Private vs Public IP (IPv4)**

- two sorts of IPs - `IPv4` & `IPv6`
	- `IPv4` - 1.160.10.240
	- `IPv6` - 2001:db8:3333:4444:5555:6666:7777:8888

- format of `IPv4` - [0-255].[0-255].[0-255].[0-255]
- allowing 3.7 billion different addresses in public space

![[Pasted image 20240808171427.png|500]]

- two machines can't have the same public `IPv4`
- But, two machines on different private networks can have same private `IPv4`

**Elastic IP** - IP that you own as long as you don't delete it. 

- when you stop and start an EC2 instance, it can change the public IP
- if you need a fixed public IP for instance, we use `Elastic IP`
- can be attached to only one instance 

---
### **Placement Groups**

- **Placement Group Cluster** 

	- Pros: Great Network (Low Latency)
	- Cons: if AZ fails, all instances fail
	- Use Case: 
		- Big Data job which needs to be finished quick
		- applications which need extreme low latency

	 ![[Pasted image 20240808175531.png|300]] 

- **Placement Group Spread**

	- Pros: 
		- Can be spread across multiple AZ's
		- Reduce risk of simultaneous failure
		- EC2 instance are on different physical hardware
	- Cons:
		- limited to 7 instances per AZ per placement group
	- Use Case: 
		- Applications which need high availability 

	![[Pasted image 20240808180353.png|400]]

- **Placement Group Partition**

	- up to 7 partition per AZ
	- a partition failure might affect EC2 instances but won't affect other partitions
	- Use Case: HDFS, HBase, Casandra 

	![[Pasted image 20240808181127.png|400]]

--- 

### **Elastic Network Interfaces (ENI)**

- ENI gives EC2 instances access to the internet 
- ENI contains 
	- primary `IPv4`, one or more secondary `IPv4`
	- one elastic IP per private `IPv4`
	- one or more security groups 
	- a MAC address
- can create independent ENI and attach them to EC2 instances for failover 
- Bound to one specific AZ

![[Pasted image 20240808182122.png|300]]

---

### **EC2 Hibernate** 

- EC2 instance is pushed to hibernate mode
- in memory RAM is preserved 
- instance boot is much faster because the OS is not stopped
- behind the scene : RAM is written to a file in EBS 

![[Pasted image 20240808182730.png|300]]\

**Note**: 
- Instance can NOT be hibernated for more than 60 days.
- the root EBS volume must be encrypted
- Make sure that the root volume has enough storage to store the RAM of the EC2 instance
- available on on demand, reserved and spot instances 
---

Date : 08/08/2024
Vivek Malapaka

---
