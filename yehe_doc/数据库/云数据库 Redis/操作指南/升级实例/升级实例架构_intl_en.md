## Overview

TencentDB for Redis supports standard architecture and cluster architecture. To help you process ever-growing business data, it allows you to upgrade from standard architecture to cluster architecture if the performance and capacity of standard architecture are insufficient.

## Upgrade Description
- For Redis 4.0 or later, a standard architecture instance can be upgraded to a cluster architecture instance on the same version; for example, you can upgrade from Redis 4.0 Standard Architecture to Redis 4.0 Cluster Architecture.
- Cross-version architecture upgrade is not supported; for example, you cannot upgrade from Redis 4.0 Standard Architecture to Redis 5.0 Cluster Architecture.
- The architecture of Redis 2.8 cannot be upgraded.
- Cluster architecture cannot be downgraded to standard architecture.
- After standard architecture is upgraded to cluster architecture, fees will be charged based on cluster architecture and thus get increased. For more information, see [Pricing](https://intl.cloud.tencent.com/document/product/239/9894).

## How Upgrade Works
- Redis standard architecture can be directly upgraded to cluster architecture (single shard) within three minutes with no data migration required.
- In Redis 4.0 or later, if standard architecture is upgraded to cluster architecture, only the runtime mode of the instance will change from having no slot limit to having one, but no data migration will occur.

## Upgrade Preparations (Compatibility Check)
To avoid business failures caused by compatibility problems during migration to cluster architecture, check the compatibility before the upgrade:
- Cluster architecture stores data in a distributed manner, and its biggest difference from standard architecture lies in whether a single command supports multikey access. For the cluster architecture, commands can be categorized into supported, partially supported, and unsupported. For the complete list of compatible commands, see [Command Compatibility](https://intl.cloud.tencent.com/document/product/239/31958).
- For more information about compatibility check, see [Check on Migration from Standard Architecture to Cluster Architecture](https://intl.cloud.tencent.com/document/product/239/37594).

## Impact of Upgrade
- Generally, upgrade can be completed in three minutes.
- During the upgrade, existing connections will be closed momentarily; therefore, your business should have a reconnection mechanism.

## Directions
1. Log in to the [TencentDB for Redis console](https://console.cloud.tencent.com/redis).
2. Above the instance list on the right, select the region.
3. In the instance list, find the target instance.
4. Click the instance ID to enter the **Instance Details** page.
5. In the **Specs Info** section on the **Instance Details** page, click **Upgrade Architecture** after **Architecture**.
![](https://qcloudimg.tencent-cloud.cn/raw/60f5d87ba5562d96bdff3a81be60b31a.png)
6. In the pop-up window, configure the upgrade parameters according to the table below.
![](https://qcloudimg.tencent-cloud.cn/raw/1eae7138afd9efc438c409ab881d20bd.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Instance ID</td>
<td>ID of the instance to be upgraded.</td></tr>
<tr>
<td>Instance Name</td><td>Name of the instance to be upgraded.</td></tr>
<tr>
<td>Compatible Version</td><td>The current compatible Redis version of the instance to be upgraded.</td></tr>
<tr>
<td>Architecture</td>
<td>Architecture information of the instance to be upgraded. Currently, the standard architecture can be upgraded to the cluster architecture, but the cluster architecture cannot be downgraded to the standard architecture.</td></tr>
<tr>
<td>Memory</td><td>Memory size of the instance to be upgraded.</td></tr>
<tr>
<td>Target Architecture</td><td>Select the target architecture in the drop-down list.</td></tr>
<tr>
<td>Preview New Specs</td><td>Preview information of the instance specifications after upgrade.</td></tr>
<tr>
<td>Switch Time</td>
<td><ul><li>Switch Now: The switch will be performed immediately. </li><li>Switch in Maintenance Time: The switch will be performed during the instance maintenance time. You can modify the <strong>Maintenance Time</strong> on the instance details page.</li></ul></td></tr>
<tr>
<td>Total Fees</td>
<td>Fees after architecture upgrade.<ul><li> <strong>Pay-as-you-go</strong>: Hourly unit price after instance architecture upgrade. You can click <strong>Billing Details</strong> to view the billable items and billing formula and confirm the fees.</li> </ul></td></tr>
</tbody></table> 

7. There is a command compatibility risk when upgrading to the cluster architecture edition. Click **Compatibility Description Document**, confirm the compatibility risk, and click **OK** to proceed with the upgrade.
8. Make the payment and return to the instance list. After the **Instance Status** changes to **Running**, you can see that the instance architecture has been upgraded to cluster architecture in the instance list or instance details.

## Related APIs

| API | Description |
| :----------------------------------------------------------- | :--------------- |
| [UpgradeInstanceVersion](https://intl.cloud.tencent.com/document/product/239/37831) | Upgrades instance architecture |

