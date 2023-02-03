## Overview

TencentDB for MongoDB allows you to upgrade both the major and minor database versions. You can enjoy more features by upgrading the major version from v3.6 to v4.0 or from v4.0 to v4.2. 

## Version description

- You can upgrade the MongoDB major version from v3.6 to v4.0 or from v4.0 to v4.2.
- You can also upgrade the minor version, for example, the minor version WT.40.3.34 of the major version 4.0.
- During minor version upgrade, the system will automatically detect the minor version and upgrade to the latest version, and you cannot select a target version.
- Cross-major version upgrade isn't supported. For example, you cannot upgrade the major version from v3.2 to v4.0. For version differences, see [Storage Engine and Version > Version Description](https://www.tencentcloud.com/document/product/240/31706#bbsm).

>?You can implement the upgrade of major version from v3.2 to v4.0 through data migration. For more information, see [Migration from MongoDB to TencentDB for MongoDB](https://www.tencentcloud.com/document/product/571/42639).

## Notes

The upgrade process is completely automatic, and there will be several momentary interruptions during the process. We recommend that you upgrade during off-peak hours.

## Prerequisites

- The instance is not a read-only or disaster recovery instance.
- The instance to be upgraded is in **Running** status and is not executing any tasks.
- The target version is confirmed.

## Directions

1. Log in to the [TencentDB for MongoDB console](https://console.cloud.tencent.com/mongodb).
2. In the **MongoDB** drop-down list on the left sidebar, select **Replica Set Instance** or **Sharded Cluster Instance**. The directions for the two types of instances are similar.
3. Above the instance list on the right, select the region.
4. In the instance list, find the target instance.
5. In the **Instance ID/Name** column of the target instance, click the instance ID to enter the **Instance Details** page.
6. In the **Specs Info** section on the **Instance Details** page, upgrade the major or minor version of the instance.
 - If the major version of the instance is **3.6**, click **Upgrade to v4.0** after **Version and Engine** to upgrade the version from v3.6 to v4.0.
 - If the major version of the instance is **4.0**, click **Upgrade to v4.2** after **Version and Engine** to upgrade the version from v4.0 to v4.2.
 - Click **Upgrade Minor Version** to upgrade the minor version to the latest version by default. For more information, see [Storage Engine and Version > Minor Version Description](https://www.tencentcloud.com/document/product/240/31706#xbbsm).
 ![](https://staticintl.cloudcachetci.com/yehe/backend-news/FKVS509_38-en.png)
7. In the **Note** pop-up window, read the prompt message carefully, confirm the upgrade, and click **OK**.

