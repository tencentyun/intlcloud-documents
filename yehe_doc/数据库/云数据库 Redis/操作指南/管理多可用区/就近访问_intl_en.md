To reduce the access latency of a multi-AZ deployed instance, TencentDB for Redis allows you to read local nodes only. The principle is as follows:
- Enable the "read-only replicas" feature. (Before you enable the feature, confirm that data delay of replicas is allowed.)
- Enable the "read local nodes only" feature by setting a database parameter.
- If there is an available proxy node in the same AZ as the load balancing cluster, the cluster can perceive and access it only.
- The proxy node can access the AZ information stored in Redis nodes and route read requests to a Redis node in the same AZ.

## Enabling the "Read Local Nodes Only" Feature
The "read local nodes only" feature is disabled by default. You can enable/disable the feature for an existing instance by setting a database parameter on the **Parameter Settings** page in the console. Or, you can create a parameter template in which the parameter is specified and apply the template when creating an instance.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the **Parameter Settings** page, set `read-local-node-only` to `yes` or `no` to enable or disable the feature.
![](https://main.qcloudimg.com/raw/07556436ee1853d0ba0db190921a812d.png)

## Read-Only Routing Policy
For more information, see [Read-only routing policy](https://intl.cloud.tencent.com/document/product/239/34590).

When the "read-only replicas" feature is enabled, a read-only routing policy can be used to control whether read requests are routed to the master node. However, when the "read local nodes only" feature is enabled, its the priority is higher than that of the read-only routing policy: read requests are routed to a local node first, and if there is no available local node, read requests are routed to other nodes according to the read-only routing policy. The following is an example:
1. Enable the "read-only replicas" feature and select a read-only routing policy (according to the policy, read requests will not be routed to the master node).
2. Enable the "read local nodes only" feature (`read-local-node-only` = `yes`).
3. Only one master node in the master AZ.
4. When the business in the master AZ accesses the proxy node in the master AZ, the proxy will ignore the read-only routing policy and route read requests to the master node in the master AZ to avoid reading across AZs.

