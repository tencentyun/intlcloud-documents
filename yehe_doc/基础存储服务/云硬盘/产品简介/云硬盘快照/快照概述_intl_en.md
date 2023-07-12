## Overview
- **Real-time replica of online data**
Snapshots are fully usable copies of cloud disks. When a problem occurs in a cloud disk where a snapshot has been created, you can use the snapshot to quickly restore the cloud disk to normal status. We recommend you create a snapshot for the cloud disk before making any major changes to your businesses, so that data can be quickly restored if the business changes fail.
- **Persistent backup at critical milestones**
Snapshots can be used as persistent backups of business data to keep the business data at milestones.
- **Quick business deployment**
Snapshots allow you to quickly clone multiple cloud disks for quick server deployment.

## Applications
Snapshots provide a convenient and efficient data protection service, which can be used in the following business scenarios:
- **Daily data backup**
You can use snapshots to regularly back up important business data to avoid data loss caused by incorrect operations, attacks, and viruses.
- **Quick data recovery**
You can create snapshots before performing major operations, such as changing operating systems, upgrading applications, or migrating business data. If any problem occurs, you can use snapshots to restore the business data.
- **Application of multiple replicas of production data**
You can create snapshots for the production data to provide near real-time data for applications such as data mining, report query, and development testing.
- **Quick environment deployment**
You can create snapshots for a CVM instance to create a custom image, and use the custom image to create CVM instances for batch deployment with the same environment and less configuration time.

## Billing
For more information about snapshot prices, see [Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415) and [Price Overview](https://intl.cloud.tencent.com/document/product/362/2413).

## Quota Limits
For more information about snapshot quota limits, see [Use Limits](https://intl.cloud.tencent.com/document/product/362/32406).

## Snapshot Types
- **Manual snapshot**
You can manually create a snapshot for a cloud disk at a certain point in time. This snapshot can be used to create more cloud disks with identical data, or to restore the cloud disk to the point in time when the snapshot was created. For more information, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
- **Scheduled snapshot**
For businesses that are updated continuously, you can use scheduled snapshots to provide continuous data backups. To achieve continuous backups of cloud disk data over a certain time period, you only need to configure a backup policy and associate it with cloud disks, which significantly enhancing data security. For more information, see [Scheduled Snapshot](https://intl.cloud.tencent.com/document/product/362/35238).


<dx-alert infotype="explain" title="">
During snapshot creation, application data saved in the memory may not be persistently stored. As such, snapshots may not capture the latest and most complete cloud disk data. Refer to [Notes](https://intl.cloud.tencent.com/document/product/362/5755#.E6.B3.A8.E6.84.8F.E4.BA.8B.E9.A1.B9) to ensure snapshot data consistency.
</dx-alert>




## Case Review
#### Case 1: No manual snapshots were created before performing high-risk operations, resulting in data loss
Customer A has never created a snapshot for the cloud disk. In May 2019, an operator performed a fio test on the cloud disk. The file system was corrupted. The data was damaged and could not be recovered.
**Analysis**: If customer A has created a snapshot for the cloud disk before testing, the snapshot can be used to roll back data and resume business immediately after the data damage.

#### Case 2: No scheduled snapshots were created for important data disks, resulting in data loss
Customer B created snapshots for multiple cloud disks, except those purchased after January 2019 for cost reasons. In June 2019, a cloud disk without snapshot protection had an unrecoverable data loss due to an accidental deletion of system-layer file data.
**Analysis**: If customer B has created scheduled snapshots for this cloud disk, the data can be recovered to the point in time when the last snapshot was created, thereby minimizing loss. After the incident, customer B created a snapshot for that cloud disk to enhance data protection.

#### Case 3: Using the scheduled snapshot to roll back data and restore business after an incorrect operation
Customer C created snapshots for all cloud disks. In May 2019, a startup exception occurred due to an incorrect operation.
**Analysis**: Customer C promptly restored data using the scheduled snapshot that was created two days ago, and the business remains stable.


These cases all involve data loss due to incorrect operations, but the results are different. By comparison, we can find that:
- In situations where **a snapshot hasn't been created**, data is rarely recoverable when a server or cloud disk exception occurs, resulting in major loss.
- In situations where **a snapshot has been created**, data can be recovered when a server or cloud disk exception occurs, minimizing loss.

We recommend regularly creating snapshots for businesses based on business types, enhancing data security and achieving low-cost, high-efficiency disaster recovery.

## Others
For other questions, refer to [Snapshot FAQs](https://intl.cloud.tencent.com/document/product/362/17820).



