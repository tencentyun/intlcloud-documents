<style>
table th:nth-of-type(1) {
width: 10%;        
}
table th:nth-of-type(2) {
width: 20%;        
}
table th:nth-of-type(3) {
width:50%;        
}
table th:nth-of-type(4) {
width: 20%;        
}
</style>

This document describes the updates to TDMQ for Pulsar clusters as well as relevant notes.

## Version 2.7.1

**Release date:** May 17, 2021

**Full switch:** June 2021

**Release notes:**

| Update Type | Update                               | Description                                                     | Documentation                                                     |
| -------- | ------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Optimization     | Unified domain name access                         | <li>A unique domain name is automatically generated for each network environment of each cluster as the access address, so you don't need to manually create and manage access points.</li> <li>The dependency that declares `listenerName` is removed, so the SDK is more compatible with TCP clients in the community that are not adapted to multiple advertised listeners in Pulsar (including C++, Python, and Node.js).</li> | <li>[Apache Pulsar SDK for C++](https://intl.cloud.tencent.com/document/product/1110/42949)</li> <li>[Apache Pulsar SDK for Python](https://intl.cloud.tencent.com/document/product/1110/42950)</li><li>[Apache Pulsar SDK for Node.js](https://intl.cloud.tencent.com/document/product/1110/42951)</li> |
| Addition     | Support for public network access                        | Public network access is supported, so you can access a TDMQ for Pulsar cluster in Tencent Cloud from a TCP client in your local system or self-built IDC. | [Getting Access Address](https://intl.cloud.tencent.com/document/product/1110/42928) |
| Optimization     | Update to the naming conventions for the retry letter and dead letter topics        | The naming conventions for the retry letter and dead letter topics are updated to the same as used by the Pulsar community, so that they are more compatible with open-source SDKs (the new naming conventions are not applicable to the original Tencent Cloud SDK)  | [Message Retry and Dead Letter Mechanisms](https://intl.cloud.tencent.com/document/product/1110/42925) |
| Optimization     | Performance optimization                             | Clusters on v2.7.1 are optimized at the system kernel level to achieve a 20% higher peak production/consumption performance than clusters on v2.6.x. In addition, they can be scaled imperceptibly according to the actual usage. | -                                                            |
| Addition     | Support for protocol-compatible plugins (in closed beta test) | You can install plugins compatible with AMQP, RocketMQ, and CMQ in clusters on v2.7.1. Currently, this feature is in beta test. After it is officially launched, you will be able to access TDMQ for Pulsar from popular message queue clients with no modifications required, which will make it easier for you to migrate existing businesses. | -                                                            |

## Version 2.6.1

**Release date:** October 12, 2020

**Full switch:** October 2020

**Release notes:**

| Update Type | Update                               | Description                                                     | Documentation                                                     |
| ---------------- | ------------------------------------------------------------ | -------- | -------- |
| Optimization | Stability enhancement       | Issues discovered during the beta test are fixed, significantly improving the cluster stability.              |    -      |
| Optimization | Hot/Cold data isolation in ZooKeeper       | The ZooKeeper component of the Pulsar kernel adopts the deployment architecture of hot/cold data isolation, where metadata and cluster broker configuration data are deployed separately in two ZooKeeper instances to increase the cluster stability.      |       -   |
| Addition | Support for creation of virtual clusters | You can create virtual clusters in the console for resource isolation.                   |      -    |

**Upgrade notes:**

- All newly created clusters will be automatically on the latest version in the current region.

- To switch to the new cluster version on your own, follow the steps below:


1. Create a cluster (all newly created clusters are on the latest version) and a copy of completely identical metadata (namespaces, role permissions, topics, and subscriptions).
2. Replace the original production/consumption access point in the client code with the access address of the new cluster.
3. Replace the authentication information (token) in the client code with the token of the new cluster.
4. Switch the producer client first (recreate a producer application and deploy it in the production environment).
5. Wait for all retained messages in the original cluster to be consumed and then switch the consumer client (recreate a consumer application and deploy it in the production environment).
