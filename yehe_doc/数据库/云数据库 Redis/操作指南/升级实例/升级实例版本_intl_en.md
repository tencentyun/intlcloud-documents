## Overview
TencentDB for Redis is compatible with Redis 2.8, 4.0, 5.0 and 6.0. Upgrade to a compatible version and minor version upgrade are supported, so that you can upgrade your instance to a newer version for more features.

## Version Differences

| Compatible Version | Minor Version | Optimizations and Fixes |
| --------- | ------ | ------------------------------------------------------------ |
| Redis 4.0 | 4.3.0 | <li>When a failed replica node is discovered in the cluster, messages can be sent to the cluster, making it quicker to locate faulty nodes. </li><li>Performance optimization: `zmalloc_get_rss()` is executed in the BIO thread to avoid blocking the main thread and increasing the request latency. </li><li>Fixed the issue where the `rdbLoadRio()` function might trigger a crash in some cases.</li> |
| Redis 5.0 | 5.2.0  | <li>Performance optimization: `zmalloc_get_rss()` is executed in the BIO thread to avoid blocking the main thread and increasing the request latency. </li></li><li>Fixed the issue where the `rdbLoadRio()` function might trigger a crash in some cases.</li> |
| Redis 6.0 | 6.0.0  | Compatible with Redis version 6.0. |
## Upgrade Description
- Currently, only standard architecture instances can be upgraded to a compatible version, while cluster architecture instances cannot.
- Instances can be upgraded from an earlier version to a later one; for example, you can upgrade from Redis 4.0 to 5.0.
- Cross-version upgrade is supported.
- If an instance is upgraded to a compatible version, no billing changes will be caused.
- Downgrade to a compatible version is not supported.
- During minor version upgrade, the system automatically detects the minor version, and you cannot select a target version.
- As the version release time varies by region, the minor version release status is as displayed in the console.

## How Upgrade Works
![](https://qcloudimg.tencent-cloud.cn/raw/3ed834421c6dffe404f55ed82dd44bb1.png)
1. Apply for resources: Apply for the resources of the new instance version, including proxy, Redis master node, and Redis replica node resources.
2. Sync the data: Sync the full and incremental data from the instance on the old version to the instance on the new version.
3. Wait for the switch: Wait until data sync is completed or wait for the switch time.
4. Switch the version: When the switch conditions are met (data sync is almost completed, and the requirements for the switch time are met), stop writing data into the old instance, unbind the virtual IP (VIP) address from it, and bind the VIP to the new instance.
5. Complete the upgrade: Update the instance status.

## Impact of Upgrade
The version upgrade process mainly consists of data sync and instance switch:
- During data sync, the service will not be affected.
- During switch, the instances will become read-only for less than one minute (to wait for the data sync completion), and a momentary disconnection (within seconds) will occur; therefore, your business should have an automatic reconnection mechanism.

## Preparations for Upgrade
- The instance to be upgraded is in **Running** status and is not executing any tasks.
- The target version is confirmed.

## Upgrading Version
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Click the instance ID to enter the **Instance Details** page.
5. In the **Specs Info** section on the **Instance Details** page, click **Upgrade Version** after **Compatible Version**.
<img src="https://main.qcloudimg.com/raw/ebc4ecc50af95d99be2fa23f45d11278.png" style="zoom:67%;" />
6. In the pop-up window, confirm the information of the target instance according to the following table, configure the target version, and click **OK**.
<img src="https://main.qcloudimg.com/raw/f584ccc7b3004feb662e72e8ddcf819a.png" style="zoom:67%;" />
<table>
<thead>
<tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Instance ID</td><td>ID of the instance to be upgraded.</td></tr>
<tr>
<td>Instance Name</td><td>Name of the instance to be upgraded.</td></tr>
<tr>
<td>Compatible Version</td><td>The current compatible Redis version of the instance to be upgraded.</td></tr>
<tr>
<td>Architecture</td>
<td>Architecture information of the instance to be upgraded. Currently, version upgrade is supported only for standard architecture instances.</td></tr>
<tr>
<td>Memory</td><td>Memory size of the instance to be upgraded.</td></tr>
<tr>
<td>Upgrade Version</td>
<td>Select the target version in the drop-down list. You can upgrade from an earlier version to a later version or across versions.</td></tr>
<tr>
<td>Preview New Specs</td><td>Preview information of the instance specifications after upgrade.</td></tr>
<tr>
<td>Switch Time</td>
<td><ul><li><strong>Switch Now</strong>: The switch will be performed when the data sync is almost completed (the data left to be synced is less than 10 MB). </li><li><strong>Switch in Maintenance Time</strong>: The switch will be performed during the instance maintenance time. If the switch conditions cannot be met in the current maintenance time, the switch will be attempted in the next maintenance time. You can modify the <strong>Maintenance Time</strong> on the instance details page.</li></ul></td></tr>
<tr>
<td>Total Fees</td><td>Fees after instance upgrade. No billing changes will be caused.</td></tr>
</tbody></table>
7. On the left sidebar, select **Task Management**, wait for the task to complete, and you can see that the version of the instance has been upgraded in the instance list.

## Upgrading Minor Version
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Click the instance ID to enter the **Instance Details** page.
5. In the **Specs Info** section on the **Instance Details** page, click **Upgrade Minor Version** after **Compatible Version**.
> !The system automatically detects the minor version. If the **Upgrade Minor Version** button is grayed out, the instance is already on the latest minor version.
> 
<img src="https://qcloudimg.tencent-cloud.cn/raw/3872d68e11922de0c3c911c0a1696305.png" />
6. In the **Upgrade Minor Version** window, confirm the instance information and the target version and select the upgrade time in **Switch Time**.
   - **Switch Now**: The switch will be performed when the data sync is almost completed (the data left to be synced is less than 10 MB).
   - **Switch in Maintenance Time**: The switch will be performed during the instance maintenance time. If the switch conditions cannot be met in the current maintenance time, the switch will be attempted in the next maintenance time. You can modify the **Maintenance Window** on the instance details page.
7. On the left sidebar, select **Task Management**, wait for the task to complete, and you can see that the minor version of the instance has been upgraded in the instance list.

## Related APIs

| API | Description |
| :----------------------------------------------------------- | :------------- |
| [UpgradeInstanceVersion](https://intl.cloud.tencent.com/document/product/239/37831) | Upgrades instance version |
| [UpgradeSmallVersion](https://cloud.tencent.com/document/product/239/74596) | Upgrades instance minor version |

