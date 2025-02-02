- - - 
### **RDS - Relational Database Service**

- managed DB service for databases which uses SQL as a language
- allows to create DB in the cloud, managed by AWS

Advantages of using RDS over deploying DB on EC2 instance 
- RDS is a managed service
	- automated, OS updates
	- continuous backups 
	- dashboards
	- multi AZ setup
	- read replicas
	- scaling capability
	- storage is backed by EBS

RDS - Storage Auto Scaling
- RDS detects running out of free storage and it scales automatically 
- set `maximum storage threshold` 
- useful for applications with unpredictable workloads

---
### **Read Replicas vs Multi AZ**

###### Read Replicas
- can create up-to 15 read replicas
- within AZ, cross AZ, cross region
- ASYNC - reads are eventually consistent (?)
- replicas can be promoted to their own DB

![[Pasted image 20240813111907.png|400]]

- create a read replica of the production database 
- and run the reporting application on top of it 
- the main DB is unaffected
- only SELECT statements run on read replicas, no (INSERT, UPDATE, DELETE)

![[Pasted image 20240813112110.png|300]]

- cost for read replicas
	- same region/different AZ's  - free
	- different regions - $(++)

###### RDS Multi AZ (Disaster Recovery)
- SYNC replication
- cannot read/write to standby db instance
- whatever changes are done in main DB is reflected in standby DB
- one DNS name - automatic failover to standby
- increased availability
- not used for scaling

![[Pasted image 20240813114003.png|300]]

RDS - from single AZ to multi AZ (behind the scene)
![[Pasted image 20240813114259.png|300]]

RSD Custom: 
- can get access to underlying database and OS to customize 
- only available with Oracle and Microsoft SQL server DB
- De-activate automation mode before performing customization, better to take a snapshot to DB 

---

### **Amazon Aurora**

- not open sourced
- postgres and MySQl are both supported as Aurora DB
- 5x performance improvement over MySQL on RDS
- 3x performance improvement over Postgres or RDS
- automatically grows in increments of 10GBS, upto 128TB
- can have up-to 15 Read Replicas, replication process is much faster compared to RDS
- failover is instantaneous
- expensive than RDS

**Aurora High Availability and Read Scaling** 

- 6 copies of your data across 3 AZ's
	- replicated
	- self healing 
	- auto expanding
- one aurora instance takes write (master)
- automated failover for master under 15 seconds
- master + upto 15 Read Replicas

![[Pasted image 20240813123912.png|300]]

**Aurora DB Cluster**

![[Pasted image 20240813124211.png|400]]

- if you autoscale, your reader endpoint will be extended to the new read replicas and the CUP usage of your aurora instances will be reduced because the traffic is distributed. 

---
### **Aurora - Advance Concepts**

**Aurora - custom endpoint

- define subset of aurora instances as custom endpoint
	- eg: run analytics on the custom endpoints
- the reader endpoint is not used after created sub custom endpoints ie. we setup many different endpoints for different kind of workloads 

![[Pasted image 20240813125257.png|500]]

**Global Aurora**

- Aurora Cross Region Read Replicas: 
	- simple for disaster recovery
- Aurora Global Database
	- 1 primary region 
	- upto 5 secondary regions (read-only), where lag is < 1 second
	- upto 16 read replicas per secondary region
	- failover is done in <mark style="background: #BBFABBA6;">less than 1 minute</mark>

**Aurora Machine Learning**
- ML based predictions to your applications via SQL 

![[Pasted image 20240813125940.png|200]]

---
### **RDS and Aurora - Backups**

**RDS Backup**

- Automated Backups
	- Daily Backup of the database done during the backup window
	- logs are backup by RDS every 5 mins 
	- you can restore the data from the transactional logs (from oldest to 5 mins ago)
	- 1 to 35 days of retention, 0 to disable automated backups
- Manual DB Snapshots
	- Manually triggered by user
	- retention of backups for as long as the user wants.

- if you stop RDS, you still have to pay for the storage, if you plan to stop the RDS for a long time, snapshot the DB and kill the RDS 
- can recover and restore from the snapshot later in future 
- advantage is it costs less 

**Aurora Backups**

- Automated Backups
	- 1 to 35 days, (cannot be disabled)
	- recover to any point in time 
- Manual DB Snapshots
	- Manually triggered by user
	- retention of backups for as long as the user wants

**Aurora Cloning**

- Faster than snapshot and restore 
- uses _copy-on-write_ protocol
	- initially, same data volume is allocated for both the DB clusters
	- when updates are made on prod aurora, storage is allocated and changes are copied to the new staging aurora

![[Pasted image 20240813131825.png|300]]

---
### RDS and Aurora Security

- At rest encryption 
	- database master and read replicas are encrypted if we check the encryption during the launch 
	- if master not encrypted, read replicas are not encrypted
	- to encrypt un-encrypted databases, DB Snapshot -> restore as encrypted

- In-flight encryption - TLS root certificate at client side
- IAM Authentication - IAM Roles to connect to database
- Audit Logs - what queries are made in RDS or aurora 
	- use cloudWatch Logs for longer retention 

---
### ElastiCache

- RDS -> Relational Database ; ElastiCache -> in memory cache databse
- eg: Redis, MemCached
- caches -> in memory database with high performance and low latency
- AWS managed service

**ElastiCache Architecture**

![[Pasted image 20240813133353.png|400]]

Redis
- ReadReplicas - High Availability
- Multi AZ - Auto Failover
- Backup and Restore Features
- Supports sets and sorted sets

Memcached
- No high availability 
- Non persistent 
- No backup
- Multi thread architecture

---

Data : 13/08/2024
Vivek Malapaka

---
