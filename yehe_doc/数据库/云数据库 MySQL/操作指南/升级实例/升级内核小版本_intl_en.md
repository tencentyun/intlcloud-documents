
TencentDB for MySQL supports automatic or manual kernel minor version upgrade. Upgrading adds new features, improves performance, and fixes issues.
For details on the TencentDB for MySQL kernel minor version, see [Kernel Version Release Notes](https://intl.cloud.tencent.com/document/product/236/35989).

## Overview
- **Automatic upgrade**:
 - Scenario 1: When a severe bug or security vulnerability occurs in TencentDB for MySQL, the system will perform database kernel minor version upgrade during the maintenance window and send upgrade notifications through the console Message Center and SMS.
 - Scenario 2: When a TencentDB for MySQL instance is migrated due to instance configuration upgrade/downgrade, storage capacity expansion/reduction, or database version upgrade, etc., the system will automatically upgrade the instance's kernel to the latest minor version. If the source instance has read-only instances, the system will automatically determine the source-replica sync compatibility. If the source instance is migrated, a minor version later than that of the read-only instances will not be used.
- **Manual upgrade**:
You can also manually upgrade kernel minor version in the console.


## Upgrade rules
- If an instance to be upgraded is associated with other instances (e.g., source instance and read-only instances), these instances will be upgraded together to ensure data consistency.
- TencentDB for MySQL upgrade involves data migration. The time it takes to migrate an instance depends on the size of the instance's data. Your business will not be affected during the upgrade and can be accessed as per usual.

## Notes
- Instance switch will be required after version upgrade is completed, which will cause your instance to disconnect for seconds. We recommend that you conduct the switch during the instance maintenance time. Make sure that your business has a reconnection mechanism. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).
- If the number of tables in a single instance exceeds one million, upgrade may fail and database monitoring may be affected. Make sure that the number of tables in a single instance is below one million.
- The kernel minor version cannot be downgraded once upgraded.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click the target instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. In the **Configuration Info** section, click **Upgrade Kernel Minor Version**.
![](https://main.qcloudimg.com/raw/3fda3cffc784b3cde619e698d728d486.png)
3. In the pop-up window, set the configuration items and click **Upgrade**.
**Delay Threshold for Data Consistency Check**: This option is available only during source instance upgrade, which can be an integer between 1 and 10 seconds. There may be a delay during the data consistency check. You need to set a data delay threshold. The database consistency check will be paused when the delay exceeds the set value and will be resumed when the delay drops below the threshold. If the threshold value is too small, the migration may take longer.
>!As database upgrade involves data migration, a momentary disconnection from the MySQL database may occur after the upgrade is completed. We recommend that you set the switch time to **During maintenance time**, so that the switch will be initiated within the next maintenance time after the instance upgrade is completed.
>
![](https://qcloudimg.tencent-cloud.cn/raw/c758e092bce297bbfeb553297bf9b266.png)
