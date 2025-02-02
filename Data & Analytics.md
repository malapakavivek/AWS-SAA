- - -
### Amazon Athena

- serverless query service to analyze data in amazon s3
- use SQL
- supports csv, json, ORC, avro, parquet
- 5$ per TB of data scanned
- Amazon Quicksight for creating dashboards 
- use case : BI, analytics, reporting or any aws logs

![[Pasted image 20240921153440.png|150]]

- use <mark style="background: #BBFABBA6;">columnar data for cost saving</mark> (parquet or ORC is recommended)
- improves performance
- use GLUE to convert data to parquet
- use larger files coz it'll be easy to scan and easy to retrieve 
- partition your datasets for easy querying

**Federated Query**
- Allows to run SQL queries across data stored in databases
- the results can be stored in s3 bucket

![[Pasted image 20240921153947.png|200]]

---
### Redshift

- based on postgres, not used for OLTP
- OLAP - analytic processing 
- columnar storage of data for speed
- Two modes: provisional cluster and serverless cluster
- SQL for queries
- BI tools such as quicksight tableau


- Leader node : query planning and result aggregation
- Compute node: performs the query and send result to leader

![[Pasted image 20240921163249.png|250]]

**Snapshots & DR**
- can restore a snapshot to a new cluster 
- automated : every 8 hrs, every 5 GB or on a schedule, we have to set retention
- Manual : snapshot is retained until you delete 

- automatically copy snapshots of a cluster to another cluster in another AWS region 

![[Pasted image 20240921163757.png|200]]

**Redshift Spectrum**

- query is submitted to thousands of redshift spectrum nodes
- these nodes perform the analysis and sends the results to the compute nodes 
- must have a redshift cluster to start the query

![[Pasted image 20240921164142.png|300]]

---
### Amazon OpenSearch

- DynamoDB -> query is possible by primary key or index
- with opensearch, you can <mark style="background: #BBFABBA6;">search any field</mark>, even partial matches
- used for search but <mark style="background: #BBFABBA6;">can also do analytic queries</mark> on top of it 
- Two modes : managed cluster or serverless cluster
- <mark style="background: #BBFABBA6;">does not natively support SQL</mark>, (can be enabled by a plugin)
- Ingestion from kinesis data firehose, AWS IoT, Cloudwatch logs
- comes with opersearch dasboards
- security through cognito IAM KMS TLS

![[Pasted image 20240921164850.png|400]]

![[Pasted image 20240921164914.png|400]]

---
### Amazon EMR

- EMR - Elastic Map Reduce
- EMR helps creating hadoop clusters for big data analytics
- clusters have to be provisioned - cluster is made of 100s of ec2
- EMR comes with lot of tools required for big data analytics
- Auto scaling and integrated with spot instances

use case: data processing, machine learning, web indexing, big data

**Nodes in EMR** 
- master node : manage the cluster
- Core node: run tasks and store data
- task node: only run tasks - usually spot instances 

---
### Amazon QuickSight

- serverless ML powered, BI service used to create interactive dashboards  
- fast, automatically scalable 
- use case: business analytics, visualizations, get business insights 
- integrated with RDS, aurora, athena, redshift and s3
- Columns level security - some columns are not visible to users who don't have access rights  - only @ enterprise edition
- SPICE - only with entire dataset is imported from computer, doesn't work if quicksight is attached to some service 

![[Pasted image 20240921170549.png|400]]

- you have users (standard versions) and groups (enterprise version)
- to share the analysis, you must first publish it 
- users who can see dashboard can also see the underlying data

--- 
### AWS Glue

- managed ELT (extract, transform and load service)
- prepare and transform data for analytics
- serverless service 

![[Pasted image 20240921171859.png|400]]

**Converting data into parquet format** 

![[Pasted image 20240921172252.png|400]]

![[Pasted image 20240921173036.png|500]]

Glue Job Bookmark - prevents re- processing of old data
Glue DataBrew - clean and normalize data using prebuilt transformations
Glue Studio - GUI to create and run ETL jobs

---
### AWS Lake

 - Data Lake - central place to have all data for analytic purposes
 - fully managed service, easy to setup data lakes in days 
 - automates cleansing, moving, collecting data (complex tasks)
 - combine structured and unstructured data
 - blueprints 
 - layer on top of AWS Glue
 - fine grained access control for your applications (row and column level)

- Centralized Permission 

![[Pasted image 20240921173211.png|400]]

instead of having security at all data sources, you enable access control at data lake 

---
### Kinesis Data Analytics 

**for SQL applications**

 - real time analytics on kinesis data streams and firehose
 - automatic scaling 
 - Output:
	 - kinesis data streams : create streams of real time analytic queries
	 - kinesis data firehose : send query results to destinations
- Use case:
	- time series analytics
	- real time dashboards
	- real time metrics 

![[Pasted image 20240921173948.png|500]]

**for apache fink**

- use flink to process and analyze data 
- flink <mark style="background: #BBFABBA6;">doesn't read from firehose</mark> (only data streams and MSK)

---
### Amazon MSK 

- MSK - managed streaming for apache kafka 

![[Pasted image 20240921174418.png|500]]

---

![[Pasted image 20240921175120.png]]


---

Date: 21/09/2024
Vivek Malapaka

---