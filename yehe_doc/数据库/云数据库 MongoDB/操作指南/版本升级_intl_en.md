TencentDB for MongoDB supports database version upgrade from 3.6 to 4.0.

## Version Requirement
Currently, only TencentDB for MongoDB 3.6 can be upgraded to 4.0, while other versions cannot. For version differences, see [Storage Engine and Version](https://intl.cloud.tencent.com/document/product/240/31706).

## Notes
The upgrade process is completely automatic, and there will be several second-level interruptions during the process. It is recommended to upgrade during off-peak period. 

## Prerequisites
- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded instance is on v3.6 and in **Running** status.
- The instance is not a read-only or disaster recovery instance.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
In the **Version and Engine** column, you can view the version of the instance.
5. In the **Instance ID/Name** column of the target instance, click the instance ID in blue font to enter the **Instance Details** page.
6. In the **Configuration Info** section on the **Instance Details** page, click **Upgrade to v4.0** after **Version and Engine**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c0a16832eda32515aab81202e4ea7980.png" style="zoom:50%;" />
7. In the pop-up window, read the prompt message carefully, confirm the upgrade, and click **OK**.
