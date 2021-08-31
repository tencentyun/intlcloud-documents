Based on the open-source Apache Kafka message queuing engine, Tencent Cloud Kafka (CKafka) provides high-throughput and highly scalable message queuing services. It is perfectly compatible with Apache Kafka APIs v0.9, v0.10, and v1.1 and has greater advantages in terms of performance, scalability, business security, and OPS, allowing you to enjoy powerful features at low costs while eliminating tedious OPS work.

CKafka operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|------------------|--------|----------------------------|
| Adding partition             | ckafka | AddPartition               |
| Adding route             | ckafka | AddRoute                   |
| Creating partition             | ckafka | CreatePartition            |
| Adding route             | ckafka | CreateRoute                |
| Creating topic             | ckafka | CreateTopic                |
| Adding topic allowlist          | ckafka | CreateTopicIpWhiteList     |
| Deleting route             | ckafka | DeleteRoute                |
| Deleting topic             | ckafka | DeleteTopic                |
| Deleting topic allowlist          | ckafka | DeleteTopicIpwhitelist     |
| Listing message groups           | ckafka | DescribeConsumerGroup      |
| Getting instance attribute           | ckafka | DescribeInstanceAttributes |
| Getting instance list           | ckafka | DescribeInstances          |
| Getting route details             | ckafka | DescribeRoute              |
| Getting topic list           | ckafka | DescribeTopic              |
| Getting topic attribute           | ckafka | DescribeTopicAttributes    |
| Getting instance attribute           | ckafka | GetInstanceAttributes      |
| Getting topic attribute           | ckafka | GetTopicAttributes         |
| Listing consumer groups           | ckafka | ListConsumerGroup          |
| Getting instance list           | ckafka | ListInstance               |
| Getting route details             | ckafka | ListRoute                  |
| Getting topic list           | ckafka | ListTopic                  |
| Setting CKafka message forwarding to COS | ckafka | ModifyForward              |
| Setting instance attribute           | ckafka | ModifyInstanceAttributes   |
| Modifying topic attribute           | ckafka | ModifyTopicAttributes      |
