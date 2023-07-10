
The data backup point of a cloud disk is provided by Tencent Cloud to back up data automatically. It is a complete copy of cloud disk data at the backup time and can be used to restore historical data.
Unlike a [snapshot](https://intl.cloud.tencent.com/document/product/362/31638), the data backup point follows the lifecycle of the cloud disk. When the cloud disk is deleted, the data backup point will be deleted automatically and can no longer be used to restore data.

## Features of the Data Backup Point
- **Backing up historical data**
After the data backup point quota is configured, Tencent Cloud will automatically retain a historical data backup of the cloud disk at any time point on the last calendar day. If data becomes abnormal due to viruses, intrusions, or maloperations, the backup can be used to restore data to a time point before the exception.
- **Long-term backups**
The data backup point at any time point can be converted into a snapshot to retain the data backup for a longer time independent of the cloud disk's lifecycle.


## Data Backup Point Quota[](id:quota)

| Item | Description|
|--|--|
| Data backup point | Data backup created at a time point, which can be used to restore data. |
| Data backup point quota | Number of data backup points that can be retained for a cloud disk. It is billed and can be adjusted/returned. |


- You can configure the data backup point quota for newly purchased or existing cloud disks.
- Currently, only **one** data backup point is supported; that is, only one historical data backup can be retained for a cloud disk. After the data backup point quota is configured for a cloud disk, Tencent Cloud will **automatically** retain a historical data backup of the cloud disk at any time point on the **last calendar day**.
For example, if you purchase a cloud disk on May 2 and configure the data backup point quota to `1`, then:
 - On May 3, a historical data backup at any time point on May 2 will be retained for the cloud disk.
 - On May 4, a historical data backup at any time point on May 3 will be retained for the cloud disk, and the data backup on May 2 will be deleted automatically.
 - The process goes on until the cloud disk reaches the end of its lifecycle.


## Billing Details
#### Pricing
The billing of the data backup point quota is only related to the size of the cloud disk. The billing mode of the quota is the same as that of the cloud disk. For billing details, see [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).
>?Cloud disk data backup points enjoy a 50% discount for a limited time. The discount period:September 12, 2022 to September 12, 2023.


#### Fees after the adjustment
When you increase or decrease the data backup point quota, you can find the billing rules and examples in [Fees After Adjustment of Data Backup Point Quota](https://intl.cloud.tencent.com/document/product/362/50027#description).



## Use Limits[](id:restrictions)
- Currently, the data backup point quota can only be configured for data disks.
- Currently, the data backup point quota can only be configured to `1` for each cloud disk; that is, each cloud disk can have one data backup point retained.
- The data backup point is not billed like a snapshot.
- The data backup point is automatically created by Tencent Cloud for cloud disks and cannot be created manually.
- The data backup point follows the lifecycle of the cloud disk. To retain data for a longer period, convert the data backup point into a [snapshot](https://intl.cloud.tencent.com/document/product/362/31638).



## Directions
<table>
<tr>
<th>Operation</th>
<th>Reference</th>
</tr>
<tr>
<td>Configure the data backup point quota when purchasing a cloud disk.</td>
<td><a href="https://www.tencentcloud.com/document/product/362/5744">Creating Cloud Disk<a></td>
</tr>
<tr>
<td>Increase or reduce/return the data backup point quota of an existing cloud disk.</td>
<td><a href="https://www.tencentcloud.com/document/product/362/50027">Adjusting Data Backup Point Quota<a></td>
</tr>
<tr>
<td>View the information of the data backup point of a cloud disk.</td>
<td><a href="https://www.tencentcloud.com/document/product/362/50602">Viewing Cloud Disk Information<a></td>
</tr>
<tr>
<td>Use an existing data backup point to restore cloud disk data.</td>
<td><a href="https://www.tencentcloud.com/document/product/362/50028">Using Data Backup Point to Restore Cloud Disk Data<a></td>
</tr>
<tr>
<td>Convert a data backup point into a snapshot to retain data for a long time.</td>
<td><a href="https://www.tencentcloud.com/document/product/362/50029">Converting Data Backup Point into Snapshot<a></td>
</tr>
<tr>
<td>Delete a data backup point.</td>
<td><a href="https://www.tencentcloud.com/document/product/362/50030">Deleting Data Backup Point<a></td>
</tr>
</table>


