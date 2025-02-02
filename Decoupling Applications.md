- - - 

### Introduction 

- Two patterns of application communication
	- Synchronous 
		![[Pasted image 20240918212417.png|300]]
	
	- Asynchronous  
		![[Pasted image 20240918212504.png|300]]

it's always better to decouple the application
- SQS - queue model
- SNS - pub/sub model
- Kinesis - real time streaming model

--- 
### SQS

message queueing service

producer - someone who sends the message
consumer - someone who receives the message

the SQS queue decouples two applications

![[Pasted image 20240918213105.png|350]]

###### **Amazon SQS - Standard Queue**

- oldest AWS service (10yo)
- used to decouple applications 

- unlimited throughput (can send as many messages/sec)
- queue can have unlimited messaged 
- retention period - 4 days to 14 days
- low latency (on publish and receive)
- 256KB per message is the limit

**SQS - Producing Messages**
- messages are produced to SQS using a SDK (sendMessage API)
- message is persisted in SQS until consumer deletes 

![[Pasted image 20240918214029.png|200]]

**SQS - Consuming Messages**
- Consumers are applications running on ec2/ on premise servers etc
- consumer will ask the SQS for messages
- consumers can receive up to 10 messages at a time
- process the messages 
- delete the messages using (DeleteMessage API)

![[Pasted image 20240918214048.png|400]]


**Multiple EC2 Instances Consumers**

- Each consumer will receive different set of messages calling the poll function.
- consumers should delete the message after processing otherwise the other consumer will receive the message and it'll be processed again.
- consumers can be scaled using auto scaling group


Increase the number of instance (auto scaling group) using the number of messages as a metric 
![[Pasted image 20240918214605.png|400]]

Architecture Example: 

![[Pasted image 20240918214910.png|500]]

- Encryption - 
	- Inflight encryption using HTTPS API
	- At rest using KMS
	- Client side encryption 

--- 
### SQS - Message Visibility Timeout

- after a message is polled, then it becomes invisible to other consumers 
- "message visibility timeout" - by default 30 seconds

![[Pasted image 20240918223425.png|400]]

- if a message is not processed within the window, it'll be processed twice
- Call ChangeMessageVisibility API to get more time (if the consumer doesn't want the message to be processed twice)

- if the timeout is really high and the consumer crashes, reprocessing takes time
- too low, may get duplicate processing

---
### SQS - Long Polling 

keeping your consumer wait for a certain period of time for the messages to appear in the queue.

advantances:
- decreases the number of API calls
- increases efficiency and latency of the application

wait time can be from 1 to 20 seconds 

---
### SQS - FIFO Queue

FIFO - First in first out 

![[Pasted image 20240918224532.png|400]]

- Limited Throughput - 300msg/s without batching, 3000msgs/s with
- Messages are processed in order by the consumer

---
### Amazon SNS (simple notification service)

pub/sub - publish/subscribe

- msg is sent to SNS topic and the SNS topic will have subscribers 
- every time a message is added, that msg is sent to all the subscribers!

![[Pasted image 20240918233622.png|300]]

**Amazon SNS**

- event producer only sends msg to one SNS topic
- subscribers subscribe to the topic to get the msg sent by the producer 
- 12,500,000 subscriptions per topic
- 100,000 topic limits

![[Pasted image 20240918235044.png|400]]

- Many AWS services can send data to SNS for notifications

**How to Publish**

- Topic Publish 
	- Create a topic
	- create a subscription 
	- publish to the topic
- Direct Publish (for mobile apps)
	- create platform app
	- create platform endpoint
	- publish to endpoint

- Encryption - 
	- Inflight encryption using HTTPS API
	- At rest using KMS
	- Client side encryption 

---

### SNS + SQS : Fan Out

objective: write to multiple SQS 

- Push once in SNS 
- add SQS's as subscribers 
- fully decoupled, no data loss
- make sure SQS access policy allows for SNS to write to it.
- works for SQS queues in other regions

![[Pasted image 20240918235703.png|400]]

SNS - message filtering

![[Pasted image 20240919000157.png|400]]

---
### Amazon Kinesis

- collect, process, analyze streaming data in real time

- Kinesis Data Streams: capture, process and store data
- Kinesis Data Firehose: load data into AWS data stores
- Kinesis Data Analytics: analyze data streams
- Kinesis Video Streams: capture process and store video 
---

### Kinesis Data Streams

- way to stream big data in systems.
- made up of shards (no of shards should be mentioned before)

Properties:
- Retention between 1 to 365 days
- once inserted in kinesis, it cannot be deleted
- data that shares same partition key goes to the same shard 

Capacity Modes: 
- Provision Mode:
	- choose the number of shards provisioned, scale manually or using API
	- 1MB/s or 1000 msg/s/shard (in)
	- 2MB/s (out)
	- pay per shard per hour
- On Demand Mode: 
	- No need to provision or manage capacity
	- 4MB/s
	- scales automatically based on observed throughput peak 
	- pay per stream per hour 

![[Pasted image 20240919105024.png|500]]

---
### Kinesis Data Firehose

- Fully managed service, automatic scaling, serverless
- pay for data going through firehose
- near real time
	- Buffer interval - 0 sec to 900 sec
	- Buffer size - minimum 1MB
- Can send all failed or all data as a backup to S3 bucket

Consumers:
- AWS : Redshift, S3, OpenSearch
- 3rd party partners 
- Custom : HTTP endpoints

![[Pasted image 20240919110826.png|500]]

Differences between kinesis data streams and kinesis data firehose 

![[Pasted image 20240919110851.png]]

---
### Ordering data into Kinesis

**Ordering data into Kinesis**

- The same key will always go to the same shard
- here truck (1,3), truck (2,5) and truck 3 have same partition key
- So each truck will be sending data to the same shard and therefore data is ordered at shard level

![[Pasted image 20240919114816.png|300]]

---
![[Pasted image 20240919115903.png]]

---

Date: 19/09/2024
Vivek Malapaka

---