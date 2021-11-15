
Binlog grows fast when a TencentDB for MySQL instance executes large transactions or lots of DML operations. MySQL’s data synchronization is based on binlog which ensures database restorability, stability, and high availability,

Before this upgrade, binlog files were stored in a special space provided by Tencent Cloud. As the speed of writing to binlog affects database performance, TencentDB for MySQL migrates the binlog files to high-performance SSDs (i.e., instance disk space), in order to improve database performance and stability.

## Upgrade Impact
This upgrade is applicable to two-node and three-node TencentDB for MySQL instances.

### Storage space
- After binlog files are migrated to high-performance SSDs, they will take up the [disk space of your instance](https://intl.cloud.tencent.com/document/product/236/18335).
- By default, TencentDB for MySQL binlog files are stored locally (that is, in instance disk space) and automatically deleted when the retention period has elapsed. For more information, please see [Configuring Local Binlog Retention Policy](https://intl.cloud.tencent.com/document/product/236/40186).
>?When a binlog file is generated, it is backed up via the [automatic backup feature](https://intl.cloud.tencent.com/document/product/236/37796) and its backup will be uploaded to COS.

### Monitored metrics
After the upgrade starts, the space taken up by binlog files will be counted into the total used disk space, which may trigger alarms. We recommend the available disk space be larger than 20%.

## Start Time of the Upgrade
- Two-node and three-node TencentDB for MySQL in Hong Kong/Macao/Taiwan (Hong Kong, China) and regions outside the Chinese mainland: 00:00:00, April 1, 2021 (UTC+8).
- Two-node and three-node TencentDB for MySQL in Southwest China (Chengdu and Chongqing): 00:00:00, April 7, 2021 (UTC+8).
- Two-node and three-node TencentDB for MySQL in North China (Beijing): 00:00:00, April 14, 2021 (UTC+8).
- Two-node and three-node TencentDB for MySQL in East China (Shanghai): 00:00:00, April 19, 2021 (UTC+8).
- Two-node and three-node TencentDB for MySQL in South China (Guangzhou): 00:00:00, April 21, 2021 (UTC+8).
- Two-node and three-node TencentDB for MySQL in newly supported regions: 00:00:00, April 22, 2021 (UTC+8).

## Suggestions on Reducing Local Binlog Space
You can shorten the local binlog retention period in the console. For more information, please see [Configuring Local Binlog Retention Policy](https://intl.cloud.tencent.com/document/product/236/40186).

## FAQs
#### Will the instance expansion and reduction be affected during the upgrade?
No. Before the upgrade, the instance expansion/reduction is based on the space taken up by data files.
After the upgrade, the instance expansion/reduction is based on the total used disk space and will notify you via SMS, Message Center, etc.

#### Will any features be affected by the upgrade?
Currently, only the disk space utilization alarm is affected. Before the upgrade, the disk space utilization is calculated by "data file size/total disk space"; after the upgrade, it is calculated by "total used disk space/total disk space".

