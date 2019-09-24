### Broker
A broker is an individual CKafka server mainly used to receive messages sent by producers, assign offsets, and save messages to disks. It also receives requests from consumers and other brokers, processes them based on request types, and returns responses.

### Partition
A partition is a physical concept for storing messages. Each topic can be divided into multiple partitions and should have at least one partition. Different partitions under the same topic contain different messages and are assigned to different brokers. Partition is the basis of CKafka's horizontal scalability. We can increase the parallel processing power of CKafka by adding servers and assigning partitions on them.

### Replica
A replica is a message backup used to ensure high service availability. Each partition can have multiple replicas that have the same messages (this is subject to the synchronization mechanism as replicas may not be exactly the same at the same time). In CKafka, each partition has at least 2 replicas to guarantee high service availability.

### Offset 
An offset is the unique identifier of a message in a partition.

### Producer
A producer produces messages and pushes each message to a topic partition according to certain rules.

### Instance
An instance is the unit used to purchase CKafka services. Instances are categorized by different specifications according to peak throughput (in MB/s) and disk capacity (in GB). You can purchase instances with different specifications to ensure the high reliability and availability of CKafka. A highly available cluster service is selected by default when you purchase an instance, where multiple broker servers are included and you do not need to worry about hardware devices.

### VPC
[Virtual Private Cloud (VPC)](https://intl.cloud.tencent.com/document/product/215) allows you to build an independent network space on Tencent Cloud, which closely resembles the traditional network hosted in your IDC, except that a VPC hosts your Tencent Cloud resources, such as CVM, CLB, and TencentDB. There is no need to consider the purchase and OPS of network devices, you only need to use softwares to customize IP range divisions, IP addresses, routing policies, etc. You can access the internet easily via EIPs, NAT gateways, and public gateways to access the internet or use VPN/Direct Connect to connect your VPC with IDC.

### Consumer
A consumer pulls and consumes messages from a topic. The consumer maintains information about the offsets of its consumed messages in a partition.

### Consumer Group
A consumer group is a set of consumers. In CKafka, multiple consumers can form a consumer group, and each consumer can only belong to one consumer group. Consumer group guarantees that each partition under the topic to which it subscribes to is assigned to exactly one consumer in the group.
We recommend that you specify a consumer group ID when messages are consumed. Otherwise, CKafka system will randomly generate a consumer group, which may reach the maximum number of consumer groups allowed. For more information, see [CKafka Billing Descriptions](https://intl.cloud.tencent.com/document/product/597/11745).

### Topic
A topic is a logical concept for storing messages and can be seen as a set of messages. Each topic can have multiple producers that push messages to it and multiple consumers that consume the messages.

### ZooKeeper	
ZooKeeper is a software program that provides centralized services for distributed applications, such as configuration maintenance, domain name service, distributed synchronization, and group service. In CKafka, ZooKeeper is mainly used to store the metadata of the cluster, elect leaders, and tolerate faults.
