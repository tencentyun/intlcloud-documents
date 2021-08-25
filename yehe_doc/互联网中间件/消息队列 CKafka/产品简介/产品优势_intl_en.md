This document describes the strengths of CKafka compared to Apache Kafka.

![](https://main.qcloudimg.com/raw/61afe09bf008596f235e750a6c31854d.png)



## Strengths

#### Full compatibility with Apache Kafka and easy migration

- CKafka is compatible with Kafka 0.9, 0.10, 1.1 and 2.4.
- CKafka is based on the existing code of the open-source Apace Kafka ecosystem. Without any changes to your existing project, you can migrate data to the cloud and enjoy the high-performance message queue services provided by Tencent Cloud Kafka.

#### High performance

- The message queue team at Tencent Cloud has optimized CKafka to allow you to enjoy higher-performance services without having to go through a complicated process of configuration.
- CKafka supports upgrade and downgrade via UI operations and is backed by a powerful IaaS layer, delivering 10% to 20% higher production capabilities than Apache Kafka.

#### High availability

- Leveraging Tencent's years of experience in monitoring technologies, CKafka offers comprehensive monitoring on clusters and has a professional OPS team in place that responds to alarms on a 24/7 basis to ensure high availability.
- Custom multi-AZ deployments in the same region is supported to improve disaster recovery ability.

#### High reliability

- CKafka uses highly reliable disks and can keep its services running even if 50% of the disks are unavailable.
- 2 replicas are created by default, and up to 3 replicas can be used. The more replicas, the higher the reliability.

#### Parallel scaling

- The backend system automatically scales resources when cluster traffic and disk usage hit the alarm thresholds. The client side is unaffected during the process.
- CKafka solves the problems in data migration with Apache Kafka and features smooth upgrade with no influence on your business.

#### Data security

CKafka provides security capabilities including authentication, authorization, and root account/sub-account, offering enterprise-level security services.
- VPC: supports access from Tencent Cloud VPC, enhancing network security.
- SASL authentication: allows safer public network access.
- Root account/sub-account: supports CAM features including root account/sub-account and collaborator, enabling authorization between root and sub-accounts as well as across organizational accounts.

## Connectivity with Related Services

#### Integration with cloud services

CKafka can easily integrate with other Tencent Cloud services such as COS and EMR.

#### Kafka Connector

CKafka supports data transfer based on open-source Kafka Connector, enabling data transfer between Kafka clusters.
