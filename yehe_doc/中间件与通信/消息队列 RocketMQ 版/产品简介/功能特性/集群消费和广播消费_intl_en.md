This document describes the features and use cases of cluster consumption and broadcast consumption in TDMQ for RocketMQ.

## Feature Description

- Cluster: If the cluster mode is used, any message only needs to be processed by any consumer in the cluster.
- Broadcast: If the broadcast mode is used, each message will be pushed to all registered consumers in the cluster to ensure that the message is consumed by each consumer at least once.

## Use Cases

Cluster consumption is suitable for scenarios where each message only needs to be processed once.

Broadcast consumption is suitable for scenarios where each message needs to be processed by each consumer in the cluster.

## Sample Code

- **Cluster subscription**
All consumers identified by the same group ID will evenly share messages for consumption. For example, if a topic has nine messages, and a group ID identifies three consumer instances, then each instance will consume only three messages evenly in the cluster consumption mode.
```java
// Set the cluster subscription mode (which is the default mode if you don't specify one)
properties.put(PropertyKeyConst.MessageModel, PropertyValueConst.CLUSTERING);
```

- **Broadcast subscription**
A message will be consumed once by all consumers identified by the same group ID. In the broadcast consumption mode, for example, if a topic has nine messages and a group ID identifies three consumer instances, each instance will consume nine messages.
```java
// Set the broadcast subscription mode
properties.put(PropertyKeyConst.MessageModel, PropertyValueConst.BROADCASTING);               
```
>?You need to ensure that all consumer instances under the same group ID have the same subscription relationships.





  
