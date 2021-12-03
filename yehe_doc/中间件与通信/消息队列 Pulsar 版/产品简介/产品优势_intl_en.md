### Strong Data Consistency

By writing message data backups to various physical machines with sync flush, TDMQ for Pulsar achieves strong data consistency (like with the Raft algorithm) by using [BookKeeper consistency protocol](https://bookkeeper.apache.org/docs/4.12.1/development/protocol/#ensembles). When one of the physical machines fails, the backend data replication mechanism can quickly migrate the data to guarantee data backups are available.

### High Performance and Low Latency

With over 100,000 QPS per cluster, TDMQ for Pulsar can easily maintain the production and consumption of millions of messages, as well as retain an unlimited number of messages. It well sustains Tencent's all billing scenarios. It also offers a duration protection mechanism to ensure minimal latency and help you easily meet business performance requirements.

### Millions of Topics

TDMQ for Pulsar's computing and storage structures are designed to be independent of one another, allowing it to support millions of message topics with ease. When compared to other message queue products on the market, the performance of a TDMQ for Pulsar cluster will not suffer much as the number of topics increases.

### Rich Diversity of Message Types

TDMQ for Pulsar offers a rich diversity of message types, such as general, sequential (global and partitioned), distributed transaction, and scheduled messages, meeting the requirements for advanced features in various demanding scenarios.

### Unlimited Consumers

Different from Kafka's message consumption pattern, the number of consumers is not limited by the number of topics in TDMQ for Pulsar, and the quantity of messages per consumer is balanced using algorithms. Businesses can start with the appropriate number of consumers as needed.

### Multi-Protocol Connection

TDMQ for Pulsar provides a client API with language bindings for Java, Go, and C++. It also supports HTTP protocol for extended accessibility. It can be connected from open-source RocketMQ and RabbitMQ clients. If you only use its basic features to produce and consume messages, you can swiftly migrate to it with no code modifications required.

### Isolation Control
TDMQ for Pulsar offers a mechanism of topic isolation by tenant. It accurately controls the production and consumption speeds of each tenant, prevents the tenants from affecting each other, and ensures that message processing won't cause resource competition.

### Global Deployment
TDMQ for Pulsar furnishes global deployment capabilities, so you can choose a region close to your business presence for nearby access.
