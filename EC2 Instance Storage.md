- - - 
### **EBS - Elastic Block Storage** 

- `EBS Volume` is a network drive, attached to instance while running 
- allows instance to persist data even after termination
- can be attached to only instance at a time
- bound to specific AZ

- to move a EBS volume across AZ, you need to snapshot it 
- can have customized capacity

- When EC2 instance is terminated 
	- by default, the root EBS volume is deleted 
	- any other attached EBS volume is not deleted

![[Pasted image 20240809154842.png|400]]

- can be attached on demand 
- one instance can have multiple EBS attached to it.

---
### **EBS Snapshots**

- Snapshots are backups of EBS volume
- we can snapshot our EBS volume at any point of time without detaching the volume (but recommended)
- We cannot share EBS across AZ's but we can copy our snapshot into another EBS in different location

![[Pasted image 20240809155758.png|400]]

**EBS Snapshot Features**
- Snapshot Archive
	- Move to "archive tire" - 75% cheaper
	- takes 24 to 72 hrs to restore

- Recycle Bin
	- retains deleted snapshots so we can recover after an accidental deletion 
	- retention - 1 day to 1 year

- Fast snapshot restore
	- restore data super fast from the snapshot (expensive)

---
### **AMI - Amazon Machine Image**

- AMI are customization for EC2 instances 
	- add own software, config, OS, monitoring
	- faster boot time 

- Can launch EC2 instances from: 
	- A public AMI : provided by AWS
	- Your own AMI
	- AMI Marketplace - AMI sold by someone else

- Building AMI 
	- Start EC2 instance and customize it 
	- Stop the Instance 
	- Build AMI - this will also create EBS snapshot
	- Launch instance at another location using this AMI 

![[Pasted image 20240809162249.png|400]]

---
### **EC2 Instance Store**

- high-performance hardware disk
- are actually physically connected to a serve
	- better I/O performance 
	- high throughput
- EC2 instance store lost their storage if they're stopped
- Use Case: 
	- temp data, buffer, cache

---
### **EBS Volume Type**

- EBS Volume comes in 6 types

| Name    | Type | Cost  | Purpose                                   |
| :------ | ---- | ----- | ----------------------------------------- |
| gp2/gp3 | SDD  | $(+)  | Variety of workloads                      |
| io1/io2 | SDD  | $(++) | high throughput, low latency              |
| st1     | HDD  | $(-)  | frequently accessed, throughput intensive |
| sc1     | HDD  | $(--) | less frequently accessed                  |
-  only `gp2/gp3` or `io1/io2` can be used as root volume
- too many numbers for comparisons - check video for ref :  [Link](https://www.udemy.com/course/aws-certified-solutions-architect-associate-saa-c03/learn/lecture/26098296#content)

**EBS Multi Attach - only for `io1/io2` family**
- Attach same EBS volume to multiple EC2 in same AZ
- Each instance has full read and write permissions to the volume
- can be attached up to only `16 EC2` instances at a time

![[Pasted image 20240809170424.png|300]]

---
### **EBS Encryption**

- When you encrypt EBS volume, the following happens:
	- Data at rest is encrypted inside the volume
	- All data in flight is encrypted
	- all snapshots are encrypted
	- all volumes created from snapshots are encrypted

Encrypt an unencrypted EBS volume: 
- Create EBS snapshot
- Encrypt the snapshot (using copy)
- Create new EBS volume from snapshot
- attach the volume to instance. 

---

### **Amazon EFS - Elastic File System**

- Managed NFS, can be mounted to many EC2
- EFS works with EC2 instances in multi - AZ
- highly scalable, super expensive, pay per use

![[Pasted image 20240809171642.png|400]]

- Use Case : data sharing, content management
- uses security group to control access to EFS
- **Only Compatible with `Linux AMI` 

---
### **Difference Between EBS and EFS**

###### **EBS Volume**
- one instance (except multi attach `io1/io2`)
- locked at an AZ level
- `gp2`: IO increase if disk size increase
- `gp3` & `io1` : Can increase IO independently

- To migrate EBS across AZ
	- Take snapshot
	- restore snapshot in different AZ
	- create volume out of snapshot
	- attach it to instance 

- Root EBS Volumes of instances get terminated by default if the EC2 instance gets terminated. (you can disable that)
###### **EFS Volume**
- can mount to 100s of instances across AZ
- only instances which run on linux AMI 
- expensive than EBS

--- 

Date: 09/08/2024
Vivek Malapaka

---
