The performance comparison between CKafka and other messaging services is as follows:

| Feature |	CKafka	| Apache Kafka	| RabbitMQ	| RocketMQ	| CMQ |
|:--------|:--------|:--------|:--------|:--------|:--------|
| Advantages |	Very high throughput; <br>very elastic scalability; <br>very low OPS costs	| High throughout |	High reliability	| High reliability |	Very high reliability; <br>suitable for finance and other scenarios where strong consistence is required |
| Disadvantages | Occasionally message loss in extreme circumstances	| Occasionally message loss; <br>Less flexible scalability;<br>Multiple dependent components, leading to heavy OPS work; <br>Limited security protection, poor isolation and compatibility |	Poor performance; <br>Less flexible scalability 	| Manual (not automatic) high-availability switch	| Average throughout for guaranteed strong consistency |
| Programming language	|Scala	|Scala|	Erlang|	Java	|C++|
| Scalability	 | Very flexible and easy to scale. Only the VIP address needs to be specified for message sending, and broker changes are imperceptible for both message sending and receiving |	Not flexible enough. The broker address needs to be specified to send messages, and ZooKeeper coordination scheduling is required for message receiving |	Not flexible enough. The broker address needs to be specified for message sending |	Relatively flexible. The sender and receiver are connected to the name server | Flexible, smooth, and horizontally scalable. Logically, a single queue can provide services across multiple clusters |
| Throughput |	Very high |	High	| Average |	Average |	Average |
| General performance |	Million-level QPS	| Million-level QPS |	100-thousand-level QPS |	100-thousand-level QPS |	100-thousand-level QPS |
| "2-core 4 GB" stress test |	220,000 read/write QPS |	200,000 read/write QPS |	100,000 read/write QPS |	100,000 read/write QPS |	120,000 read/write QPS |
| Sync algorithm |	ISR (Replica) |	ISR (Replica) |	GM	| Synchronous double write |	Raft |
| Availability	| Very high availability. Automatic master/slave switch is supported. CKafka guarantees an availability of 99.95% |	 High availability. Automatic master/slave switch is supported. Messages may be lost after switch due to async flush and replication |	Automatic master/slave switch is supported. The mirror queue is used to support m/s where the master provides services and the slave implements backup only |	Automatic master/slave is not supported. The slave only reads but does not write when the master is not available |	Very high availability. The broker can provide high-availability services as long as it contains two nodes |
| Consumption method |	Pull |	Pull |	Pull and push |	Pull and push |	Pull and push |
| Message reliability |	High reliability; <br>Reliability can be further improved based on the three-copy mechanism, and the cluster features better disaster recovery where failures rarely occur |	Low reliability; <br>The broker has only async flush and async master/slave replication mechanisms, which may cause message loss	| High reliability; <br>When messages are sent, if they are specified as persistent, they will be written into the disk	| High reliability; <br>The broker supports sync doublewrite, and a success will be returned only after the message is written into both the master and the slave	| Extremely high reliability; <br>Message loss is eliminated with sync flush. The data persistence is 99.999999% |
| Data verification	| CRC |	CRC	| None	| CRC	| Checksum |
| Message rewind	| Yes	| Yes |	No |	No	| Yes |
| Security protection | Yes |	No | No | No | Yes |	
| Monitoring and alarming | Yes |	No | No | No | Yes |	
| Service support | Yes |	No | No | No | Yes |	

>"2-core 4 GB stress test" indicates the result of a stress test on a server with 2 CPU cores and 4 GB memory.
