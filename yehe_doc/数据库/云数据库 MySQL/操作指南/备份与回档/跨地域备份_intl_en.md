This document describes the cross-region backup feature of TencentDB for MySQL. This feature allows you to store backup files in another region, which enhances the regulatory compliance and disaster recovery capabilities and improves the data reliability.



## Background
Data is an important part of enterprise operations. Although the information technology brings convenience, electronic data and stored information are very vulnerable to damage or loss. Any incident, such as natural disaster, system failure, maloperation, or virus, can cause business interruptions or even disastrous losses. Therefore, ensuring the security and integrity of core data is a top priority of every enterprise.

The cross-region backup feature of TencentDB for MySQL can be used to store backup files in another region so as to minimize data corruptions caused by natural disasters or system failures. This feature ensures the high availability, security, and recoverability of data and implement various features, such as remote backup and restoration, remote disaster recovery, long-term data archive, and regulatory compliance.
![](https://qcloudimg.tencent-cloud.cn/raw/0ef38b85a725ba88de13c31179d06e17.jpeg)

## Notes on Cross-Region Backup
- A cross-region backup can be restored to the instance regions or backup region.
- Once enabled, cross-region backup doesn't affect the local default backup, and both coexist.
- Cross-region backup will be triggered after the local automatic backup is completed, that is, the automatic backup will be dumped to the storage device for cross-region backup.
- The retention period of cross-region backup only affects the backup cycle of the cross-region storage.
- Backups and binlogs stored in a remote region cannot use the free storage space, and cross-region backups will use the space in the backup region of the source instance.
- Enabling/disabling cross-region backup or changing the region won't affect existing backups.
- After cross-region backup is enabled, the last valid backup and the binlogs generated from the last valid backup time to the current time will be synced to the target region.
- If you enable cross-region backup again, remote backups generated before the enablement cannot be used to restore data to the specified time point.

## Billing
For more information on cross-region backup billing, see [Backup Space Billing](https://intl.cloud.tencent.com/document/product/236/32344).

## Differences Between Cross-Region Backup and Local Default Backup

| Comparison Item | Cross-Region Backup | Local Default Backup |
|---------|---------|---------|
| Enabled by default | No. It needs to be enabled manually. | Yes. |
| Backup storage region | Up to two specified remote regions. | Instance region. |
| Backup restoration | The data can be restored to: <li>Original instance<li>New instance in the target region | The data can be restored to: <li>Original instance<li>New instance in the current region</li> |
| Uses the free storage space | No. | Yes. |

## Supported Regions
This feature is currently available in Beijing, Shanghai, Guangzhou, Shenzhen, and Chengdu regions and will be available in more regions in the future.

## Enabling Cross-Region Backup
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Backup and Restoration** > **Cross-Region Backup**.
3. In the **Cross-Region Backup** window, complete the configuration and click **OK** to enable cross-region backup.
 - Cross-Region Backup: It is disabled by default.
 - Back Up Binlog: When cross-region backup is enabled, it will be enabled automatically and can be disabled separately.
 - Backup Region: Select one or two regions other than the source instance region.
 - Backup Retention Period: 7 days by default. Value range: 3–1830 days. Backup sets will be deleted automatically upon expiration.
4. After cross-region backup is completed, the backup will be synced to the target region and can be queried in the backup list of the source instance.
For cross-region backup files, all selected backup regions are displayed in the **Backup Region** column.
The backup list has the following fields:
<table>
<thead><tr><th>Field</th><th>Description</th></tr></thead>
<tbody><tr>
<td>File Name</td>
<td>You can set a filename when creating a backup, which cannot be modified after the backup is created.</td></tr>
<tr>
<td>Backup Time</td>
<td>The backup start time.</td></tr>
<tr>
<td>Task Start Time<br>Task End Time</td>
<td>The time points when the backup task starts and ends respectively.</td></tr>
<tr>
<td>Backup Size</td>
<td>The size of the current backup file.</td></tr>
<tr>
<td>Type</td>
<td>The type of the backup file. For a cross-region backup, it is **Physical cold backup**.</td></tr>
<tr>
<td>Backup Mode</td>
<td>Automatic backup</td></tr>
<tr>
<td>Backup Method</td>
<td>Full backup</td></tr>
<tr>
<td>Backup Region</td>
<td>It displays all regions where the backup file is stored.</td></tr>
<tr>
<td>Status</td>
<td>It displays the backup task status.</td></tr>
<tr>
<td>Operation</td>
<td><a href="https://www.tencentcloud.com/document/product/236/50651">Download</a><br><a href="https://intl.cloud.tencent.com/document/product/236/38864">Clone</a></td></tr>
</tbody></table>


## Disabling Cross-Region Backup
You can disable the cross-region backup feature in the console. After it is disabled, cross-region backup files won't be deleted immediately; instead, they will be deleted automatically upon expiration.
1. Log in to the [TencentDB for MySQL console](https://console.cloud.tencent.com/cdb). In the instance list, click an instance ID or **Manage** in the **Operation** column to enter the instance management page.
2. On the instance management page, select **Backup and Restoration** > **Cross-Region Backup**.
3. In the **Cross-Region Backup** window, disable the feature and click **OK**.

## FAQs
#### Why are fees still incurred after I disable cross-region backup?
If your data volume exceeds the free storage space, the excessive data will be billed. After cross-region backup is disabled, no more new backups will be generated, but existing backups won't be deleted immediately. They will be retained within the retention period and use the storage space before expiration, so they will still incur fees before expiration. You can set the backup retention period to automatically clear all expired backup files, and then no more cross-region backup fees will be incurred.
