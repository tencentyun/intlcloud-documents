### Broker
A broker is an individual CKafka server which is mainly used to receive messages sent by producers, assign offsets, and save messages to disks. At the same time, it also receives requests from consumers and other brokers, processes them according to their type, and returns responses.

### Partition
A partition is a physical concept for storing messages. Each topic can be divided into multiple partitions and should have at least one partition. Different partitions under the same topic contain different messages and are assigned to different brokers. Partition is the basis for CKafka's horizontal scalability. The parallel processing power of CKafka can be increased by adding servers and assigning partitions on them.

### Replica
A replica is a redundant backup of messages and used to ensure high service availability. Each partition can have multiple replicas, and all replicas have the same messages (however, they may not be exactly identical at the same time, subject to the synchronization mechanism). Each partition in CKafka has at least two replicas to guarantee high availability for services.

### Offset 
An offset is the unique serial number of a message in a partition.

### Producer
A producer is a partition used to produce messages and push them to a topic according to certain rules.

### Instance
An instance is the unit in which the CKafka service is purchased. Instances are divided into different specifications according to peak throughput (in MB/s) and disk capacity (in GB). You can purchase instances of different specifications to ensure the high reliability and availability of CKafka. The highly available cluster service is selected by default when you purchase an instance, where multiple broker servers are included and you do not need to concern over hardware devices.

### VPC
A [virtual private cloud (VPC)](https://intl.cloud.tencent.com/document/product/215) builds a separate network space in Tencent Cloud, which is very similar to a traditional network run in your IDC, except that the services hosted in a VPC are resources of your Tencent Cloud services such as CVM, CLB, and TencentDB. You don't have to care about the procurement and OPS of network devices at all; instead, you only need to customize IP ranges, IP addresses, routing policies, etc. through easy-to-use software programs. You can use EIPs, NAT gateways, and public gateways to flexibly access the internet or interconnect a VPC with your IDC through VPN or Direct Connect.

### Consumer
A consumer is a service that pulls messages from a topic and consumes them. Consumers maintain on their own the information about the offsets in the partitions they consume.

### Consumer Group
A consumer group is a set of consumers. In CKafka, multiple consumers can form a consumer group, but a consumer can belong to only one consumer group. The consumer group guarantees that each partition under the topic to which it subscribes is only assigned to one of the consumers in it for processing.
It is recommended that you specify a consumer group ID when messages are consumed. If this is not specified, the CKafka system will randomly generate a consumer group, which will be prone to reaching the maximum number of consumer groups in an instance. For more information, see [CKafka Billing Descriptions](https://intl.cloud.tencent.com/document/product/597/11745).

### Topic
A topic is a logical concept for storing messages and can be seen as a set of messages. Each topic can have multiple producers that push messages to it and multiple consumers that consume the messages.

### ZooKeeper	
ZooKeeper is a software program that provides consistency services for distributed applications, such as configuration maintenance, domain name service, distributed synchronization, and group service. In CKafka, ZooKeeper is mainly used to store the metadata of the cluster, elect leaders, and tolerate faults.	
