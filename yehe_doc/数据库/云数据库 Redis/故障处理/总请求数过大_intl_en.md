## Error Description
- Symptom 1: the QPS value was high.
![](https://qcloudimg.tencent-cloud.cn/raw/a17ff6a9a1234786ebe2644ff62077bd.png)
- Symptom 2: the response latency increased.
- Symptom 3: connection timeout occurred.

## Common Causes
- The business needs to be optimized.
- The instance configuration needs to be upgraded.

## Solution
- Check the node load: for the cluster architecture, check the node load. If the QPS of only one or a few nodes exceeds the alarm threshold, there may be a hot key; if the QPS of most nodes is high, the overall load of the TencentDB for Redis instance is high, in which case the instance configuration needs to be upgraded.
- Check slow queries: you can check whether there are slow queries in the console, and if so and the slow queries match the time when the problem occurred, the problem may be caused by a big key.
- Check the CPU utilization: you can check whether the CPU utilization is too high, and if so, the machine resources may be insufficient, in which case the instance configuration needs to be upgraded.

If your business requires optimization, you can optimize it in terms of hot keys and big keys. If the instance configuration requires upgrade, you can enable read/write separation and add more shards to meet your current business needs.


## Troubleshooting Procedure
### [Optimizing your business](id:ywyh)
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the **System Monitoring** tab, check whether QPS is high or whether there are unexpected hot keys.
3. After troubleshooting exceptional access, optimize your business logic:
 - Hot keys: you can split hot keys of complex data structures into several new keys and distribute them across Redis nodes to reduce the pressure. For example, if a two-level hash hot key has a lot of hash elements, you can split it.
 - Big keys: if the value is too large, you can split the object into multiple key-values so that multiple Redis nodes will share the pressure. If there are too many keys, you can store multiple keys in a hash structure.


### [Upgrading the instance](id:slsj)
#### Heavy read load
[Add replicas](#zjfb) and enable [read/write separation](https://intl.cloud.tencent.com/document/product/239/31935) to share the read load.
>!Confirm that your business allows inconsistent data before enabling read/write separation, because after it is enabled, inconsistent data may be read from the replica node and the master node (the replica node lags behind the master node). For more information, see [Changing Instance Specification](https://intl.cloud.tencent.com/document/product/239/31934).

[](id:zjfb)
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configure** > **Add Replica** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/babd6ccfe0eb42326fda4e25101e50a4.png)
2. In the pop-up dialog box, adjust the configuration and click **OK**.
3. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.

#### Heavy write load
- **Cluster architecture**
Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configure** > **Add Shard** in the **Operation** column.
>?
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- When shards are added, the system will automatically balance the slot configuration and migrate data, which may fail. It is recommended to perform such operations during off-peak hours to avoid the impact of migration on business access.
>- Add shards as needed: each shard supports a QPS of 80,000 to 100,000.
>
![](https://qcloudimg.tencent-cloud.cn/raw/c9b06662d7f15daf5c7f1c89a4de54fd.png)

- **Standard architecture**
Upgrade the instance from standard architecture to cluster architecture to improve the processing power of CPU. Before the upgrade, you need to check the compatibility. For more information, see [Check on Migration from Standard Architecture to Cluster Architecture](https://intl.cloud.tencent.com/document/product/239/37594).
 1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance details page.
 2. In the **Specs Info** block, click **Upgrade Architecture**.
![](https://qcloudimg.tencent-cloud.cn/raw/52633dac2a97272cab593fc1eb306221.png)
 3. After the upgrade is completed, go to the instance list and select **Configure** > **Add Shard** in the **Operation** column.

>?If the problem persists, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
>
