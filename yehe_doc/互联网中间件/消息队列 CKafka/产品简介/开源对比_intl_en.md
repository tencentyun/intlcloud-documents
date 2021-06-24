The performance comparison between CKafka and open-source Apache Kafka is as follows:



| Feature       | CKafka                                                       | Apache Kafka                                                 |
| ---------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| Advantages       | <li>Very high throughput </li><li>Very elastic scalability </li><li>Very low OPS costs</li>           | High throughout                                                     |
| Disadvantages       | Occasional message loss in extreme circumstances                                         | <li>Occasional message loss </li><li>Less flexible scalability </li><li>Multiple dependent components, leading to heavy OPS work </li><li>Limited security protection and poor isolation and compatibility</li> |
| Throughput     | Very high                                                       | High                                                         |
| General performance   | Million-level QPS                                                    | Million-level QPS                                                    |
| <nobr>2-core 4 GB stress test</nobr> | 220,000 read/write QPS                                                  | 200,000 read/write QPS                                                  |
| Cost       | Very flexible billing based on your estimated peak traffic and disk capacity             | High costs with labor and OPS environment required                        |
| OPS       | Complete monitoring and alarming system, OPS ticket system, and CKafka R&D experts who answer questions at any time to quickly solve your problems | Cumbersome OPS and deployment where it is difficult to locate problems                |
| Scalability   | Very flexible and easy to scale. Only the VIP address needs to be specified for message sending, and broker changes are imperceptible for both message sending and receiving | Not flexible enough. The broker address needs to be specified to send messages, and ZooKeeper coordination scheduling is required for message receiving |
| Availability     | Very high availability. Automatic leader/follower switch is supported. CKafka guarantees an availability of 99.95%     | High availability. Automatic leader/follower switch is supported. Messages may be lost after switch due to async flush and replication |
| Message reliability | <li>High reliability </li><li>Reliability can be further improved based on the three-copy mechanism, and the cluster features better disaster recovery where failures rarely occur</li>| <li>Low reliability </li><li>The broker has only async flush and async primary/secondary replication mechanisms, which may cause message loss</li> |
| Security protection   | Supported                                                         | Not supported                                                       |
| Monitoring and alarming   | Supported                                                         | Not supported                                                       |
| Service support   | Supported                                                         | Not supported                                                       |

>?
>- "2C 4GB Stress Test" indicates the result of a stress test on a 2-core 4GB memory server.
>- CKafka is compatible with the Producer and Consumer APIs of Apache Kafka 0.9 and later versions. To connect to an on-premises Kafka of an earlier version (such as v0.8), the APIs need to be rewritten. For details, see [Connecting to On-Premises Kafka of Earlier Versions](https://intl.cloud.tencent.com/document/product/597/11173).
