## CKafka Overview
Based on the open-source Apache Kafka message queuing engine, Message Queue CKafka (CKafka) provides high-throughput and highly scalable message queuing services. It is perfectly compatible with the APIs of Apache Kafka v0.9, v0.10, v1.1, v2.4 and v2.8 and has greater advantages in terms of performance, scalability, business security, and Ops, allowing you to enjoy powerful features at low costs while eliminating tedious Ops work.

## Features
- **Message Decoupling**
  CKafka effectively decouples the relationship between message producer and consumer, allowing you to independently scale or modify the production/consumption processing procedure as long as they follow the same API constraints.

- **Peak Shifting**
  CKafka can withstand access traffic surges instead of completely crashing due to sudden overwhelming requests, which effectively boosts system robustness.
  
- **Sequential Read/Write**
  CKafka can guarantee the order of messages in a partition. Just like most message queue services, it can also ensure that data is processed in order, greatly improving disk efficiency.

- **Async Communication**
  In the scenario where the business does not need to process messages immediately, CKafka provides an async message processing mechanism, that is, when the traffic is high, messages will be put into the queue only and processed after the traffic drops, which significantly relieves the system pressure.

>?CKafka supports private deployment. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for consultation.
