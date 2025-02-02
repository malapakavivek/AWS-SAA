- - -

### CIDR, Private vs Public IP

- CIDR consists of two components
	- Base IP 
		- xx.xx.xx.xx
		- example: 10.0.0.0, 192.168.0.0
	- Subnet Mask 
		- defines how many bits can change in the IP
		- /0, /24, /32
		- can take two forms:
			- /8 - 255.0.0.0
			- /16 - 255.255.0.0
			- /24 - 255.255.255.0
			- /32 - 255.255.255.255

![[Pasted image 20240927100904.png|200]]

Private IP allows only certain values
- 10.0.0.0 - 10.255.255.255 (10.0.0.0/8) - in big network 
- 172.16.0.0 - 172.31.255.255 (172.16.0.0/12) - AWS default VPC in range


all the rest of IP addresses are public IPv4

---
### VPC Overview

- all new aws accounts have default VPC
- when a new ec2 instance is launched it is launched in the default VPC if not subnet is specified

VPC - Virtual Private Cloud
- can have multiple VPC's in an AWS region (max: 5)
- Max CIDR per VPC is 5, and for each CIDR:
	- Min size is /28 (16 IP addresses)
	- max size is /16 (32 IP addresses)

- only private IPv4 ranges are allowed
- VPC CIDR should not overlap with other networks (eg: corporate)

---
### VPC Subnet (IPv4)
- AWS reserves 5 IP addresses in each subnet 
- these 5 are not available for use 
- 10.0.0.0/24 is the cider block 
	- 10.0.0.0, 10.0.0.1, 10.0.0.2, 10.0.0.3 and 10.0.0.255 are not available 
	- basically the first 4 and the last 1 

![[Pasted image 20240927103848.png|400]]
**2 ^ (32 - CIDR Range suffix)**  - 5 = the number of IP address available to use 

---

### Internet Gateway and Route Tables 

- allows resources in a VPC to connect to the internet 
- must be created separately from VPC
- one VPC can be only attached to one IGW

- IGW on their own do not allow internet access
- route tables must also be edited 

--- 
### Bastion Hosts 

- use bastion hosts to ssh into private ec2 instances
- bastion host in in the public subnet and is connected to the the private subnet 
- security group of ec2 instances must allow the security group of the bastion host tot connect to it. 

![[Pasted image 20240927113704.png|200]]

---
### NAT instances  (outdated)

- NAT = Network Address Translation 
- allows ec2 instances in private subnets to connect to the internet
- NAT must be launched in a public subnet 
- NAT must be associated with an elastic IP
- Route tables must be configured in such a way that it sends traffic from private subnets to NAT instance

![[Pasted image 20240927145156.png|300]]

---
### NAT Gateway 

- managed by AWS, higher bandwidth, high available and no administration 
- created in specific AZ and used elastic IP 
- Requires internet gateway 
- Private subnet ---> NATGW ---> IGW
- bandwidth is 5Gbps with automatic scaling up to 100Gbps
- no need to manage any security groups 

- must create multiple NAT Gateways in multiple AZ's for fault tolerance 

![[Pasted image 20240927151035.png|500]]

![[Pasted image 20240927151056.png|500]]


---

### NACL and security groups 

**Stateless vs Stateful**

- Stateful security groups allow return traffic automatically, simplifying rule management.
- Stateless network ACLs (NACL) require explicit rules for both inbound and outbound traffic.

![[Pasted image 20240927191414.png]]

**NACL**
- firewall which controls traffic to and from subnets
- NACL per subnet, new subnets are assigned with default NACL
- Rules have numbers - lower the number higher the preference 
- last rule is * and denies everything from every IPv4

- newly defined NACLs will deny everything - *

- Default NACL will allow everything inbound and outbound with subnets it's associated with 

![[Pasted image 20240927192214.png|400]]

**Ephemeral Ports** 

- clients connect on a defined port, expects response from ephemeral port
- defined ports - 80 for HTTP, 22 for SSH, 443 for HTTPS 
- ephemeral ports - different port ranges depends on OS. works only till the connection is lived 

