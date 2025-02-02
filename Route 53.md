- - -
### DNS - Domain Name System

- translates human friendly hostnames into the target machine IP addresses

**Terminologies**
- DNS Registrar : Amazon Route 53, GoDaddy .... 
- DNS Records : A, AAA, CNAME etc
- Top Level Domain (TLD): .com, .us, .in, .gov, .org
- Secondary Level Domain (SLD) : google.com, amazon.com

![[Pasted image 20240814101203.png|300]]

How DNS works? 

- first the local DNS server asks the root DNS server for example.com
- then it asks the TLD for example.com
- then it asks the secondary level domain DNS server and it gives the answer
- the Local DNS server will cache the IP of example.com for a period of time 
- and it gives the web browser it IP address of example.com and we can access it.

![[Pasted image 20240814101631.png|500]]

---
### Route 53

- Highly available, scalable and fully managed DNS 
- Route 53 is also a domain registrar
- can also perform health checks 

![[Pasted image 20240814102753.png|300]]

Route 53 - We'll have a bunch of DNS records and these records contains 
- Domain/Subdomain Name : example.com
- Record Type : A, AAA, CNAME
- Value : 12.34.56.78
- Routing Policy : How route 53 responds to queries
- TTL - amount of time the record is cached. 

**Record Types**

- A - Maps a hostname to Ipv4
- AAAA - Maps a hostname to IPv6
- CNAME - maps hostname to another hostname
	- target domain name which must have an A or AAAA record

**Hosted Zones**

- container of records
- defines how to route traffic to a domain and it's subdomains

**Public Hosted Zones** - contains records on how to route traffic on internet (public domain names)

![[Pasted image 20240814103821.png|300]]

**Private Hosted Zones:** contains records on how to route traffic on a private VPC (private domain names)

![[Pasted image 20240814103853.png|300]]

---

### Records TTL (Time To Live)

- High TTL 
	- less traffic on route 53
	- possibly outdated records
- Low TTL
	- More traffic on route 53 ($++)
	- Records are outdated for less time 
	- easy to change records

![[Pasted image 20240814105721.png|400]]

---
### CNAME vs Alias

**CNAME** : 
- points hostname to other hostname (app.mydomain.com -> blabla.anything.com)
- only for non root domain 

**ALIAS** : 
- points hostname to AWS service (app.mydomain.com -> something.amazonaws.com)
- works for both root domain and non root domain 
- free of charge
- health checks

![[Pasted image 20240814110706.png|400]]

- Alias record is always of type A/ AAAA
- The TTL is not sent automatically by aws when asked for that particular record. we cannot set ttl to alias records.

**Alias Target Records:** 
- elastic load balancers
- cloudfront 
- s3 websites
- other aws services

You cannot set an ALIAS record for an EC2 DNS name. 

---

### Routing Policy - Simple

- route traffic to single resource
- if a resource has multiple values, all the values are given to the client 
- the client will randomly pick one and have access to the resource

![[Pasted image 20240814114337.png|300]]

---
### Routing Policy - Weighted

- resources are assigned a particular weight
$$
traffic = weighs\:of\:specific\:record\:/sum\:of\:all\:the\:wieghts\:for\:all\:the\:records)
$$

- can be associated with health checks
- assign weight 0 to a record to stop sending traffic
- if all the records have weight 0, all the records will be returned with equally.

![[Pasted image 20240814115531.png|200]]

---
### Routing Policy - Latency

- redirects to a resource that has the least latency close to the user 
- helpful with latency is priority 
- latency is based on traffic between users and aws region
- can be associated with health checks. 
- it will direct to the aws region which the user can reach at a less time. 

![[Pasted image 20240814132235.png|400]]

---
### Health Checks

- HTTP health checks for public resources
- we use health checks for automated DNS failover and we use then on
	- monitor an endpoint (application, AWS resource, server)
	- monitor other health checks (calculated health checks)
	- monitor cloudwatch alarms (for private hosted resources)

**Health checks  - Monitor an endpoint**

- 15 global health checkers will check the end point health 
	- healthy or unhealthy threshold - 3 seconds
	- interval of health checks - 30 seconds
	- supports HTTP, HTTPS, TCS

- if > 18% of the checks report the endpoint healthy, it's healthy otherwise, it's unhealthy

![[Pasted image 20240814173729.png|300]]

**Health checks  - Calculated Health Checks**

- multiple health checks into a single health checks
- can monitor upto 256 child health checks 
- can specify how many of the child health checks need to pass for the parent to pass 

![[Pasted image 20240814174014.png|300]]

**Health Checks on a private hosted zone**

- Route 53 checks can't access private endpoints
- Create a cloudWatch metric and an alarm and then check create a health check that checks the alarm

![[Pasted image 20240814174324.png|300]]

---
### Routing Policy - Failover

- perform health checks on the primary EC2 instance (mandatory in failover policy)
- if fail, the Route 53 will start sending the DNS requests to the secondary Ec2 instance 

![[Pasted image 20240814174925.png|400]]

---
### Routing Policy - Geolocation

- Routing is based on user location
	- eg: if the user is in Germany - direct them to an IP address which has the German version of the app
	-  if the user is in France - direct them to an IP address which has the French version of the app 
	- if they don't belong to both, send them to default, might contain the English version of the app (DEFAULT)

- can be associated with health checks

![[Pasted image 20240814175619.png|300]]

---
### Routing Policy - Geoproximity

- set bias on aws availibilty zone
	- more bias, more traffic
	- less bias, less traffic 
	- no bias, equally distributed

![[Pasted image 20240814180109.png|400]]

![[Pasted image 20240814180128.png|400]]

---
### Routing Policy - IP 

- Routing is based on clients IP addresses 
- Define CIRD collection - Range of IP's and assign them to a particular EC2 instance 

![[Pasted image 20240814180325.png|300]]

---

Date: 14/08/202
Vivek Malapaka

---
