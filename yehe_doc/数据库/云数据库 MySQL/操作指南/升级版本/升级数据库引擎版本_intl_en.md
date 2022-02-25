
## Overview
This document describes how to upgrade the TencentDB for MySQL engine in the console.
TencentDB for MySQL supports database engine upgrade:
- From MySQL 5.5 to MySQL 5.6
- From MySQL 5.6 to MySQL 5.7

>?
>- Database engine downgrading is not supported.
>- Upgrading across major releases is not supported. For example, to upgrade a TencentDB for MySQL 5.5 instance to MySQL 5.7 or later, you have to upgrade it to MySQL 5.6 first.
>- Currently, MySQL 5.7 cannot be upgraded to MySQL 8.0. 
<span id ="shengjiguize"></span>
## Upgrade Rules
- The `create table …  as select …` syntax is not supported.
- Source-replica sync in TencentDB for MySQL 5.6 and 5.7 is implemented based on GTID. Only InnoDB is supported by default.
- MyISAM tables will be converted to InnoDB tables during the process of upgrading from MySQL 5.5 to 5.6. **We recommend that you complete the conversion first before upgrading.**
- During upgrade, TencentDB for MySQL will clear the `slow_log` table. Please save the logs before upgrading if necessary.
- **If an instance to be upgraded is associated with other instances (e.g., the source instance and read-only replicas), these instances will be upgraded together to ensure data consistency.**
- TencentDB for MySQL upgrade involves data migration and generally takes a relatively long time. Please wait patiently. During the upgrade process, your business will not be affected and the instance can be accessed as usual.
- Instance switchover may be needed after version upgrade is completed (i.e., the MySQL instance may be disconnected for a few seconds). We recommend that applications be configured with auto reconnection feature and that instance switchover be conducted during the instance maintenance window. For more information, see [Setting Instance Maintenance Window](https://intl.cloud.tencent.com/document/product/236/10929).
- If the number of tables in a single instance exceeds one million, upgrade may fail and database monitoring may be affected. Please make sure the number of tables in a single instance is no more than one million.

## Directions
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb/), locate the desired instance in the instance list, and select **More** > **Upgrade Version** in the **Operation** column.
>?MySQL 8.0 cannot be upgraded to a later version.
>
2. In the pop-up window, select the database version to be upgraded to and click **Upgrade**.
As database upgrading involves data migration, after the upgrade is completed, a very short disconnection from the MySQL database lasting for just seconds may occur. When the upgrade is initiated, the **Switch Time** can be selected as **During maintenance time**, so that the switch will be initiated within the next **maintenance window** after the instance upgrade is completed.
>!If you select **During maintenance time**, the switch will not occur immediately after the database specification upgrade is completed; instead, the sync will continue till the instance goes into the next **maintenance window** when the switch will be performed. In this way, the overall time it takes to upgrade the instance may be extended.
>
![](https://qcloudimg.tencent-cloud.cn/raw/5fd7b83457ffb0cab80112ad32e8e0be.png)

## FAQs
#### Will TencentDB for MySQL automatically back up data before upgrade?
TencentDB for MySQL adopts the daily real-time dual-server hot backup mechanism which supports lossless restoration of data from the last 7–732 days based on data backup and log backup (binlog).

#### Can TencentDB for MySQL be downgraded from MySQL 5.7 to MySQL 5.6?
No. Database engine downgrading is not supported. To use a MySQL 5.6 instance, you need to terminate or return the existing MySQL 5.7 instance, and then purchase a MySQL 5.6 instance.

#### Will there be a source-replica delay during upgrade?
Source instance upgrade requires data comparison and may cause a source-replica delay.

#### Will the instance switch after database engine version upgrade affect my TencentDB for MySQL instance?
The upgrade won’t affect your business but the TencentDB for MySQL instance may be disconnected for a few seconds. We recommend that applications be configured with auto reconnection feature and that instance switch be conducted during the instance maintenance window.

#### How long will it take to upgrade the database engine version of a TencentDB for MySQL instance? How do I check the upgrade progress?
The upgrade duration depends on the amount of data in the instance, the data replication speed, etc.
TencentDB for MySQL upgrade involves data migration and generally takes a relatively long time. Please wait patiently. Your business will not be affected during the upgrade process and can be accessed normally.

#### Why is the instance always in the "Waiting for switch" status?
It may be because you select **During maintenance time** as the **Switch Time**, and the switch will be initiated within the next maintenance window after the instance upgrade is completed.
To switch the instance immediately, click **Switch Now** in the **Operation** column in the instance list. The connection may be interrupted during switch. Make sure that the database has a reconnection mechanism.