![[Pasted image 20240927192959.png|500]]


 ![[Pasted image 20240927193235.png]]

---
### VPC Peering 

- connect two private VPC, to make them behave as if they were in the same network 
- VPC's Must NOT have overlapping CIDRs
- NOT transitive eg: A-->B, B--->C =/ A--->C 
- You must update route tables in each VPC’s subnets to ensure EC2 instances can communicate with each other

![[Pasted image 20240927195455.png|200]]

can create VPC peering across different aws accounts/ regions 

---

### VPC Endpoints

- connect to AWS services using a private network instead of using the public network 
- they scale horizontally 
- they remove the need of NATGW ---> IGW ---> connect to internet

![[Pasted image 20240927223722.png|300]]

**Types of Endpoints** 

- Interface endpoints
	- provides an ENI (private IP address) as an entry point
	- supports most AWS services
	- $ per hour + $ per GB of data processed

![[Pasted image 20240927224240.png|300]]

- Gateway Endpoints 
	- free
	- supports only S3 and DynamoDB
	- need not attach security group, must only change in the route table

![[Pasted image 20240927224330.png|300]]

---
### VPC Flow Logs

- captures info about all IP traffic going into interfaces
	- VPC level
	- Subnet level
	- ENI level
- helps to troubleshoot connectivity issues
- flow logs can be sent to s3, cloudwatch logs, kinesis data firehose

- Query VPC flows using athena on s3 or cloudwatch logs insights 

![[Pasted image 20240927232420.png|500]]

---
### Site to Site VPN 

- connecting AWS to corporate data center located outside of aws
- you need two things 
	- Virtual Private Gateway (VGW)
		- at the AWS Side
		- connected to the VPC from which you want to create a S2S VPN connection 
	-  Customer Gateway (CGW)
		- software application or physical device on customer side of VPN connection 

![[Pasted image 20240928001010.png|200]]


provides secure connection between multiple sites if you have a VPN connection 
- the customer networks can communicate with each other
- VPN connection, so it goes over the public internet but the VPN connection is encrypted 

![[Pasted image 20240928001236.png|300]]


--- 
### Direct Connect and Direct Connect Gateway

==INCOMPLETE==




----
### Transit Gateway

- Transitive peering between multiple VPCs / on premise hubs
- regional resource, works cross region 
- can peer transit gateways across regions 
- can limit which VPC can talk to other VPC
- works with VPN and Direct connect gateways to connect with on premise hubs
- Supports MultiCast IP (only service which supports) - see multicast - answer is transit gateway

![[Pasted image 20240928010636.png|200]]


**Transit Gateway - Site to Site ECMP**

- ECMP - Equal cost multi path routing
- routing strategy to allow to forward a packet over multiple best path
- increased bandwidth of your aws connection

![[Pasted image 20240928011112.png|300]]

difference of connection (using VPN to connect to VPC vs transit gateway)

![[Pasted image 20240928011243.png|500]]

---
### VPC Traffic Mirroring

- allows to capture and inspect network traffic in VPC
- how? route the traffic to the security appliance that you manage
- Capture the traffic 
	- From - ENIs
	- To - ENIs or NLB
- can capture all traffic or can filter traffic
- source and target should be in same VPC or can be in different if VPC peering is enabled 

Use cases: content inspection, threat monitoring, troubleshooting, …

![[Pasted image 20240928012118.png|200]]

---
### IPv6 for VPC

- IPv4 - 4.3 billion addresses (will be exhausted very soon)
- Ipv6 is successor of IPv4
- every IPv6 in aws is public 

- IPv4 cannot be disabled for your VPC and subnets
- EC2 instances can connect to the network via IPv4 and IPv6 through internet gateway

---
### Egress-only internet gateway

- used for IPv6
- Similar to NAT Gateway but for IPv6
- allows instances in VPC to connect to internet and not vice versa 

![[Pasted image 20240928110312.png|250]]

![[Pasted image 20240928110611.png|600]]

---

Date: 28/09/24
Vivek Malapaka

---
