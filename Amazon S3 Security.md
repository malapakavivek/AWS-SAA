- - - 
### S3 Encryption 

- Server side encryption (SSE)
	- SSE S3 - keys managed and owned by amazon - default
	- SSE KMS - key management service
	- SSE-C - we manage our own encryption keys

- Client Side Encryption

**SSE-S3**
- handled, managed and owned by AWS
- server side encryption
- AES-256
- enabled by default

![[Pasted image 20240820221527.png|400]]

**SSE - KMS**
- encryption keys managed by AWS KMS
- KMS adv : user control + log key usage in cloudtrail
- server side encrption
- when you want to use object, you need access to the object + the underlying kms key
![[Pasted image 20240820221557.png|400]]

**SSE-C**
- server side encryption
- S3 does not store encryption key that we provide
- HTTPS must be used
- key must be provided in HTTP header for every request

![[Pasted image 20240820221628.png|400]]

**Client Side Encryption**
- clients must encrypt data before sending to amazon s3
- client must decrypt data themselves when retrieving from s3

![[Pasted image 20240820221649.png|400]]

---

### CORS - Cross Origin Resource Sharing 

- origin = scheme (protocol) + host (domain) + port
	- eg: `https://www.example.com`

same origin : `https://example.com/page1` and `https://example.com/page2
different origin : `https://example.com` and `https://otherexample.com`

the request won't be fulfilled unless the other origin allows for the request using CORS headers

it is a web browser security

![[Pasted image 20240820224003.png|500]]

---
### S3 - MFA Delete

- generated code on device before doing an important operation on S3 

- MFA is required to:
	- permanently delete an object
	- suspend versioning

- To use MFA delete, versioning must be enabled 
- only the bucket owner (root account) can enable/disable MFA delete.

---
### S3- Access Logs

- any request made to the s3 account, from any account will be logged into another s3 bucket
- target logging bucket must be in the same AWS region

![[Pasted image 20240820235518.png|100]]
- logging bucket should not be the same as monitored bucket
![[Pasted image 20240820235554.png|300]]

---
### Pre Signed URLs

- can generate pre signed URLs using S3 console, CLI, SDK
- URL expiration
	- s3 console - 12hrs
	- AWS CLI - 168hrs

- pre-signed URLs contain the permissions of the user that generated the URL for GET/PUT

![[Pasted image 20240821001516.png|100]]

---
### S3 Glacier Vault Lock

- Create a vault lock policy
- lock the policy for further edits (cannot be changed)
- helpful for compliance and data retention

**s3 object lock**

- Retention mode - Compliance
	- object version cant be overwritten
	- cant be deleted by any user including root
	- retention period can't be shortened 

- Retention mode - Governance
	- most users can't overwrite or delete object version
	- some users have special permissions to change or delete the obj

- Retention Period - protect the object for fixed period, can be extended

---
### S3 Access Points


![[Pasted image 20240821002629.png|400]]

---

Date: 20/08/2024
Vivek Malapaka

---
