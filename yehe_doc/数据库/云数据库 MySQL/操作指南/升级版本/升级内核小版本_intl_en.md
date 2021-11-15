TencentDB for MySQL supports automatic or manual kernel minor version upgrade. Upgrading adds new features, improves performance, and fixes issues.
For details on the TencentDB for MySQL kernel minor version, please see [Kernel Version Updates](https://intl.cloud.tencent.com/document/product/236/35989).

>?Currently, basic single-node instances do not support kernel minor version upgrade.

## Overview
- **Automatic upgrade**:
 - Scenario 1: when a severe bug or security vulnerability occurs in TencentDB for MySQL, the system will perform database kernel minor version upgrade during the maintenance window and send upgrade notifications through the console Message Center and SMS.
 - Scenario 2: when a TencentDB for MySQL instance is migrated due to instance configuration upgrade/downgrade, storage capacity expansion/reduction, or database version upgrade, etc., the system will automatically upgrade the instance’s kernel to the latest minor version.
- **Manual upgrade**:
You can also manually upgrade kernel minor version in the console.


## Upgrade Rules
- If an instance to be upgraded is associated with other instances (e.g., source instance and read-only replicas), these instances will be upgraded together to ensure data consistency.
- TencentDB for MySQL upgrade involves data migration. The time it takes to migrate an instance depends on the size of the instance’s data. Your business will not be affected during the upgrade and can be accessed as per usual.

## Notes
- Instance switchover may be needed after version upgrade is completed (i.e., the MySQL instance may be disconnected for a few seconds). We recommend that applications be configured with auto reconnection feature and that instance switchover be conducted during the instance maintenance window. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).
- If the number of tables in a single instance exceeds one million, upgrade may fail and database monitoring may be affected. Please make sure the number of tables in a single instance is no more than one million.
- The kernel minor version cannot be downgraded once upgraded.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb) and click the instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. In the **Configuration Info** section, click **Upgrade Kernel Minor Version**.
![](https://main.qcloudimg.com/raw/3fda3cffc784b3cde619e698d728d486.png)
3. In the pop-up dialog box, select the switch time and click **Upgrade**.
>!As database upgrading involves data migration, after the upgrade is completed, a very short disconnection from the MySQL database lasting for just seconds may occur. We recommend that you select **During maintenance window** as the switch time, so that the switch will be initiated within the next maintenance time after the instance upgrade is completed.
>
![](https://main.qcloudimg.com/raw/19d059cb26a22b9ae8c173daae8590e8.png)

