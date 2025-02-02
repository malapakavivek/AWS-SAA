- - - 

### Introduction 

- Disaster recovery is about preparing for and recovering from a disaster
- what kind of disaster recovery?
	- On premise --> on premise
	- on premise --> cloud
	- cloud region A ---> cloud region B 


- RPO - recovery point objective
- RTO - recovery time objective 

![[Pasted image 20240930130116.png|400]]

**Strategies** 
- Backup and restore
- Pilot Light
- Warm Standby
- Hot Site/ Multi Site Approach 

**Backup and restore** (High RPO)

- very easy, pretty expensive, high RPO and RTO

![[Pasted image 20240930170112.png|400]]

**Pilot Light** 

- small version of app is always running in the cloud 
- similar to backup and restore 
- faster than backup and restore as systems are already up
- lower RTO and lower RPO

![[Pasted image 20240930170451.png|400]]

- only for critical core assistance 

**Warm Standby** 

- full system up and running, but at a minimum size 
- upon disaster, we can scale it 

![[Pasted image 20240930170728.png|400]]

**Hot Site/ Multi Site Approach**

- very expensive 
- very low RTO and RPO
- full production scale is running on aws and on premise 

![[Pasted image 20240930170956.png|400]]


---
### Database Migration Service (DMS)

- quickly and securely migrate database to AWS
- the source database remains available during migration 
- supports: 
	- homogeneous - Oracle to Oracle
	- heterogeneous - Microsoft SQL to aurora
- must create ec2 instance to perform replication task 

![[Pasted image 20240930173400.png|150]]

**AWS Schema Conversion Tool

- convert database schema from one engine to another
- you do not need SCT if you are migrating the same DB engine 
	- on premise postgres --> RDS postgres 

![[Pasted image 20240930173809.png|400]]

**DMS Continuous Replication** 
![[Pasted image 20240930174011.png|500]]

---
### RDS and Aurora Migration

**RDS MySQL to Aurora MySQL**

- RDS MySQL to Aurora MySQL
	- DB snapshot from RDS MySQL to Aurora MySQL
	- create aurora read replica from RDS and when replication lag is 0, then promote aurora as own database cluster 

![[Pasted image 20240930175049.png|200]]

- External MySQL to Aurora MySQL
	- use percona XtraBackup to create file backup in s3 after that create an aurora mySQL DB from s3
	- create an aurora mySQL DB and Use the mysqldump utility to migrate MySQL into Aurora (slower than S3 method)

![[Pasted image 20240930175208.png|200]]


**RDS Postgres to Aurora Postgres** 

- same as above 

--- 
### On Premise strategy with AWS 

- ability to download Amazon Linux 2 AMI as a VM 
- VM import/export 
	- migrate existing applications into ec2
	- export VM from ec2 to on premise 
- AWS DMS 
	- on premise -> AWS 
	- AWS -> AWS
	- AWS -> on premise 
- AWS server migration service (SMS) 
	- replication of on premise live servers to AWS 

--- 
### AWS Backup 

- fully managed service
- manage and automate backups across AWS service 
- supports cross regions backups 
- supports cross accounts backups 

- supports PITR for supported services 
- on demand and scheduled backups
- tag based backup policies 

- you create backup plan 
	- backup frequency 
	- backup window
	- transition to cold storage
	- retention period 

![[Pasted image 20240930182624.png|400]]

---
### Application Migration Service (AMS)

- lift and shift - migrating applications from on premise to AWS
- minimal downtime, reduce costs

![[Pasted image 20240930184645.png|500]]

---
### Transferring large data into AWS

if you have to transfer 200 TB of data in cloud and 100Mbps internet speed 

- Over the internet/ Site-to-Site VPN
	- immediate to setup
	- takes 185 days

 - Over Private network (direct connect) 1GBps
	 - long for one time setup (over a month)
	 - 18.5 days

- Over snowball
	- takes 2 to 3 snowballs in parallel 
	- takes 1 week 

---
