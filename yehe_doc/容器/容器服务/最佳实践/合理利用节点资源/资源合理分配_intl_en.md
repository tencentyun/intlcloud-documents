You can set request to schedule pods to nodes with sufficient resources but cannot ensure refined control. This document describes how to use node affinity, taint, and toleration to schedule pods to suitable nodes in order to make full use of resources.




### Using node affinity
- You can use node affinity to deploy services that have special node requirements to nodes that meet these requirements. For example, you can enable MySQL to schedule a model with high I/O to improve data reading and writing efficiency.
- You can use node affinity to deploy services that need to be associated. For example, you can ensure the web service and Redis cache service are deployed in the same availability zone to ensure a low latency.
- You can use node affinity to schedule separated pods to prevent issues caused by a single point of failure (SPOF) or centralized traffic.




### Using taint and toleration
Taint and toleration can help optimize cluster resource scheduling.
- You can add taints to nodes reserved for certain applications, which prevents other pods from being scheduled to these nodes.
- You can add tolerations to pods that need to use reserved resources. Tolerations work with node affinity, to ensure pods can be scheduled even when their affinity settings cannot be matched.

