- - - 
### Introduction 

- use case:
	- used for backup and storage
	- disaster recovery
	- archive data
	- application hosting
	- media hosting 
	- data lakes and big data analytics 

- Amazon S3 allows people to store objects in buckets 
	- objects - "files"
	- buckets - "directories/folders"

- buckets name must be globally unique
- buckets are defined at regional level

- Objects (files) have a key (full path)
- key = <mark style="background: #BBFABBA6;">prefix</mark> + <mark style="background: #FFB86CA6;">object name</mark> 
	- s3://my-bucket/<mark style="background: #BBFABBA6;">myfolder1/anotherfolder2</mark>/<mark style="background: #FFB86CA6;">myfile.txt</mark>
- max. object size is 5TB, if more than 5GB, use multi part upload

---
### Amazon S3 - Security

- **User Based**
	- IAM Policies
- **Resource Based**
	- Bucket Policies
	- Object Access Control List (ACL)
	- Bucket Access Control List (ACL)

**Bucket Policies**
- JSON based policies
	- Resource - buckets and objects
	- Effect - Allow/Deny
	- Actions: set of API to allow or deny
	- Principal: user to apply the policy 


![[Pasted image 20240816092022.png|300]]

The above policy says all accounts <mark style="background: #BBFABBA6;">(Principal)</mark> have access to get all the objects <mark style="background: #BBFABBA6;">(Action)</mark> inside the examplebucket bucket. <mark style="background: #BBFABBA6;">(Resource)</mark>

Note: an IAM principal can access an s3 object if,
- user IAM Permission ALLOWS it or Resource Policy ALLOWS it
- AND no explicit deny

---
### Static Website Hosting

- s3 can host static websites and can have them accessible on the internet
- 403 error means your bucket is not public so we change that bucket policy

---
### Amazon S3 - Versioning 

- we can version our files in amazon s3
- enabled at bucket level
- if we upload another document of the same name, it will not replace the file, but will create another version of it. eg: 1,2,3

- it is a best practice to version your bucket
	- protection from unintended deletes
	- rollback to previous version

- suspending versioning (disabling it) does not delete previous version.

![[Pasted image 20240816093937.png|150]]

---
### Amazon S3 - Replication (CRR & SRR)

CRR - Cross Region Replication
SRR - Same Region Replication

- to perform replication, we must enable versioning in source and destination buckets. 
- buckets can be different AWS accounts
- copying is asynchronous 
- IAM permissions must be given to s3


after enabling replication, only new objects are replicated.
To replicate existing objects use s3 Batch Replication.

---
### S3 Storage Class

The types are
- S3 Standard - General Purpose
- S3 Standard - Infrequent Access
- S3 One Zone - Infrequent Access
- S3 Glacier Instant Retrieval
- S3 Glacier Flexible Retrieval 
- S3 Glacier Deep Archieve
- S3 Intelligent Tiering

Durability - Highly Durable (99.999999999%), same for all storage classes

Availability - measures how readily available a service is, depends on storage classes

###### S3 standard - general purpose
- 99.99% available
- used for freq accessed data
- low latency and high throughput 
- use case : big data analytics, mobile gaming, content distribution

###### S3 infrequent access
- less freq access but requires rapid access when needed
- lower cost than s3 standard

-  **S3 Standard - infrequent access**
	- 99.9% availability
	- use case: disaster recovery, backups
- **S3 one zone - infrequent access**
	- 99.5% available 
	- data is lost when AZ is destroyed
	- used for data which can be recreated

###### S3 Glacier Storage Classes
- low cost object storing 
- price for storage + price for retrieval = pricing 

- **Amazon S3 Glacier Instant Retrieval**
	- millisecond retrieval
	- minimum storage duration is 90 days
- **Amazon S3 Glacier Flexible Retrieval**
	- retrieval options- 
		- expedited (1 to 5 minutes)
		- standard (3 to 5 hours)
		- bulk (5 to 12 hours)
	- minimum storage days of 90 days
- **Amazon S3 Glacier Deep Archieve**
	- retrieval options 
		- Standard - 12 hours
		- Bulk - 48 hours
	- minimum storage duration of 180 days

---

Date: 16/08/2024
Vivek Malapaka

---
