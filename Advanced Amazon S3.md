- - -
### S3 Lifecycle Rules

- for infrequently accessed objects move them to standard IA
- for achieve objects, don't need fast access to objects move them to glacier or glacier deep archive

- moving is done manually but it can be automated using lifecycle rules. 

- **Lifecycle Actions**
	- Transition Action - configure objects to transition from one storage class to another
		- eg: move objects to standard IA after 60 days from creation
		- eg: move to glacier for archiving after 6 months

	- Expiration actions - configure objects to (delete) after some time 
		- can be used to delete older version of files
		- delete incomplete multi part uploads
		- access logs can be deleted 

- Rules can be created for a certain prefix
- or can be create for objects with particular tags

--- 
### Requester Pays

- Generally, the owner pays for the bucket cost and the data transfer costs associated with the bucket

- With requester pays, the owner just has to pay for the bucket cost, the networking cost is paid by the user who's requesting for the files in the bucket

- helpful while sharing large datasets 

![[Pasted image 20240817185614.png|300]]

---
### S3 Event Notification 

events can be: 
- objectcreation
- objectremoved
- objectrestore
- replication 

events notifications sends events to different AWS services such as
- SNS 
- SQS
- Lambda functions 

these services must have IAM permissions attached to receive the notifications from s3 bucket 

![[Pasted image 20240817190332.png|500]]

![[Pasted image 20240817190353.png|400]]

---
### S3 Performance

- **Multi Part Upload**
	- Recommended for files > 100MB
	- must use for files > 5GB

![[Pasted image 20240817191256.png|200]]

- **S3 Transfer Acceleration** 
	- send the file to an edge location using public www 
	- send the file from edge to target location using private aws network (fast)

![[Pasted image 20240817191530.png|300]]

- **S3 Byte Range Fetch**
	- parallelize GET's by requesting specific byte ranges
	- can be used to speed up downloads
	- can be used to retrieve only partial data (first 50 bytes)

![[Pasted image 20240817191811.png|400]]

---
### S3 Select 

- retrieve data by using SQL at server side
- high speed, less cost

![[Pasted image 20240817192047.png|300]]

![[Pasted image 20240817192107.png|300]]

---
### S3 Batch Operations

- perform bulk operations on s3 objects with a single request
	- encrypt all unencrypted objects
	- restore objects from s3 glacier
	- copy objects between s3 buckets

- Job - list of objects + actions to perform + other parameters 

![[Pasted image 20240817192749.png|300]]

---

Date: 17/08/2024
Vivek Malapaka

---
