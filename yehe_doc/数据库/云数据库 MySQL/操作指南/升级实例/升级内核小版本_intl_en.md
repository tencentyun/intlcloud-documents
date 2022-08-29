
TencentDB for MySQL supports automatic or manual kernel minor version upgrade. The upgrade can add new features, improve the performance, and fix issues.
For more information on the TencentDB for MySQL kernel minor version, see [Kernel Version Release Notes](https://intl.cloud.tencent.com/document/product/236/35989).

>?Currently, basic single-node instances don't support kernel minor version upgrade.

## Overview
- **Automatic upgrade**:
 - Scenario 1: When a severe bug or security vulnerability occurs in TencentDB for MySQL, the system will upgrade the database kernel minor version during the maintenance time and send upgrade notifications through Message Center and SMS.
 - Scenario 2: When a TencentDB for MySQL instance is migrated due to instance configuration upgrade/downgrade, disk capacity expansion/reduction, or database version upgrade, etc., the system will automatically upgrade the instance's kernel to the latest minor version. If the source instance has read-only instances, the system will automatically determine the source-replica sync compatibility. If the source instance is migrated, a minor version later than that of the read-only instances will not be used.
- **Manual upgrade**:
You can also manually upgrade kernel minor version in the console.


## Upgrade rules
- If an instance to be upgraded is associated with other instances (such as source and read-only instances), these associated instances will be upgraded together to ensure the data consistency.
- TencentDB for MySQL upgrade involves data migration. The time it takes for migration depends on the data size. Your business will not be affected during the upgrade and can be accessed as per usual.

## Notes
- Instance switch will be required after version upgrade is completed (that is, the MySQL database may be disconnected for seconds). We recommend you use applications configured with auto reconnection feature and conduct the switch during the instance maintenance time. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).
- If the number of tables in a single instance exceeds one million, upgrade may fail and database monitoring may be affected. Make sure that the number of tables in a single instance is below one million.
- The kernel minor version cannot be downgraded once upgraded.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click the target instance ID or **Manage** in the **Operation** column to enter the instance details page.
2. In the **Configuration Info** section, click **Upgrade Kernel Minor Version**.
![](https://main.qcloudimg.com/raw/3fda3cffc784b3cde619e698d728d486.png)
3. In the pop-up window, select the switch time and click **Upgrade**.
>!As database upgrade involves data migration, a momentary disconnection from the MySQL database may occur after the upgrade is completed. We recommend you set the switch time to **During maintenance time**, so that the switch will be initiated within the next maintenance time after the instance upgrade is completed.
>
<img src="https://qcloudimg.tencent-cloud.cn/raw/c758e092bce297bbfeb553297bf9b266.png"  style="zoom:90%;">

