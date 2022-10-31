## Overview
Minor versions of the TencentDB for Redis proxy are released from time to time to add more database features or fix known bugs.

<table>
<thead><tr><th width=15%>Proxy Version</th><th width=15%>Proxy Minor Version</th><th width=70%>New Feature, Optimization, or Fix</th></tr></thead>
<tbody><tr>
<tr><td rowspan=5>Proxy 5.0</td>
<td>5.6.0</td><td><ul><li>Supported `wait` commands in Cluster Architecture instances.</li><li>Supported SSL encryption to implement encrypted data transfer.</li></ul></td></tr>
<tr>
<td>5.5.0</td>
<td><ul><li> Supported `wait` commands in Cluster Architecture instances. </li><li>Supported the “Read Local Nodes Only” feature.</li><li>Supported the `dbsize` command in Cluster Edition instances to return the number of keys in all shards.</li><li>Supported displaying the client port information in slow logs.</li><li>Supported `flushall` and `flushdb` commands, which can be distributed to the master node of all shards in a Cluster Architecture instance while retaining data in nodes with the specified `nodeid`.</li><li>Supported monitoring the number of big value requests.</li><li>Supported the `Scan` command in Cluster Edition instances to traverse all shards.</li><li>Fixed the issue where "ERR unknown command 'select' command" might be returned when the `select` command was executed after a transaction.</li><li>Fixed the issue where the command was sent to an incorrect node and the `Move` error was reported when the locked connection wasn't released in time as the `watch+` transaction was used in the pipeline scenario.</li></ul></td></tr>    
<tr>
<td>5.4.0</td><td>Optimized the statistics collection policies of P99 monitoring metrics, including metrics for all Redis commands.</td></tr>
<tr>
<td>5.2.0</td><td>Supported the five-second granularity for monitoring data.</td></tr>
<tr>
<td>5.1.0</td><td><li>Supported the `keys` command in Cluster Architecture instances.</li><li>Supported displaying the client address in slow logs.</li><li>Fixed the "ERR MULTI calls can‘t be nested" error.</li></ul></td></tr>    
<tr>
<td>5.0.0</td><td>Supported `unlink` and `exists` commands in Cluster Architecture instances.</td></tr>
<tr>
<td rowspan=3>Proxy 4.0</td> 
<td>3.5.0</td><td>Supported the command analysis feature. You can view information such as QPS, P99 execution latency, average execution latency, and max execution latency of individual commands.</td></tr>
<tr>
<td>3.3.0</td><td>Supported the five-second granularity for system monitoring data collection.</td></tr>
<tr>
<tr><td>3.2.0</td><td><li>Supported displaying the client address in slow logs.</li><li>Fixed the "ERR MULTI calls can’t be nested" error.</li></td></tr>    
</tbody></table>

## Notes on Upgrade
- The system automatically detects the minor version of the proxy. If the **Upgrade Proxy** button is grayed out, the instance proxy is already on the latest minor version.
- As the version release time varies by region, the minor version release status is as displayed in the console.

## Upgrade Impact
The version upgrade process mainly consists of data sync and instance switch:
- During data sync, the service will not be affected.
- During switch, the instances will become read-only for less than 1 minute (to wait for the completion of data sync), and a momentary disconnection (within seconds) will occur; therefore, your business should have an automatic reconnection mechanism.

## Preparations for Upgrade
- The instance to be upgraded is in **Running** status and is not executing any tasks.
- We recommend that you perform upgrade in the maintenance time during off-peak hours.

## Upgrade Directions
1. Log in to the [Redis Console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Click the target instance ID to enter the **Instance Details** page.
5. In the **Specs Info** section on the **Instance Details** page, click **Upgrade Proxy** after **Proxy Version**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c9f1d31f6687c96115af9cbda957fc2c.png"  style="zoom:70%;">
6. In the pop-up window, confirm the information of the target instance based on the following table, configure the target version, and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9dce36bc5cc603e415e7211951920859.png"  style="zoom:50%;">
<table>
<thead><tr><th >Parameter</th><th >Description</th></tr></thead>
<tbody>
<tr>
<td>Instance ID</td><td>ID of the instance to be upgraded.</td></tr>
<tr>
<td>Current Version</td><td>Current minor version of the proxy.</td></tr>
<tr>
<td>Target Version</td><td>Target version after proxy upgrade. The target version cannot be selected.</td></tr>
<tr>
<td>Switch Time</td>
<td><ul><li><strong>Switch Now</strong>: The switch will be performed when the data sync is almost completed (the data left to be synced is less than 10 MB). </li><li><strong>Switch in Maintenance Time</strong>: The switch will be performed during the instance maintenance time. If the switch conditions cannot be met in the current maintenance time, the switch will be attempted in the next maintenance time. You can modify the <strong>Maintenance Time</strong> on the instance details page.</li></ul></td></tr>
</tbody></table>
7. Return to the instance list. After the **Instance Status** changes to **Running**, you can see that the instance version has been upgraded in the instance list or instance details.

## Related APIs

| API | Description |
| :----------------------------------------------------------- | :----------- |
| [UpgradeProxyVersion](https://intl.cloud.tencent.com/document/product/239/47724) | Upgrades proxy version |

