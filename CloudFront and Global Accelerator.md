- - -
### Introduction

- Content Delivery Network (CDN)
- Content is cached at edge location - improves read performance - lower latency

CloudFront Origins
- S3 Bucket
- Custom Origin (HTTP)
	- ALB
	- EC2
	- S3 Website 


![[Pasted image 20240917150438.png|400]]

- Files are cached for a TTL (maybe for a day)

---

### CloudFront - ALB / EC2 as an Origin


![[Pasted image 20240917151318.png|500]]

---
### CloudFront Geo Restriction 

- Allowlist - Allows users to access content from list of approved countries
- BlockList - Prevents access from list of banned countries 

Use Case - Copyright laws

---
### CloudFront - Pricing 

- Reduce the number of edge locations for cost reduction 
- Three Price Classes
	- Price Class All : all regions - best performance ($++)
	- Price Class 200 : most regions, exclude most expensive
	- Price Class 100 : only least expensive regions


![[Pasted image 20240917152010.png|400]]

---
### CloudFront - Cache Invalidations 

- If you make any changes at the backend, cloudfront doesn't know until the TTL is expired 
-  perform cloudfront invalidation
- invalidate all file `(*)` specific path `(/images/*)`

![[Pasted image 20240917161419.png|300]]

---
### AWS Global Accelerator

- Unicast IP - one server holds one IP address
- Anycast IP - all servers hold same IP, client is routed to nearest one.

works with ElasticIP, EC2, ALB, NLB 
Consistent Performance
- lowest latency
- no issue with client cache
- internal aws network

![[Pasted image 20240917180153.png|500]]


| Feature                 | AWS Global Accelerator                     | Amazon CloudFront                            |
| ----------------------- | ------------------------------------------ | -------------------------------------------- |
| **Primary Use**         | Improve global application performance     | Deliver static and dynamic web content (CDN) |
| **Traffic Type**        | TCP, UDP (all traffic types)               | HTTP/HTTPS                                   |
| **Caching**             | No caching                                 | Content caching at edge locations            |
| **Static IP Addresses** | Provides static Anycast IPs                | No static IPs, uses DNS-based routing        |
| **Routing**             | Routes traffic to AWS regions or endpoints | Routes traffic to edge locations             |
| **Failover**            | Automatic failover across regions          | No regional failover (focuses on caching)    |
| **Security**            | Integrated with AWS Shield & AWS WAF       | Integrated with AWS Shield & AWS WAF         |

---

Date: 17/09/2024
Vivek Malapaka

---
