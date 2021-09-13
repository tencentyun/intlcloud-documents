
## Error Description
- Symptom 1: you received an alarm about high CPU utilization.
- Symptom 2: the value of the CPU utilization metric was high.
- Symptom 3: the overall throughput became lower and the response slower.

## Possible Reasons
- Commands with high time complexity
- High load, such as frequent access to hot keys
- Connections that are established frequently
- Exceptional access

## Solutions
1. [Optimize your business](#ywyh)
 1. Go to the **System Monitoring** tab in the TencentDB for Redis console to check whether QPS (Queries per Second) is high and whether there are unexpected hot keys.
 2. Optimize your business logic after troubleshooting exceptional access. For example, optimize commands with high time complexity, hot keys, and non-persistent connections, or disable AOF (Append Only File). If the problem persists, upgrade the instance.

2. [Upgrade the instance](#slsj)
 - If the read load is heavy, you can add replicas to share the read load. Please confirm that your business allows inconsistent data before enabling read/write separation, because after it is enabled, inconsistent data may be read from the replica node and the master node (the replica node lags behind the master node).
 - If the write load is heavy, you can upgrade the instance from standard architecture to cluster architecture to improve the processing power of CPU. Before the upgrade, you need to check the compatibility. For more information, see [Check on Migration from Standard Architecture to Cluster Architecture] (https://intl.cloud.tencent.com/document/product/239/37594).

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
>!Please confirm that your business allows inconsistent data before enabling read/write separation, because after it is enabled, inconsistent data may be read from the replica node and the master node (the replica node lags behind the master node). For more information, see [Changing Instance Specification](https://intl.cloud.tencent.com/document/product/239/31934).

[](id:zjfb)
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configure** > **Add Replica** in the **Operation** column.
![](https://main.qcloudimg.com/raw/53a2005cd6050ee2bbcdb32b4b64e48d.png)
2. In the pop-up dialog box, adjust the configuration and click **OK**.
3. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.

#### Heavy write load
- **Cluster architecture**
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configure** > **Add Shard** in the **Operation** column.
>?
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- When shards are added, the system will automatically balance the slot configuration and migrate data, which may fail. It is recommended to perform such operations during off-peak hours to avoid the impact of migration on business access.
>- Add shards as needed: each shard supports a QPS of 80,000 to 100,000.
>

- **Standard architecture**
Upgrade the instance from standard architecture to cluster architecture to improve the processing power of CPU. Before the upgrade, you need to check the compatibility. For more information, see [Check on Migration from Standard Architecture to Cluster Architecture] (https://intl.cloud.tencent.com/document/product/239/37594).
 1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance details page.
 2. In the **Specs Info** block, click **Upgrade Architecture**.
![](https://main.qcloudimg.com/raw/03fc7dc818b3a893c904f8d15d61c3c6.png)
 3. After the upgrade is completed, go to the instance list and select **Configure** > **Add Shard** in the **Operation** column.
