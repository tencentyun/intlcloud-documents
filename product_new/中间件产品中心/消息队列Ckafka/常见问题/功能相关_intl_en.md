### What is the difference between CKafka and CMQ?
CMQ provides financial-level message transmission with high reliability and high data persistence while ensuring strong data consistency.
CKafka is suitable for scenarios that require higher throughput and lower reliability (such as log aggregation). In addition, CKafka is compatible with existing Kafka users, enabling migration at zero cost and full instance exclusivity.

### Which version of the open-source Kafka is compatible with CKafka?
Currently, CKafka is fully compatible with the open-source Kafka API v0.9-0.10, allowing users free migration to the cloud.

### Which version of the open-source Kafka is the current CKafka based on?
The current CKafka is based on Apache Kafka v0.10. We recommend using v0.10 SDK for production and consumption.

### Does CKafka expose Zookeeper?
It does not expose Zookeeper nor its address.

### Does CKafka support public network access?
Currently, CKafka transfers data over the private network by default. As public network access runs the risk of issues such as delay and network environment security, we do not recommend using public network transfer long term.
If you have temporary need for public network transfer, please contact your Tencent Cloud account manager for evaluation and assistance.

### Does CKafka support message compression?
Currently, CKafka supports open-source Snappy and LZ4 message compression formats. As gzip compression consumes more CPU resources, it is currently not supported.
We recommend disabling message compression when testing.
Configuration Method: In the configuration file of the producer, set the compression.type parameter to snappy or lz4. The default is none, i.e. the feature is disabled.


### Can a Kafka client connect directly to the CKafka service?
CKafka is compatible with the open-source Kafka v0.9-0.10. You can connect to the message center via a Kafka client and deploy codes to Tencent Cloud services to produce or consume messages.

### What are the restrictions on a CKafka instance?
Restrictions on peak throughput, disk capacity and instance-level number of topics and partitions vary by instance specifications.




### Will CKafka lose messages?
- Apache Kafka does not guarantee no message loss. As CKafka is optimized in availability, Tencent Cloud promises a CKafka availability of over 99.95%.
- Ckafka users can enable ACK during production to avoid message loss and improve message reliability.
- Cluster changes and upgrades happen in seconds and will not affect user experience.
- CKafka is mainly used in big data processing scenarios that require high throughput and high performance but relatively low data reliability. In extreme cases, a small number of messages may be lost. If you require zero message loss and have relatively low requirement for performance, we recommend CMQ.


### How does CKafka guarantee security?
CKafka guarantees security with the following features:
- Tenant isolation: The network access of instances is naturally isolated among different accounts.
- Permission control: CKafka has an additional whitelist-based authentication mechanism at the application layer and supports SASL authentication.
- Security protection: Services such as multi-dimensional security protection and anti-DDoS attacks are provided.


