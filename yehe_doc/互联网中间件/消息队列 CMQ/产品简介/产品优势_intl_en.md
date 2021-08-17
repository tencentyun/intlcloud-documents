

## Advantages over RabbitMQ
- **QPS:** CMQ features higher QPS. When high reliability is ensured and the same physical device is used, the throughput of CMQ is four times higher than that of RabbitMQ, with a single CMQ cluster providing over 100,000 QPS.

- **Message rewind:** RabbitMQ does not support message rewind, while CMQ allows you to rewind messages by time; for example, messages can be consumed again from a specified time point on the day before. In a typical scenario where a consumer needs to analyze orders, if the messages consumed today have all become invalid due to problems such as program logic errors or dependent system faults, then the messages need to be consumed again from 00:00 yesterday on, and message rewind will be much helpful in this case.

- **Consistency algorithm:** CMQ and RabbitMQ both support hot backup with multiple servers to improve availability. CMQ implements this feature based on the Raft algorithm which is simpler and easier to be maintained. RabbitMQ uses its proprietary Guaranteed Multicast (GM) algorithm which is difficult to learn.

- **OPS difficulty:** OPS in RabbitMQ is more difficult, as it is developed in Erlang, a less popular programming language that has higher learning costs.

## Advantages over RocketMQ
- **Data loss**: in extreme cases, data may be lost in RocketMQ. Because RocketMQ allows ACK to be returned to the client before data flushing, messages will be lost when the server is down due to exceptions.

- **Multiple masters and slaves**: multiple masters and slaves need to be set up for RocketMQ to ensure high business availability. RocketMQ can ensure availability and reliability only when there are healthy nodes in ISR; otherwise, the availability and reliability cannot be guaranteed, and the overheads will be high.

Therefore, compared with traditional open-source message queue applications, Tencent Cloud CMQ has the following advantages:

| Comparison Items | Tencent Cloud CMQ | Open-Source Messaging Middleware | 
|---------|---------|---------|
| High performance | High performance and reliability can be guaranteed at the same time, and the QPS of a single CMQ instance reaches 5,000 | High performance and reliability cannot be guaranteed at the same time |
| High scalability | <li>The number of queues and queue storage capacity are highly scalable</li><li>The underlying system can be automatically scaled based on the business volume, which is imperceptible to upper-layer businesses</li><li>Hundreds of millions of messages can be received, sent, pushed, and retained efficiently with an unlimited capacity</li><li>The message service is provided in multiple regions: Beijing, Shanghai, and Guangzhou</li> | <li>The numbers of queues and retained messages are limited</li><li>Each IDC needs to have devices purchased and deployed, which is complicated</li> |
| High reliability | <li>Backed by Tencent's proprietary Cloud Reliable Message Queue (CRMQ) distributed framework, CMQ has been widely used in Tencent businesses such as QQ and WeChat red packet systems and lottery</li><li>CMQ ensures that data is replicated to different physical servers in three copies before a successful write of each message is returned to the user, and the backend data replication mechanism guarantees that data can be quickly migrated when any physical server fails, so that the three copies of user data are always available with a reliability of 99.999999%</li><li>The improved Raft consistency algorithm is integrated to delivery a strong data consistency</li><li>The business availability is guaranteed at 99.95%</li> | <li>Data is stored in single servers or a simple master/slave architecture, where data cannot be rewound once lost due to single points of failure</li><li>The open-source replica algorithm will cause rebalancing of global data when a server is added to or removed from the cluster, drastically bringing down the availability</li><li>If Kafka flushes and replicates data asynchronously, strong data consistency cannot be ensured</li> |
| Business security | <li>Multi-dimensional security protection and anti-DDoS services are provided</li><li>Each message service has an independent namespace to strictly isolate data of different customers</li><li>HTTPS access is supported</li><li>Cross-region secure message service is supported</li> | <li>The security protection features are limited</li><li>To avoid public network threats, cross-region and cross-IDC services over the public network usually cannot be provided</li> |
