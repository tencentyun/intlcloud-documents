
## Overview
TencentDB for SQL Server allows you to create databases on the **Database Management** page in the console and authorize accounts for database access.

## Maximum number of databases created in a single instance
>!
>- In a High Availability or Cluster Edition instance, if you use the default value of 0 for the `max worker threads` parameter, you cannot create more than 100 databases. To create more databases, you must set this parameter to 20,000 as instructed in [Setting Instance Parameters](https://intl.cloud.tencent.com/document/product/238/41609).
>- If the instance only has one CPU core, we recommend that you keep the database limit at 70 to guarantee instance stability.
>
SQL Server 2008 R2 Enterprise instances don't support lifting the database quantity limit, which is 70. The limit in other SQL Server instances is subject to the number of instance CPU cores as calculated below:
- **High Availability Edition**
2012 Standard/Enterprise
2014 Standard/Enterprise
2016 Standard/Enterprise
Maximum number of databases:
![](https://qcloudimg.tencent-cloud.cn/raw/7d31129a2b024e9fd35711f063f4a140.jpg)
Extract the square root of the CPU core quantity, round it to one decimal place, multiply the result by 40, and add the product to 80 to get the value X. The smaller value between X and 300 is the maximum number of databases. For example, you can create up to 160 databases in a 4-core 16 GB MEM SQL Server 2014 Enterprise instance.
- **Cluster Edition**
2017 Enterprise
2019 Enterprise
Maximum number of databases:
![](https://qcloudimg.tencent-cloud.cn/raw/2d10dfd0365cd7217849aa1aafaf5a8c.jpg)
Extract the square root of the CPU core quantity, round it to one decimal place, multiply the result by 40, and add the product to 120 to get the value Y. The smaller value between Y and 340 is the maximum number of databases. For example, you can create up to 200 databases in a 4-core 16 GB MEM SQL Server 2017 Enterprise instance.
- **Basic Edition**
2008 R2 Enterprise
2012 Enterprise
2014 Enterprise
2016 Enterprise
2017 Enterprise
2019 Enterprise
Maximum number of databases:
![](https://qcloudimg.tencent-cloud.cn/raw/3bc4f1a02187becdecb1f47d70676a46.jpg)
Extract the square root of the CPU core quantity, round it down to the nearest integer, and multiply the result by 100 to get the value N. The smaller value between N and 400 is the maximum number of databases. For example, you can create up to 200 databases in a 4-core 16 GB MEM SQL Server 2017 Enterprise instance.

**Table of instance CPU core quantity and corresponding maximum database quantity**
<dx-tabs>
::: Maximum number of databases in Dual-Server High Availability/Cluster Edition
| CPU Cores | Dual-Server High Availability Edition | Cluster Edition |
|---------|---------|---------|
| 1 | 70 | 70 |
| 2 | 136 | 176 |
| 4 | 160 | 200 |
| 8 | 193 | 233 |
| 12 | 218 | 258 |
| 16 | 240 | 280 |
| 24 | 275 | 315 |
| 32 | 300 | 340 |
| 48 | 300 | 340 |
| 64 | 300 | 340 |
| 96 | 300 | 340 |

:::
::: Maximum number of databases in Basic Edition
| CPU Cores | Basic Edition |
|---------|---------|
| 2 | 100 |
| 4 | 200 |
| 8 | 200 |
| 16 | 400 |
| 24 | 400 |

:::
</dx-tabs>

## Directions
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver) and click the ID of the target instance in the instance list or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select the **Database Management** tab, click **Create Database**, set configuration items in the pop-up window, confirm that everything is correct, and click **OK**.
![](https://main.qcloudimg.com/raw/e35649cddc46342128bb8c396d120dd1.png)
 - Database Name: It can contain up to 32 letters, digits, and underscores and must start with a letter.
 - Supported Character Set: Select the character set to be used by the database. Currently, most native character sets are supported.
 - Authorize Account: You can authorize existing accounts to access the database. If you haven't created an account yet, see [Creating Account](https://intl.cloud.tencent.com/document/product/238/7521).
 - Remarks: It can contain up to 256 characters.

