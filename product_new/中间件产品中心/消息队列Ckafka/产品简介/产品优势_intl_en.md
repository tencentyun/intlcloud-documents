This document describes the strengths of CKafka compared to Apache Kafka. 

![](https://main.qcloudimg.com/raw/61afe09bf008596f235e750a6c31854d.png)

## Strengths
#### Full Compatibility with Open-source Programs for Easy Migration
CKafka is not only compatible with Kafka 0.9 and 0.10, but also features exclusive cluster version 1.1.1.
The CKafka service system is based on the existing code of open-source Apache Kafka; therefore, your code can be migrated to high-performance CKafka without any modification required. For more information on migration, see [Migrating Data to CKafka](https://intl.cloud.tencent.com/document/product/597/17272).

#### High Performance
Tencent Cloud CKafka team has further fine-tuned the service performance to eliminate complex parameter configuration and offer higher performance.

#### High Availability
Backed by Tencent's many years of experience in technical monitoring, CKafka features comprehensive monitoring on clusters and has a professional OPS team in place to respond to alarms on a 24/7 basis and ensure high availability of CKafka.
Multi-AZ disaster recovery solutions are available with imperceptible failover.

#### High Reliability
The disks used are highly reliable, and the service will not be affected even if 50% disks are damaged.
There are 2 replicas by default, and 3 replicas can be supported. The more replicas, the higher the reliability.

#### Parallel Scaling
CKafka eliminates the pain points in data migration faced by open-source Kafka and features imperceptible configuration upgrade.

#### Secure Public Network Access
SASL authentication is supported to secure public network access.

#### Data Security
CKafka provides various security features such as authentication, authorization, root account, and sub-account, enabling enterprise-level security protection.
VPC: Access from more secure VPC is supported.
Root account and sub-account: CAM features such as root account, sub-account, and collaborator are fully supported, enabling authorization between root account and sub-account as well as across organizational accounts.

## Connectivity with Associated Services
#### Connectivity with Tencent Cloud Services
CKafka can be easily connected to other Tencent Cloud services such as COS and EMR.
#### Kafka Connector
Data transfer based on open-source Kafka Connector is supported, so that data can be transferred between two Kafka clusters.
