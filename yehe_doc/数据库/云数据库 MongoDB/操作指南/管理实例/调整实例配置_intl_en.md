TencentDB for MongoDB provides flexible scaling operations. You can adjust the configuration of the current instance to make it better meet your business requirements.

## Background
- If the configuration of your purchased TencentDB for MongoDB instance isn't suitable for (either below or above) your current business requirements, you can quickly adjust its specifications according to your actual business conditions (at the initial stage, at the rapid development stage, during peak hours, or during off-peak hours), so as to better meet your needs such as full utilization of resources and real-time cost optimization.

- The default architecture of each replica set cluster is one-primary-two-secondary. If the number of your purchased cluster nodes isn't suitable for (either below or above) your current business requirements, you can promptly adjust the number of nodes according to your actual business conditions to better meet your business requirements.

- Each shard in a sharded cluster is a replica set, and each replica set consists of one primary node and one or more secondary nodes. If the number of shards in your purchased sharded cluster isn't sufficient to meet your business requirements such as video live streaming, flash sales, and promotion campaigns, you can add more shards as needed.

## Version Description
- Currently, TencentDB for MongoDB 4.2, 4.0, 3.6, and 3.2 support adjusting the instance capacity specification.
- TencentDB for MongoDB 4.2 replica set instances don't support adjusting the number of instance nodes.
- TencentDB for MongoDB 4.2 sharded instances don't support adjusting the number of nodes per shard and the number of shards.

## Billing Description
After the instance configuration is adjusted, the instance will be billed by the new configuration. Make sure that your Tencent Cloud account balance is sufficient. For more information, see [Configuration Adjustment Billing](https://intl.cloud.tencent.com/document/product/240/44174).

## Notes
1. You can adjust the configuration only when there are no tasks being executed in the instance.
2. During configuration adjustment, there may be one or two momentary disconnections for around 10s each. We recommend you configure an automatic reconnection feature for your application.
3. Data migration may be involved in configuration adjustment. During data migration, the instance can be accessed normally.
4. You cannot cancel an ongoing configuration adjustment operation.
5. There may be a short request delay during configuration adjustment; therefore, set an appropriate business timeout period.

## Notes
1. During configuration adjustment, we recommend you also adjust the oplog capacity, which must be at least 10% of the total node capacity. If it is too small, oplogs will be easily flushed, which will affect the rollback feature.
2. During instance downgrade, the oplog capacity will be reset to 10% of the new storage capacity.
3. The name, private network address, and port of the instance remain unchanged after configuration adjustment.
4. After new nodes are added to the cluster, data sync will start without affecting the business.
5. Currently, shards can be only added but not removed for sharded instances. After new shards are added to the cluster, data sync will start without affecting the business.

## Prerequisites
- You have [applied for a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- If your instance is pay-as-you-go, make sure that your Tencent Cloud account balance is sufficient.
- The instance and its associated instances are in **Running** status and are not executing any tasks.

## Directions
### Adjusting capacity
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **Adjust Configuration** in the **Adjust Configuration** drop-down list.
6. On the **Adjust Configuration** page, you can adjust the node specification, node capacity, and oplog capacity.
7. In the **Switch Time** option, select the specific time for instance specification switch.
   - If you select **Upon modification completion**, the instance specification adjustment task will be executed immediately.
   - If you select **Maintenance time**, the instance specification switch task will be executed during the maintenance time.
>!We recommend you set the **maintenance time** to be within off-peak hours of your business, and you need to regularly maintain your instance. If you select **Upon modification completion**, the instance configuration will be adjusted immediately, which may involve node migration or primary-secondary switch. As the switch time point is uncontrollable, we strongly recommend you make the instance configuration executed within the **maintenance time**. For more information, see [Set Instance Maintenance Time](https://intl.cloud.tencent.com/document/product/240/31190).
8. You can click **Billing Details** to view billable items and billing formula and confirm the **fees**.
9. After confirming that everything is correct, click **Submit**.

### Adjusting node quantity
#### Adjusting node quantity (replica set instance)
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance**.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **Adjust Configuration** > **Adjust Node Quantity**.
6. In the **Adjust Node Quantity** window, read the notes on node quantity adjustment carefully.
7. In the **Node Quantity** input box, select the desired numbers of primary and secondary nodes as detailed below:
   - **3**: downgrade is not supported.
   - **5**: downgrade to **3** nodes is supported.
   - **7**: downgrade to **3** or **5** nodes is supported.
8. Confirm the fees and click **OK**.

#### Adjusting node quantity per shard (for sharded instance)
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Sharded Instance**.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **Adjust Configuration** > **Adjust Node Quantity per Shard**.
6. In the **Adjust Node Quantity per Shard** window, read the notes on node quantity adjustment carefully.
7. In the **Node Quantity** input box, select the desired numbers of primary and secondary nodes as detailed below:
   - **3**: downgrade is not supported.
   - **5**: downgrade to **3** nodes is supported.
   - **7**: downgrade to **3** or **5** nodes is supported.
8. Confirm the fees and click **OK**.

### Adjusting shard quantity (for sharded instance)
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Sharded Instance**.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Operation** column of the target instance, select **Adjust Configuration** > **Adjust Shard Quantity**.
6. In the **Adjust Shard Quantity** window, read the notes on shard quantity adjustment carefully.
7. In the **Shard Quantity** input box, select the number of shards, which can be 2–19.
8. You can click **Billing Details** to view billable items and billing formula and confirm the **fees**.
9. After confirming that everything is correct, click **Submit**.

## API
| API Name                                                  | Feature Description      |
| ------------------------------------------------------------ | -------------------- |
| [ModifyDBInstanceSpec](https://intl.cloud.tencent.com/document/product/240/34699) | Adjusts TencentDB instance configuration. |

