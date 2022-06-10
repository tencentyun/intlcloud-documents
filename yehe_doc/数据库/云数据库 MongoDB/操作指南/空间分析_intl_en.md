## Overview
TencentDB for MongoDB supports connection to DBbrain to analyze the computing and storage specifications of the mongod node. You can view the instance space utilization, including the sizes of data and logs, the daily increase in space utilization, the estimated number of available days, and the space used by the tables and databases of the instance. 

## Prerequisites
- You have [created a TencentDB for MongoDB instance](https://intl.cloud.tencent.com/document/product/240/3551).
- The TencentDB for MongoDB replica set or sharded instance is in **Running** status.

## Directions
1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Instance ID/Name** column of the target instance, click the instance ID in blue font to enter the **Instance Details** page.
6. In the **Configuration Info** section on the **Instance Details** page, click **Space Analysis** after **mongod Specs**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/413495df598c0f4c6d56154b03526abc.png" style="zoom:80%;" />
7. On the space analysis page in the [DBbrain console](https://console.cloud.tencent.com/dbbrain), analyze the space usage details of the mongod node.

