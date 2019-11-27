## Feature Overview
- Real-time replica of online data
Snapshots are fully usable copies of cloud disks. When a problem occurs to a cloud disk for which a snapshot has been created, the state before the problem occurred can be quickly restored using the snapshot. We recommend that you create a snapshot of the related cloud disk before making major changes to your businesses so that the data can be quickly restored if the change to the business fails. 
- Persistent backup of critical milestones
Snapshots can be used as persistent backups of business data, which can keep the milestone status of the business data.
- Fast deployment of business
You can use the snapshot of business to quickly clone multiple cloud disks, achieving quick server deployment.

## Scenarios
As a convenient and efficient data protection service, snapshots are recommended for the following business scenarios:
- Daily data backup
You can use snapshots to regularly back up important business data to counter the risk of data loss caused by mis-operations, attacks, viruses or etc. 
- Fast restoration of data
Before making major upgrades, such as switching operating systems, upgrading applications, or migrating business data, you can create one or more snapshots so that if any problem occurs in the process of making the change, you can then restore the business data using the snapshot that you previously created.
- Application of multiple replicas of production data
You can provide real production data in near real time for applications such as data mining, report query, and development testing by creating snapshots of production data.
- Fast deployment of environments
You can create a snapshot of a CVM and use the snapshot to create a custom image. Using the created image, you can create one or more CVM instances quickly, so as to deploy multiple CVMs with the same environment in a batch, eliminating the effort for duplicate configurations.

## Billing Rules
For detailed billing information on snapshot service, please see [Snapshot Billing Overview](https://intl.cloud.tencent.com/document/product/362/32415) and [Snapshot Pricing List](https://intl.cloud.tencent.com/document/product/362/2413). 

## Quota Limits
For details on snapshot quota limits, refer to [Use Limits](https://intl.cloud.tencent.com/document/product/362/5145).

## Snapshot Types
- Manual Snapshot
You can manually create a snapshot for data in a cloud disk at a certain point in time. This snapshot can be used to create more cloud disks with identical data, or to later restore the cloud disk to the state at that point in time. For more information, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755).
- Scheduled Snapshot
For frequently-updated business, you can configure scheduled snapshot policy to create data backups continuously. You just need to configure a backup policy and associate it with cloud disks, and then you can making backups for cloud disks over a certain period, substantially enhancing data security. For more information, see [Scheduled Snapshots](https://intl.cloud.tencent.com/document/product/362/31622).

> In the process of creating snapshots, application data that saved in the memory may be failed to be persistently stored. This can lead to the snapshot not being able to capture the latest and most complete cloud disk data. Refer to [Notes](https://intl.cloud.tencent.com/document/product/362/5755) to ensure the consistency of snapshot data.


## Case Review
#### Case 1: Failing to do a manual snapshot before a high-risk operation, leading to data loss
**Details**: Customer A has never created a snapshot for their cloud disk. One day in May 2019, an operator performed a fio test on the cloud disk, and the file system was corrupted, with the data unable to be recovered.
**Analysis**: If customer A had made a snapshot of the cloud disk before the testing, then they could quickly enable snapshot rollback after the data was corrupted and be able to restore the business right away.

#### Case 2: Scheduled snapshots not created for important data disk, leading to data loss
**Details**: Customer B made snapshots of multiple cloud disks, but did not make snapshots of cloud disks newly purchased after January 2019 due to cost concerns. One day in June 2019, a cloud disk that was not protected by snapshot had an unrecoverable data loss because of an accidental deletion of file system layer data.
**Analysis**: If customer B had protected the cloud disk with scheduled snapshots, then they could have restored the data to the state at the time point of the previous snapshot after the accidental deletion of data, thereby minimizing loss. After the incident occurred, customer B took the initiative to create a snapshot for that cloud disk to strengthen the all-around protection of data.  

#### Case 3: Rolling back with scheduled snapshot to restore data after a mis-opeartion
**Details:** Customer C has created snapshots for all cloud disks. One day in May 2019, a startup exception occurred due to a mis-operation. Customer C promptly restored the data from the scheduled snapshot taken two days ago, and the business was not affected. 
**Analysis**: The snapshot helps Customer C to restore data and ensure normal business running.


From the above cases, we can learn the following:
- In the situation where **a snapshot was not created**, it will be very difficult to recover the data of the server or cloud disk when a problem occurs, easily leading to major loss.
- In the situation where **a snapshot was created**, the data can be recovered when a problem occurs to the server or cloud disk, minimizing the loss.

We recommend that you regularly create snapshots for businesses of different types to enhance data security and to achieve low-cost, high-efficiency disaster recovery for businesses.

## Others
If you still have other questions, please refer to [FAQ About Snapshots](https://intl.cloud.tencent.com/document/product/362/17820). 







