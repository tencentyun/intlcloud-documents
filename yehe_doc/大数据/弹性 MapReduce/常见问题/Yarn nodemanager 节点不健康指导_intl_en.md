### How do I fix an unhealthy node in YARN NodeManager?

#### Symptoms
When disk utilization of a core node exceeds 90%, NodeManager will set it as "Unhealthy".

#### Solution
1. You are recommended to use Cloud Monitor and set the alarm threshold for EMR node disk utilization to 80–85% in order to prevent the node from being flagged as unhealthy in NodeManager when the disk utilization exceeds 90%.
Configure the EMR disk utilization threshold in Cloud Monitor at the following address:
`https://console.cloud.tencent.com/monitor/policyTemplate`
![](https://main.qcloudimg.com/raw/a6018ed544407e2912427485ef25c57c.png)
2. If the disk capacity is insufficient, you can add core nodes and perform load balancing to reduce the load of HDFS storage on the core nodes.
3. Clean up the disk regularly, especially the following parts:
 - Storage space of the core nodes.
 - Entire storage space of HDFS.
