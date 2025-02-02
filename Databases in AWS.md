- - - 
### Database Types

| Type                               | Service                                               |
| ---------------------------------- | ----------------------------------------------------- |
| RDBMS (SQL/OLTP)                   | RDS, Aurora (great for joins)                         |
| NoSQL (no joins, no SQL)           | DynamoDB, Elasticache, neptune, DocumentDB, KeySpaces |
| Object Store                       | S3                                                    |
| Data Warehouse (SQL Analytics, BI) | Redshift, Athena, EMR                                 |
| Search                             | OpenSearch                                            |
| Graphs                             | Neptune                                               |
| Ledger                             | Amazon Quantum Ledger Database                        |
| Time series                        | Amazon Timestream                                     |

---
### Amazon RDS 

- Managed postgres, mysql, oracle, sql server, db2 
- provisioned RDS instance size and EBS Volume type and size
- supports read replicas and multi AZ
- security through IAM, KMS, SSL in transit
- automated backup point in time recovery (35 days)
- Manual DB snapshot for longer timer recovery
- RDS custom for access to underlying instance (oracle and SQL server)
- Use case : Store Relational Database, SQL queries, transactions

KeyWords - Relational Database , SQL , postgres, mysql, oracle

---
### Amazon Aurora

- Compatible for postgres SQL and mySQL 
- storage in 6 replicas across 3 AZ - highly available, self healing, auto scaling
- custom endpoints for writer and reader 
- same security/monitoring as RDS
- aurora serverless for unpredictable workloads
- aurora global - 16 DB read instances and <1 sec storage replication
- aurora database cloning - new cluster from existing one, faster than restoring from snapshot
- use case - same as RDS, less maintenance and more flexibility/ more performance and more features

KeyWords - Relational Database , SQL , postgres, mysql, highly available, flexible compared to RDS, serverless

--- 

### ElastiCache 

- Managed Redis/ Memcached (similar as RDS but for cache)
- in memory data store - sub millisecond latency
- security though IAM, KMS, Redis Auth
- Backup/Snapshot/Point in time - (Same as RDS)
- managed and scheduled maintenance 
- <mark style="background: #BBFABBA6;">Requires some application code changes to use elasticache</mark>
- Use case - frequent reads, less writes, store session data
- No SQL 

keywords: cache

---
### Amazon DynamoDB

- managed serverless, noSQL, <mark style="background: #BBFABBA6;">millisecond latency</mark>
- Capacity modes : provisioned with autoscaling or on-demand capacity
- highly available, multi AZ , read and writes are decoupled, transaction capability
- DAX as cache, microsecond read latency, 10x improvement
- security, authentication is done through IAM 
- Global Table - Active-active replication
- automated backups - 35 days PITR or on demand backups
- Export to S3, import to S3
- Great for rapid evolve schemas 
- use case: serverless application (small documents), serverless cache 

keywords : serverless, nosql, s3 integrations, small documents, No changes to codebase and caching 

---
### Amazon S3

- key/value store for objects
- great for bigger objects
- serverless scales, max object size - <mark style="background: #BBFABBA6;">5TB</mark>, versioning capability
- tiers : use lifecycle policy for managing tiers
- features : Versioning, encryption, replication, MFA - Delete, Access logs
- Encyption: SSE - S3, SSE - KMS, SSE - C, Clientside, TLS in transit
- Performance: multi part upload, s3 transfer acceleration , S3 select
- Automation: S3 event notifications (SNS,SQS)
- Use case: hosting static websites, store big objects

keywords - key/value storage, hosting static websites, bigger objects

--- 
### DocumentDB

- Aurora : Postgres SQL, MySQL :: DocumentDB : MongoDB
- documentDB is noSQL and compatible with mongoDB
- similar deployment concepts as Aurora
- fully managed, highly available with replication across 3 AZ
- grows automatically with increments of 10GB
- millions of requests per second 

keywords : mongoDB

---
### Amazon Neptune 

- fully managed graph database
- graph database example is social network 
- 15 read replicas spread across 3 AZ's
- can store billions of relations and can query the graph with millisecond latency
- highly available with replication across multi AZ
- wikipedia, fraud detection, social network are use cases

**Neptune Streams** 
- real time ordered sequence for every change made to your graph is sent to a stream called neptune stream 
- changes are available immediately after writing 
- no duplicates, strict ordering
- use cases : send notifications when changes are made and maintain your graph data in sync in another data store 

keywords: social media, graph

---
### Amazon Keyspaces (for Apache Cassandra)

- managed apache cassandra database service 
- serverless, scalable, highly available, fully managed by aws
- auto scaling based on traffic
- replicated 3 times across AZ
- query language is CQL - cassandra query language
- super fast
- capacity modes : on demand or provisioned mode with auto scaling 
- encryption and PITR 35 days
- use case: time series data, IOT device info

keywords: apache cassandra 

--- 

- Financial transactions, Ledger - QLDB 

### Amazon Timeseries

- fully managed, serverless, time series database
- automatically scale up and down 
- store and analyze trillions of events per day
- 1000 times faster and 1/10th of cost of relational database
- SQL compatibility 
- recent data is kept in memory , older data is kept in cost optimized storage
- time series analytic functions 
- encryption at rest and in flight
- use case: IOT, etc

keywords: time series 

---

Date: 21/09/2024
Vivek Malapaka

---