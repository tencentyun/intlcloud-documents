## Overview

TencentDB for Redis is compatible with Redis 2.8, 4.0, and 5.0. Upgrade to a compatible version is supported, so that you can upgrade your instance to a newer version for more features.

## Upgrade Description
- Currently, only standard architecture instances can be upgraded to a compatible version, while cluster architecture instances cannot.
- Instances can be upgraded from an earlier version to a later one; for example, you can upgrade from Redis 2.8 to 4.0 or from 4.0 to 5.0.
- Cross-version upgrade is supported; for example, you can upgrade from Redis 2.8 to 5.0.
- If an instance is upgraded to a compatible version, no billing changes will be caused.
- Downgrade to a compatible version is not supported.

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

## Directions

1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Click the instance ID to enter the **Instance Details** page.
5. In the **Specs Info** section on the **Instance Details** page, click **Upgrade Version** after **Compatible Version**.
![](https://main.qcloudimg.com/raw/ebc4ecc50af95d99be2fa23f45d11278.png)
6. In the pop-up window, confirm the information of the target instance according to the following table, configure the target version, and click **OK**.
<img src="https://main.qcloudimg.com/raw/f584ccc7b3004feb662e72e8ddcf819a.png" style="zoom:90%;" />
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
7. Return to the instance list. After the **Instance Status** changes to **Running**, you can see that the instance version has been upgraded in the instance list or instance details.

## Related APIs

| API | Description |
| :----------------------------------------------------------- | :----------- |
| [UpgradeInstanceVersion](https://intl.cloud.tencent.com/document/product/239/37831) | Upgrades instance version |

