## Overview

You can add more mongos nodes to increase the maximum number of connections to the database instance.

## Version requirements

Currently, sharded cluster instances on v4.0, v4.2 and v4.4 support adding mongos nodes.

## Notes

After you add a mongos node, the system will automatically bind an IP address to it and enable the connection string for mongos access. Then, you can directly copy the connection string in the **Network** section on the **Instance Details** page.

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
7. On the **Mongos Node** tab, click **Add Mongos Node**
 - **The instance nodes are in the same AZ:**
![](https://qcloudimg.tencent-cloud.cn/raw/29b9e1265c34bc6dcffa69eae5f9c1e5.png)
 - **The instance nodes are in different AZs:**
![](https://qcloudimg.tencent-cloud.cn/raw/f9c1cb193845eb81f70b32fda0c13de3.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Instance ID/Name</td>
<td>The unique ID and name of the instance.</td></tr>
<tr>
<td>AZ</td>
<td>The AZ where the instance resides. This parameter will be displayed if the instance nodes are in the same AZ.</td></tr>
<tr>
<td>Mongos Quantity</td>
<td>The current number of mongos nodes configured for the instance. This parameter will be displayed if the instance nodes are in the same AZ.</td></tr>
<tr>
<td>Mongos Specs</td>
<td>Specification of mongos nodes, including the number of CPU cores, memory, and maximum number of connections.</td></tr>
<tr>
<td>Add Mongos Node</td>
<td>Select the number of mongos nodes to be added. An instance can have up to 48 mongos nodes.</td></tr>
<tr>
<td>Total Fees</td>
<td>Fees after specification adjustment. <ul><li>In pay-as-you-go billing mode, fees are charged hourly by the new specification in three billing tiers.</li></ul></td></tr>
<tr>
<td>Compare</td>
<td>You can compare the specification, number of nodes in the AZ, and maximum numbers of connections before and after mongos nodes are added to assess whether the new specification meets your needs.</td></tr>
</tbody></table>
8. After confirming that everything is correct, click **OK**.


