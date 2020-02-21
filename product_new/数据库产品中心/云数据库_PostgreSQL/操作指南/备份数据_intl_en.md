## Operation Scenarios
Currently, TencentDB for PostgreSQL High Availability Edition only supports physical backup:
- **Full backup**: once a day at 01:00.
- **Incremental backup**: for xlog files, backup will be performed once every 15 minutes or when the number of files reaches 60.
- **Data file retention period**: full and incremental backups in the last 7 days will be retained.

This document describes how to download backup files in the TencentDB for PostgreSQL Console.

## Directions
1. Log in to the [TencentDB for PostgreSQL Console](https://console.cloud.tencent.com/pgsql) and click an instance name to enter the instance details page.
2. On the **Backup Management** tab, click **Backup List** or **xlog List**, select the desired backup, and click **Download** in the "Operation" column.
>Backup data in the **Backup List** is full backup, while that in the **xlog List** is incremental backup.
3. In the pop-up window, you can choose a VPC address or public network address to download the backup file.
>To ensure data security, an address will be valid for 15 minutes. After it expires, please refresh the page to get a new address. Please access a VPC address in a VPC.
>
