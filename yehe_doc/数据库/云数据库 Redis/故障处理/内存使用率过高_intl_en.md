
## Error Description
- Symptom 1: you received an alarm about too high memory utilization.
- Symptom 2: the value of the memory utilization metric was high.
- Symptom 3: more keys were evicted and response latency increased.

## Possible Reasons
- Your business needs optimization.
- The current memory cannot meet the requirements of your business.

## Solutions
- Analyze the causes of high memory utilization and troubleshoot accordingly.
- Expand instance capacity in the console if the problem persists.

## Troubleshooting Procedure
### Expanding the capacity of a Memory Edition instance in standard architecture
>!
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- To expand the capacity of a Memory Edition instance in standard architecture, if the remaining available capacity of the physical machine is insufficient, a migration will occur, which will not affect your access to the instance. However, if the instance is running Redis 2.8, a flash disconnection will occur after the migration is completed, so we recommend that your business have a reconnection mechanism.
>- As the maximum capacity of a Memory Edition instance in standard architecture is 64 GB, you cannot expand its capacity to more than 64 GB.

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configure** > **Expand Node** in the **Operation** column.
2. In the pop-up dialog box, adjust the configuration and click **OK**.
3. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.

### Expanding the capacity of a Memory Edition instance in cluster architecture
>!
>- After the configuration is adjusted, the instance will be charged at the price of the new configuration.
>- When shards are added, the system will automatically balance the slot configuration and migrate data.
>- During capacity expansion and reduction, such blocking commands as `BLPOP`, `BRPOP`, `BRPOPLPUSH`, and `SUBSCRIBE` may fail once or more (which is related to the number of shards). Please assess the impact on your business before starting capacity expansion and reduction.
>

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis), locate the desired instance in the instance list, and select **Configure** > **Add Shard** or **Expand Node** in the **Operation** column.
2. In the pop-up dialog box, adjust the configuration and click **OK**.
3. Return to the instance list. After the status of the instance changes to "Running", the instance can be used normally.


>?If the problem persists, please [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category).
