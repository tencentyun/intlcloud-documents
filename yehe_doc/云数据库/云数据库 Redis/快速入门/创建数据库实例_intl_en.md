## Operation Scenarios
This document describes how to create an instance in the TencentDB for Redis Console.

## Directions
### Creating an instance
1. Log in to the [TencentDB for Redis Console](https://console.cloud.tencent.com/redis) and select **Instance List** on the left sidebar.
2. Click **Create Instance** and enter the parameters as required.
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Remarks</th>
</tr>
</thead>
<tbody><tr>
<td>Billing Mode</td>
<td>Pay-as-you-go billing is supported.</td>
</tr>
<tr>
<td>Network Type</td>
<td>The basic network and VPC cannot communicate with each other. You cannot change the network type after purchase. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/213/5227" target="_blank">Network Environment</a>.</td>
</tr>
<tr>
<td>Engine</td>
<td>The Redis Community Edition is supported.</td>
</tr>
<tr>
<td>Compatible Version</td>
<td>It is compatible with Redis 2.8 and Redis 4.0.</td>
</tr>
<tr>
<td>Replica Count</td>
<td><ul><li>Redis 2.8 Standard Edition supports 0–1 replica. </li><li>Redis 4.0/5.0 Standard Edition supports 1–5 replicas. </li><li>Redis 4.0/5.0 Cluster Edition supports 1–5 replicas.</li></td>
</tr>
<tr>
<td>Port</td>
<td>The custom port number needs to be between 1024 and 65535</td>
</tr>
<tr>
<td>Specify Project/Security Group</td>
<td>Specify the project and security group for the database.</td>
</tr>
<tr>
<td>Instance Name/Set Password</td>
<td>You can directly set the instance name and password here or set them in the instance list after creation.</td>
</tr>
</tbody></table>
3. After confirming that everything is correct, click **Buy Now**. For detailed pricing of each edition, please see [Product Pricing](https://intl.cloud.tencent.com/document/product/239/9894).
4. Return to the instance list. After the status of the instance is displayed as **Running**, it can be used normally.

### Renaming an instance
In the **Instance ID / Name** column in the instance list, click the small icon below to rename the instance.
![](https://main.qcloudimg.com/raw/8a6917c05adb4e06731dbdd836c620da.png)
