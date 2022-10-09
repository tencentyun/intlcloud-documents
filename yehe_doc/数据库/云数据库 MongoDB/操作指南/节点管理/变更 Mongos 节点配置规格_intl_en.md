## Overview

Upgrading the computing specification of mongos nodes can increase the maximum number of connections to the database. You can adjust the mongos node specification appropriately based on the actual conditions of your business access.

## Notes

Upgrading the CPU performance and memory capacity of mongos nodes may involve cross-node data migration and cause a momentary disconnection. Therefore, before performing this operation, make sure that your business has an automatic reconnection mechanism. We recommend you complete this operation within the maintenance time during off-peak hours.

## Version requirements

TencentDB for MongoDB 4.0, 4.2 and 4.4 support adjusting the mongos node specification.

## Prerequisites

- Instance type: Sharded cluster instance.
- Instance status: Running.
- The CPU performance and memory capacity of the mongos nodes are insufficient and need to be upgraded.

## Directions

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Sharded Cluster Instance**.
3. Above the **Instance List** on the right, select the region.
4. In the **Instance List**, find the target instance.
5. Click the **Instance ID** to enter the **Instance Details** page and click the **Node Management** tab.
6. On the **Node Management** tab, click the **Mongos Node** tab.
7. On the **Mongos Node** tab, click **Modify Mongos Configuration**. In the pop-up window, configure the new specification.
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Instance ID/Name</td>
<td>The unique ID and name of the instance.</td></tr>
<tr>
<td>AZ</td>
<td>The AZ where the instance resides.</td></tr>
<tr>
<td>Mongos Quantity</td>
<td>The current number of mongos nodes.</td></tr>
<tr>
<td>Mongos Specs</td>
<td>Select the new mongos node specification in the drop-down list, which can be 1-core 2 GB MEM, 2-core 4 GB MEM, 4-core 8 GB MEM, 8-core 16 GB MEM, or 16-core 32 GB MEM.</td></tr>
<tr>
<td>Switch Time</td>
<td><ul><li>If you select <b>Upon modification completion</b>, the instance specification adjustment task will be executed immediately. Instance memory and capacity adjustment may involve node migration or primary-secondary switch. As the switch time point is uncontrollable, disconnection or restart may occur. </li><li>If you select <b>During maintenance time</b>, the task will be executed during the maintenance time. For more information, see <a href="https://intl.cloud.tencent.com/document/product/240/31190">Setting Instance Maintenance Time</a>.</li></ul></td></tr>
<tr>
<td>Configuration Change Fee</td>
<td>Fees after specification adjustment. In pay-as-you-go billing mode, fees are charged hourly by the new specification in three billing tiers.</td></tr>
<tr>
<td>Compare</td>
<td>You can compare the maximum number of connections before and after the mongos specification adjustment to assess whether the new specification meets your needs.</td></tr>
</tbody></table>
8. Click **OK**.

   
