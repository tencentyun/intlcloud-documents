## Overview

- **Real-time replica of online data**
  Snapshots are fully usable copies of file systems. When a problem occurs in a file system where a snapshot has been created, you can use the snapshot to quickly restore the file system to normal status. We recommend you create a snapshot for the file system before making any major changes to your businesses, so that data can be quickly restored if the business changes fail.
- **Persistent backup at critical milestones**
  Snapshots can be used as persistent backups of business data to keep the business data at milestones.
- **Quick business deployment**
  Snapshots allow you to quickly clone multiple file systems for quick service deployment.


## How Snapshots Work

A file system snapshot is a block-level clone or backup. In general, the snapshot size will be larger than the data size displayed in the file system because:

- The underlying data block stores the metadata of the file system.
- Deleting data modifies the written-in data block, which will be backed up to snapshots.

## Use Cases

Snapshots provide a convenient and efficient data protection service, which can be used in the following business scenarios:

- **Daily data backup**
  You can use snapshots to regularly back up important business data to avoid data loss caused by incorrect operations, attacks, and viruses.
- **Quick data recovery**
  You can create snapshots before performing major operations, such as changing operating systems, upgrading applications, or migrating business data. If any problem occurs, you can use snapshots to restore the business data.
- **Application of multiple replicas of production data**
  You can create snapshots for the production data to provide near real-time data for applications such as data mining, report query, and development testing.
- **Quick environment deployment**
  You can use an existing snapshot to create one or more file systems to quickly deploy the same business environment in batches, saving the time of repeated configuration.

## Billing

The free beta is scheduled to end on March 1, 2022.

## Quota Limits

For more information about snapshot quota limits, see [Use Limits](https://intl.cloud.tencent.com/document/product/582/44913).

## Snapshot Types

- **Manual snapshot**
  You can manually create a snapshot for a file system at a certain point in time. This snapshot can be used to create more file systems with identical data. For more information, see [Creating Snapshots](https://intl.cloud.tencent.com/document/product/582/44914).
- **Scheduled snapshot**
  For businesses that are updated continuously, you can use scheduled snapshots to provide continuous data backups. To achieve continuous backups of file system data over a certain time period, you only need to configure a backup policy and associate it with file systems, significantly enhancing data security. For more information, see [Scheduled Snapshot](https://intl.cloud.tencent.com/document/product/582/44915).

>? During snapshot creation, application data saved in the memory may not be persistently stored. As such, snapshots may not capture the latest and most complete file system data. Refer to [Notes](https://intl.cloud.tencent.com/document/product/582/44914) to ensure snapshot data consistency.



## Case Review

#### Case 1: No manual snapshots were created before performing high-risk operations, resulting in data loss

Customer A has never created a snapshot for its file system. In May 2019, an operator performed a fio test on the file system. The file system was corrupted. The data was damaged and could not be recovered.
**Analysis**: If customer A has created a snapshot for the file system before testing, the snapshot can be used to create a new file system and resume business immediately after the data damage.

#### Case 2: No scheduled snapshots were created for important file systems, resulting in data loss

Customer B created snapshots for multiple file systems, except those purchased after January 2019 for cost reasons. In June 2019, a file system without snapshot protection had an unrecoverable data loss due to an accidental deletion of system-layer file data.
**Analysis**: If customer B has created scheduled snapshots for this file system, the data can be recovered to the point in time when the last snapshot was created, thereby minimizing loss. After the incident, customer B created a snapshot for that file system to enhance data protection.

#### Case 3: Using the scheduled snapshot to roll back data and restore business after an incorrect operation

Customer C created snapshots for all file systems. In May 2019, a startup exception occurred due to an incorrect operation.
**Analysis**: Customer C promptly restored data using the scheduled snapshot that was created two days ago, and the business remains stable.


These cases all involve data loss due to incorrect operations, but the results are different. By comparison, we can find that:

- In situations where **a snapshot hasn’t been created**, data is rarely recoverable when a server or file system exception occurs, resulting in major loss.
- In situations where **a snapshot has been created**, data can be recovered when a server or file system exception occurs, minimizing loss.

We recommend regularly creating snapshots for businesses based on business types, enhancing data security and achieving low-cost, high-efficiency disaster recovery.





