Tencent Cloud EMR-Kafka offers the cloud hosting service of open-source Kafka, with convenient Kafka cluster deployment, configuration modification, monitoring and alarming, and other features, providing enterprises and users with safe, stable OLAP solutions. Kafka data pipelines have been the most commonly used data sources and data sinks in stream computing systems. You can import streaming data into a certain topic in Kafka, process it through Flink operators, and output it to another topic in the same or a different Kafka instance. Kafka supports reading/writing data from/to multiple partitions in the same topic, which increases throughput and reduces data skew and hotspots.

## Architecture
Both single-node and multi-node architectures are available for your choice based on business needs.

## OPS
The console provides out-of-the-box services such as monitoring, log search, and parameter adjustment.

## Features
- Sending-receiving decoupling: the relationship between producers and consumers is effectively decoupled. Under the premise that the same API constraint is ensured, the processing between producers and consumers can be independently expanded or modified.
- Flexibility: Kafka clusters are able to withstand sudden increases in requests without breakdown, effectively improving the robustness of the system.
- Orderly reading and writing: Kafka clusters can guarantee the order of messages in a partition. Just like most message queue services, they can also ensure that data is processed in order, greatly improving disk efficiency.
- Asynchronous communication: in scenarios where the business does not need to process messages immediately, Kafka clusters provide the asynchronous message processing mechanism. When the traffic is heavy, messages are put into the queue only, and they will be processed after the traffic become lighter, which relieves the system pressure.

## Strengths
### 100% compatibility with open-source Kafka and easy migration
- Kafka clusters are compatible with open-source Kafka v1.1.1.
- The business system of Kafka clusters is based on the existing code of the open-source Apache Kafka ecosystem. Without any changes to your existing project, you can migrate to the cloud and enjoy the high-performance Kafka services provided by Tencent Cloud.

### High performance
- Tencent Cloud has improved the service performance, eliminating the need for complicated parameter configuration.
- You can upgrade or downgrade configurations on the UI and enjoy high-performance IaaS layer support.

### High availability
- Leveraging Tencent's years of experience in monitoring technologies, EMR offers comprehensive monitoring on clusters and has a professional OPS team in place that responds to alarms on a 24/7 basis to ensure the high availability of Kafka clusters.
- Custom multi-AZ deployment in the same region is supported to improve disaster recovery ability.

### High reliability
- The disks are highly reliable, making it possible to keep services running even if 50% of the disks become faulty.
- Two replicas are created by default, and up to three replicas can be used. The more replicas, the higher the reliability.
