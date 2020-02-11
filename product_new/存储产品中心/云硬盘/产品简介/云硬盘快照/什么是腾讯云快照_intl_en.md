## Feature Overview
- Real-time replica of online data
Snapshots are fully usable copies of cloud disks. When a problem occurs to a cloud disk for which a snapshot has been created, the status before the problem occurred can be quickly restored using the snapshot. We recommend you create a snapshot of the related cloud disk before making major changes to your businesses, so that data can be quickly restored if business changes fail.
- Persistent backup of critical milestones
Snapshots can be used as persistent backups of business data to keep the milestone status of business data.
- Fast deployment of business
You can use the snapshot of your business to quickly clone multiple cloud disks, achieving quick deployment of servers.

## Scenarios
A convenient and efficient data protection service, snapshots are recommended for the following business scenarios:
- Daily data backup
You can use snapshots to regularly back up important business data to counter data loss caused by misoperations, attacks, viruses, etc.
- Fast restoration of data
Before performing major operations such as switching operating systems, upgrading applications, or migrating business data, you can create one or more snapshots. If any problem occurs when making these changes, you can restore the business data using the snapshot you have created.
- Application of multiple replicas of production data
You can provide actual production data in near real time for applications such as data mining, report query, and development testing by creating snapshots of production data.
- Fast deployment of environments
You can create a snapshot of a CVM and use the snapshot to create a custom image. You can use this image to quickly create one or more CVM instances, deploying multiple CVMs with the same environment in a batch to save the time spent on duplicate configurations.

## Billing
For detailed billing information on snapshot service, please see [Snapshot billing overview](https://intl.cloud.tencent.com/document/product/362/32415) and [Billing Overview](https://intl.cloud.tencent.com/document/product/362/2413).

## Quota Limits
For details on snapshot quota limits, refer to [Service Limits](https://intl.cloud.tencent.com/document/product/362/5145).

## Snapshot Types
- Manual Snapshot
You can manually create a snapshot for cloud disk data at a certain point in time. This snapshot can be used to create more cloud disks with identical data, or to restore the cloud disk to the status at this point in time later. For more information, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
- Scheduled Snapshot
For continuously updated business, you can use scheduled snapshots to create continuous data backups. To achieve continuous backups of cloud disk data over a certain period, you just need to configure a backup policy and associate it with cloud disks, significantly enhancing data security. For more information, see [Scheduled Snapshots](https://intl.cloud.tencent.com/document/product/362/31622).

> During snapshot creation, application data saved in the memory may not be persistently stored, causing snapshots to be unable to capture the latest and most complete cloud disk data. Refer to [Notes]) to ensure the consistency of snapshot data.


## Case Review
#### Case 1: Failing to manually create snapshots before a high-risk operation, causing data loss
**Details**: Customer A never created a snapshot for the cloud disk. In May 2019, an operator performed a fio test on the cloud disk. The file system was corrupted and data could not be recovered.
**Analysis**: If customer A has created a snapshot for the cloud disk before testing, he can enable snapshot rollback after data damage occurred to restore the business right away.

#### Case 2: Failing to create scheduled snapshots for important data disk, causing data loss
**Details**: Customer B created snapshots for multiple cloud disks, but not for cloud disks newly purchased after January 2019 due to cost concerns. In June 2019, a cloud disk not protected by snapshots had an unrecoverable data loss due to an accidental deletion of system-layer file data.
**Analysis**: If customer B has created scheduled snapshots for this cloud disk, he can restore the data to the status at the time point of the previous snapshot, thereby minimizing loss after the accidental data deletion. After the incident, customer B has created a snapshot for that cloud disk to enhance data protection.

#### Case 3: Rolling back with scheduled snapshot to restore business after a misopeartion
**Details:** Customer C created snapshots for all cloud disks. In May 2019, a startup exception occurred due to a misoperation.
**Analysis**: Customer C promptly restored data using scheduled snapshots taken two days ago, and the business was not affected.


In these above cases, operating errors lead to data loss. By comparison, we find that:
- In the situation where **a snapshot hasn’t been created**, data recovery is difficult when a server or cloud disk exception occurs, causing major loss.
- In the situation where **a snapshot has been created**, data can be recovered when a server or cloud disk exception occurs, minimizing loss.

We recommend you regularly create snapshots for businesses based on their types, enhancing data security and achieving low-cost, high-efficiency disaster recovery.

## Others
For other questions, please refer to [Snapshot FAQs](https://intl.cloud.tencent.com/document/product/362/17820).







