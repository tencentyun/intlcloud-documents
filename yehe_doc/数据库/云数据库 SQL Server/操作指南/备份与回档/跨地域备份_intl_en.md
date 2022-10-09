This document describes the cross-region backup feature of TencentDB for SQL Server. This feature allows you to store backup files in another region, which enhances the regulatory compliance and disaster recovery capabilities and improves the data reliability.

## Overview
Data is an important part of enterprise operations. Although the information technology brings convenience, it also reveals that electronic data and stored information are very vulnerable to damage or loss. Any incident, such as natural disaster, system failure, maloperation, or virus, can cause interruption of business operations or even disastrous losses. Therefore, ensuring the security and integrity of core data is a top priority of every enterprise.

The cross-region backup feature of TencentDB for SQL Server can be used to store backup files in another region so as to minimize data corruptions caused by natural disasters or system failures. This feature ensures the high availability, security, and recoverability of data and implement various features, such as remote backup and restoration, remote disaster recovery, long-term data archive, and regulatory compliance.

![](https://qcloudimg.tencent-cloud.cn/raw/cb4c4fe6a1bb77c3e0cb0819639406e4.jpeg)

## Notes on cross-region backup
- Cross-region backup doesn't affect the local default backup, and both coexist after cross-region backup is enabled.
- Cross-region backup will be triggered after the local default automatic backup is complete, that is, the default automatic backup is dumped to the storage device for cross-region backup.
- Backup files in the cross-region backup space include automatic data backups and log backups, that is, local automatic backups are automatically synced to the destination region for storage.
- The retention period of cross-region backups is 7 days by default and customizable between 7 and 1,830 days.
- Enabling/Disabling cross-region backup or changing the backup region won't affect existing backups.
- The retention period of cross-region backups only affects their lifecycle.
- Modifying the cross-region backup retention period will affect the lifecycle of existing cross-region backups.
- Changing the backup region option for cross-region backup won't affect the backup and storage regions of existing cross-region backups.
- Cross-region backups stored in another region cannot use the free storage space provided for local backups.

## Billing
Cross-region backup fees consist of **storage** and **traffic** fees:
**Cross-region backup fees = cross-region backup storage fees + cross-region replication traffic fees**

Cross-region backup storage and traffic fees are charged based on the destination region and the linkage between the source and destination regions respectively in a pay-as-you-go manner.
For billing details, see [Cross-Region Backup Billing](https://www.tencentcloud.com/document/product/238/50229).

## Differences between cross-region backup and local backup

| Item | Local Backup | Cross-Region Backup |
|---------|---------|---------|
| Enabled by default | Yes. | No. It needs to be enabled manually. |
| Backup storage region | Instance region. | Destination region. |
| Region for backup billing | The backup volume is counted in the backup space for the backup region of the primary instance. | The backup volume is counted in the backup space for the backup region of the primary instance, and backup fees are calculated at the price of the backup storage region (i.e., the destination region). |
| Billing cycle | <li>For a pay-as-you-go instance, local backups are retained for three days by default after the instance is moved to the recycle bin and are terminated along with the instance after three days. | For a pay-as-you-go instance, local backups are retained for three days by default after the instance is moved to the recycle bin and are terminated along with the instance after three days. |
| Uses the free storage space | Yes. | No. |
| Backup space billing rules | <li>Before the backup size exceeds the free tier, backups are free of charge. After the backup size exceeds the free tier, the `hourly backup fees = (total size of backup files - free tier) * backup unit price`<li>`Billable space = data backup volume (automatic + manual) + log backup volume (automatic) - free backup space (all values are for the current region)`. | <li>After cross-region backup is enabled, all the generated cross-region backup files will incur fees.<li>`Billable space (for the region of the primary instance) = data backup volume (automatic) + log backup volume (automatic) (all values are for the destination region)`. |

## Supported regions

| Source Region | Supported Destination Region |
|---------|---------|
| Beijing, Guangzhou, Shanghai, Chengdu, Chongqing, Nanjing, Beijing Finance, Shanghai Finance, Shenzhen Finance, and Hong Kong (China) | Beijing, Guangzhou, Shanghai, Chengdu, Chongqing, Nanjing, Beijing Finance, Shanghai Finance, and Shenzhen Finance.<br>Any region other than the source region, subject to the supported regions as indicated in the console. |


>?
>- Currently, you cannot perform a cross-region backup task from a Chinese mainland region to Hong Kong (China).
>- Currently, cross-region backup is not supported outside the Chinese mainland but will be supported in more regions in the future.

## Enabling cross-region backup in the console
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. In the instance list, click the ID or **Manage** in the **Operation** column of the target instance to enter the **Instance Management** page.
3. On the **Instance Management** page, select **Backup Management** and click **Cross-Region Backup Settings**.
![](https://qcloudimg.tencent-cloud.cn/raw/5b2d5d4ad76e1c6b3c131195e36955a8.png)
4. In the **Cross-Region Backup Settings** window, set the following parameters and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/9247e48ada9e07af5febece30e57d219.png)
<table>
<thead><tr><th>Parameter</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Cross-Region Backup</td>
<td>Switch for the cross-region backup feature, which can be toggled on.</td></tr>
<tr>
<td>Backup Region</td>
<td>The region where to store cross-region backups. Click the drop-down list to select one or two target regions.</td></tr>
<tr>
<td>Cross-Region Backup Retention Period</td>
<td>The period for retaining cross-region backup files, which can be set between 7 and 1,830 days.</td></tr>
<tr>
<td>Cross-Region Backup Billing Notes</td>
<td>Enabling cross-region backup will incur additional charges. Read the notes and indicate your consent.</td></tr>
</tbody></table>

## Modifying cross-region backup settings
>?
>- Changing the backup region will affect the storage region of new backups only but not existing backups.
>- Modifying the cross-region backup retention period will affect the lifecycle of both existing and new cross-region backups.

**Option 1**
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. In the instance list, click the ID or **Manage** in the **Operation** column of the target instance to enter the **Instance Management** page.
3. On the **Instance Management** page, select **Backup Management** and click **Cross-Region Backup Settings**.
4. In the **Cross-Region Backup Settings** window, modify the backup region and cross-region backup retention period and click **Save**.

**Option 2**
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select **Database Backup** on the left sidebar, and select a region at the top of the **Database Backup** page.
3. On the **Database Backup** page, select **Overview** > **Real-Time Backup Statistics** > **Cross-Region Backup**.
4. In the cross-region backup list, click **Cross-Region Backup Settings** in the **Operation** column of the target instance.
5. In the **Cross-Region Backup Settings** window, modify the backup region and cross-region backup retention period and click **Save**.

## Disabling cross-region backup
>?After cross-region backup is disabled, no cross-region backup files will be generated and billed.

**Option 1**
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. In the instance list, click the ID or **Manage** in the **Operation** column of the target instance to enter the **Instance Management** page.
3. On the **Instance Management** page, select **Backup Management** and click **Cross-Region Backup Settings**.
4. In the **Cross-Region Backup Settings** window, toggle off the **Cross-Region Backup** feature.
5. In the pop-up window, select **Retain** or **Delete** and click **OK**.
>?
>- If **Retain** is selected, existing cross-region backup files will be retained and billed for the configured cross-region backup retention period, which can be modified before cross-region backup is disabled.
>- If **Delete** is selected, existing cross-region backup files will be deleted when cross-region backup is disabled.

**Option 2**
1. Log in to the [TencentDB for SQL Server console](https://console.cloud.tencent.com/sqlserver).
2. Select **Database Backup** on the left sidebar, and select a region at the top of the **Database Backup** page.
3. On the **Database Backup** page, select **Overview** > **Real-Time Backup Statistics** > **Cross-Region Backup**.
4. In the cross-region backup list, click **Cross-Region Backup Settings** in the **Operation** column of the target instance.
5. In the **Cross-Region Backup Settings** window, toggle off the **Cross-Region Backup** feature.
6. In the pop-up window, select **Retain** or **Delete** and click **OK**.
