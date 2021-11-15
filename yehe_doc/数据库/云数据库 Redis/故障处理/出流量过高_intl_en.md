
## Error Description
- Symptom 1: you received an alarm about the outbound traffic being restricted because the outbound traffic metric reached the maximum value allowed.
- Symptom 2: the response latency increased.

## Possible Reasons
The reasons are as follows:
- Big keys
- Insufficient instance configuration

## Solutions
1. Adjust the bandwidth of the instance in the TencentDB for Redis console to alleviate the problem.
2. Check and optimize big keys in the following ways:
 - Split big keys.
 - Have less access to big keys as long as your business won't be affected.
 - Delete useless big keys.
3. If the bandwidth upper limit problem persists after optimization, upgrade the instance to improve its ability to handle more traffic. 

## Troubleshooting Procedure
### Step 1. Adjust the bandwidth
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance details page.
2. Adjust the bandwidth in the **Network Info** block (the additional bandwidth is currently free of charge).
>?
>- Increasing bandwidth has no impact on your business. However, if the bandwidth is decreased, the traffic which exceeds the bandwidth may be restricted.
>- Standard bandwidth: it is the bandwidth per (master or replica) node in the instance.
>- Read-Only replica bandwidth: each read-only replica has the same bandwidth as that of the master.
>- Additional bandwidth: if the standard bandwidth cannot meet your needs, you can add additional bandwidth.
>- Total instance bandwidth = additional bandwidth * the number of shards + standard bandwidth * the number of shards * the number of replicas. (There is one shard in standard architecture. If the instance has no replica, the number of replica in this formula is one.)
>
![](https://main.qcloudimg.com/raw/00c7d78cc03dabf405ffff8fbc40eae5.png)

### Step 2. Optimize big keys
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), click an instance ID in the instance list, and enter the instance management page.
2. On the **System Monitoring** tab, view the key size distribution chart and optimize big keys in the following ways:
 - Split big keys.
 - Have less access to big keys as long as your business won't be affected.
 - Delete useless big keys.

If the bandwidth upper limit problem persists, go to [Step 3. Upgrade the instance](#sjsl).

### [Step 3. Upgrade the instance](id:sjsl)
#### Upgrading a Memory Edition instance in standard architecture
>!
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- To expand the capacity of a Memory Edition instance in standard architecture, if the remaining available capacity of the physical machine is insufficient, a migration will occur, which will not affect your access to the instance. However, if the instance is running Redis 2.8, a flash disconnection will occur after the migration is completed, so we recommend that your business have a reconnection mechanism.
>- As the maximum capacity of a Memory Edition instance in standard architecture is 64 GB, you cannot expand its capacity to more than 64 GB.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configure** > **Expand Node** or **Add Replica** in the **Operation** column.
![](https://main.qcloudimg.com/raw/d4dbc95ee670595149c7609f03d8d92f.png)
2. In the pop-up dialog box, adjust the configuration and click **OK**.
3. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.

#### Upgrading a Memory Edition instance in cluster architecture
>!
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- When shards are added, the system will automatically balance the slot configuration and migrate data.
>- During capacity expansion and reduction, such blocking commands as `BLPOP`, `BRPOP`, `BRPOPLPUSH`, and `SUBSCRIBE` may fail once or more (which is related to the number of shards). Please assess the impact on your business before starting capacity expansion and reduction.
>

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configure** > **Add Shard**, **Expand Node**, or **Add Replica** in the **Operation** column.
![](https://main.qcloudimg.com/raw/9c24103c52a67fbcd463e6f359ab0369.png)
2. In the pop-up dialog box, adjust the configuration and click **OK**.
3. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.

