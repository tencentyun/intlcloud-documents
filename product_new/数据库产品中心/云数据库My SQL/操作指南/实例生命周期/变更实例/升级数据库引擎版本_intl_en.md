## Operation Scenario
This document describes how to upgrade the TencentDB for MySQL engine in the console.
TencentDB for MySQL supports database engine upgrade:
- From MySQL 5.5 to MySQL 5.6
- From MySQL 5.6 to MySQL 5.7

<span id="shengjiguize"></span>
## Upgrade Rules
- Upgrading across major releases is not supported. For example, to upgrade a TencentDB for MySQL 5.5 instance to MySQL 5.7 or higher, you have to upgrade it to MySQL 5.6 first.
- The `create table …  as select …` syntax is not supported.
- Master-slave sync in TencentDB for MySQL 5.6/5.7 is implemented based on GTID. Only InnoDB is supported by default.
- MyISAM tables will be converted to InnoDB tables during the process of upgrading from MySQL 5.5 to 5.6. **You are recommended to complete the conversion first before upgrading**.
- During upgrade, TencentDB for MySQL will clear the `slow\_log` table. Please save the logs before upgrading if necessary.
- **If an instance to be upgraded is associated with other instances (e.g., master instance and read-only instances), these instances will be upgraded together to ensure data consistency.**
- TencentDB for MySQL upgrade involves data migration and generally takes a relatively long time. Please wait patiently. Your business will not be affected during the upgrade process and can be accessed normally.
- Instance switchover may be needed after an upgrade is completed (i.e., the MySQL instance may be disconnected for seconds). It is recommended that applications be configured with auto reconnection feature and that instance switchover be conducted during the instance maintenance period. For more information on maintenance period, see [Setting Instance Maintenance Period](https://intl.cloud.tencent.com/document/product/236/10929).
- If the number of tables in a single instance exceeds one million, upgrade may fail, and database monitoring may be affected. Please control this value appropriately and make sure that it is below 1 million.

## Directions
1. Log in to the [TencentDB for MySQL Console](https://console.cloud.tencent.com/cdb/).
2. Select the instance to be upgraded in the instance list and select **More** > **Upgrade Version** in the "Operation" column (MySQL 5.7 cannot be upgraded to a higher version).
![](https://main.qcloudimg.com/raw/ec14ff513f80db6e87338b5a531f6126.png)
3. In the pop-up window, select the database version to be upgraded to and click **Upgrade**.
As database upgrading involves data migration, after the upgrade is completed, a very short disconnection from the MySQL database lasting for just seconds may occur. When the upgrade is initiated, the **Switch Time** can be selected as **During maintenance window**, so that the switch will be initiated within the next **Maintenance Time** after the instance upgrade is completed.
>If you do so, the switch will not occur immediately after the database specification upgrade is completed; instead, the sync will continue till the instance goes into the next **maintenance period** when the switch will be performed. In this way, the overall time it takes to upgrade the instance may be extended.
>
![](https://main.qcloudimg.com/raw/8a27b736891296d8c64077cf01409f08.png)

