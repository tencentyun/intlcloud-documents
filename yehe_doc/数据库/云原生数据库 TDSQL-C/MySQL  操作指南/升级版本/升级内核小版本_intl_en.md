TDSQL-C for MySQL supports automatic or manual kernel minor version upgrade. Upgrading adds new features, improves performance, and fixes issues.
For more information on the TDSQL-C for MySQL kernel minor version, see [Kernel Version Release Notes](https://intl.cloud.tencent.com/document/product/1098/44587).

## Overview
- **Automatic upgrade**:
 - Scenario 1: when a severe bug or security vulnerability occurs in TDSQL-C for MySQL, the system will perform database kernel minor version upgrade during the maintenance window and send upgrade notifications through the Message Center and SMS.
 - Scenario 2: when a TDSQL-C for MySQL cluster is migrated due to cluster configuration upgrade/downgrade, storage capacity expansion/reduction, or database version upgrade, etc., the system will automatically upgrade the cluster's kernel to the latest minor version.
- **Manual upgrade**:
You can also manually upgrade kernel minor version in the console.

## Upgrade Rules
- To ensure database replication consistency, the kernel minor versions of all associated instances (read-write and read-only instances) in the cluster will also be upgraded.
- TDSQL-C for MySQL upgrade involves data migration. The time it takes for migration depends on the data size. Your business will not be affected during the upgrade and can be accessed as per usual.

## Notes
- Cluster switch may be needed after version upgrade is completed (that is, the database may be disconnected for seconds). We recommend you use applications configured with auto reconnection feature and conduct the switch during the instance maintenance window.
- If the number of tables in a single instance exceeds one million, upgrade may fail and database monitoring may be affected. Make sure that the number of tables in a single instance is below one million.
- The kernel minor version cannot be downgraded once upgraded.

## Directions
1. Log in to the [TDSQL-C console](https://console.cloud.tencent.com/cynosdb) and click a cluster name in the cluster list or **Manage** in the **Operation** column to enter the cluster details page.
2. On the cluster details page, click **Upgrade** after **Database Version** in the **Configuration Info** section.
![](https://qcloudimg.tencent-cloud.cn/raw/08679ee2ac0cfa9afe1ca51c107dd86a.png)
3. In the pop-up window, select the switch time, indicate your consent, and click **OK**.
>!As database upgrade involves data migration, after the upgrade is completed, a momentary disconnection from the database lasting for just seconds may occur. We recommend you select **During maintenance time** as the switch time, so that the switch will be initiated within the next maintenance time after the instance upgrade is completed.
>
![](https://qcloudimg.tencent-cloud.cn/raw/c6b3523586d21d68d3938900d061714a.png)

