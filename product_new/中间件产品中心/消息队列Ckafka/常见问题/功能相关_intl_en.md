### What is the difference between CKafka and CMQ?
CMQ provides finance-grade message transmission with high reliability and high data persistence while ensuring strong data consistency.
CKafka is suitable for scenarios where throughput requirement is higher while reliability requirement is relatively low (such as log aggregation). In addition, CKafka is completely compatible with existing Kafka clusters, enabling migration at zero cost and full instance exclusivity.

### Which versions of open-source Kafka are compatible with CKafka?
Currently, CKafka is fully compatible with open-source Kafka API v0.9-0.10, enabling you to cloudify your business at zero cost.

### Which version of the open-source Kafka is the current CKafka based on?
The current CKafka is based on Apache Kafka v0.10. It is recommended to use the v0.10 SDK for production and consumption.

### Does CKafka open ZooKeeper?
It does not open ZooKeeper or offer zk addresses.

### Does CKafka support public network access?
Currently, CKafka transfers data over the private network by default. As public network access involves problems such as delays, network environment restrictions, and security issues, it is not recommended to enable public network transfer for a prolonged time.
If you have temporary need for public network transfer, please contact your Tencent Cloud account manager for evaluation and assistance.

### Does CKafka support message compression?
Currently, CKafka supports open-source Snappy and LZ4 message compression formats. As gzip compression consumes more CPU resources, it is not supported for the time being.
During test, it is recommended that you disable message compression.
How to configure: In the configuration file of the producer, set the compression.type parameter to snappy or lz4, which is none by default.


### Can a Kafka client connect directly to the CKafka service?
CKafka is compatible with open-source Kafka v0.9-0.10. You can connect to the Message Center via a Kafka client and deploy the code in Tencent Cloud services to produce or consume messages.

### What are the limitations of a CKafka instance?
The restrictions on peak throughput, disk capacity, and instance-level number of topics and partitions vary by instance specification.




### Will CKafka lose messages?
- Apache Kafka does not guarantee that no messages will be lost. Tencent Cloud has specifically optimized CKafka for availability and promises a CKafka availability of over 99.95%.
- You can enable ACK during production to ensure that few or no messages will be lost and improve message reliability.
- Cluster change or upgrade is imperceptible to users and can be completed in a matter of seconds.
- CKafka is mainly applicable to scenarios of big data processing with high requirements for throughput and performance but less demanding requirement for data reliability. In extreme cases, a small number of messages may get lost. If you require zero message loss with relatively low requirement for performance, CMQ is recommended.


### How does CKafka guarantee security?
CKafka ensures security with the following features:
- Tenant isolation: The network access of instances is naturally isolated among different accounts.
- Permission control: CKafka has an additional whitelist-based authentication mechanism at the application layer and supports SASL.
- Security protection: Multi-dimensional security protection and DDoS attack prevention are provided.


