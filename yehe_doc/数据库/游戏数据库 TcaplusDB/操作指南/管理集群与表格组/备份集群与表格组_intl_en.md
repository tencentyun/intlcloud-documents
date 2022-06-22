 
This document describes how to back up a cluster and a table group in the TcaplusDB console.

## Prerequisites
You have created a cluster and a table group as instructed in:
- [Creating Cluster](https://intl.cloud.tencent.com/document/product/1016/32714)
- [Creating Table Group](https://intl.cloud.tencent.com/document/product/1016/32716)

## Backup Settings
### Cluster
There are two types of clusters: dedicated and non-dedicated. They have different backup retention period settings as detailed below.

#### Dedicated cluster
For a dedicated cluster, you can modify the data retention period (N) and database operation log retention period (M). Both N and M are seven days by default, and N must be greater than or equal to M. Backups will be automatically deleted upon expiration.

#### Non-dedicated cluster
For a non-dedicated cluster, the database operation log retention period is fixed at seven days. Backups will be automatically deleted upon expiration.
The data retention period (N) is seven days by default and can be modified. If N is less than or equal to 7, data can be rolled back to any time point within N days. If N is greater than 7, data can be rolled back to any time point within the first seven days and only to an automatic (cold) backup time point afterwards. Backups will be automatically deleted upon expiration.

#### Cluster settings
1. Go to the [Cluster List](https://console.cloud.tencent.com/tcaplusdb/app) page and click **Backup Settings** in the **Operation** column.
2. In the **Backup Settings** pop-up window, modify the backup retention period and click **OK**.

### Table group
For a table group, the database operation log retention period is fixed at seven days. Backups will be automatically deleted upon expiration.
The data retention period (N) is seven days by default and can be modified. If N is less than or equal to 7, data can be rolled back to any time point within N days. If N is greater than 7, data can be rolled back to any time point within the first seven days and only to an automatic (cold) backup time point afterwards. Backups will be automatically deleted upon expiration.

#### Table group settings
1. Go to the [Cluster List](https://console.cloud.tencent.com/tcaplusdb/app) page, select the target cluster and table group, and click **More** > **Backup Settings** in the **Operation** column of the table group.
2. In the **Backup Settings** pop-up window, modify the backup retention period and click **OK**.

### Backup policy priority
A cluster contains table groups and a table group contains tables. When their backup policies conflict, the table policy has the highest priority, followed by the table group policy and then the cluster policy, as detailed below. "&#10003;" indicates that a backup policy has been configured at the particular level, while "-" indicates not.

| Cluster Policy | Table Group Policy | Table Policy | Effective Policy |
| -------- | ---------- | -------- | ---------- |
| &#10003;         | -          | -        | Cluster policy   |
| -        | &#10003;           | -        | Table group policy |
| -        | -          | &#10003;         | Table policy   |
| &#10003;         | &#10003;           | -        | Table group policy |
| &#10003;         | -          | &#10003;         | Table policy   |
| &#10003;         | &#10003;           | &#10003;         | Table policy   |

For example, if a cluster policy is configured, there are three table groups (1, 2, 3) in the cluster, and only table group 1 has the retention period configured, then table group 1 will follow its own policy, while table groups 2 and 3 will inherit the cluster policy since they don't have specific table group policies.

Similarly for tables, only if a table policy is configured for table A will table A follow the configured policy, while tables without a table policy will inherit the policy at the upper level.

## Automatic Backup
TcaplusDB automatically backs up clusters and table groups between 02:00 and 06:00 every day.

## Backup History
Go to the [Table List](https://console.cloud.tencent.com/tcaplusdb/table) page, click a table ID to enter the table backup page, and view the table's backup history in the **Data Backup List**.

Among them,
- Only the automatic backup method is available for clusters and table groups.
- **Backup File Quantity** indicates the number of stored files into which this data backup is divided.
- **File Size** indicates the size of the backup file.
- **Backup Time** indicates the time when the backup task was started.
- **File Expiration Time** indicates the expiration time of the backup file, after which the file will be automatically deleted by the system.
- **Backup Status** shows the result (successful or failed) of the backup task.

