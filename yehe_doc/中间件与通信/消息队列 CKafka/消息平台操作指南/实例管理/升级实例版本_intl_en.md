CKafka supports upgrading the open-source version of instances to the latest version for more features. It also supports upgrading the kernel minor version to use new features, improve the performance, and fix bugs.

> ?Currently, only CKafka Pro Edition instances in Changsha, Moscow, Frankfurt, and Singapore regions support version upgrade.



## Overview

- Automatic upgrade **(kernel minor version)**

  - Scenario 1: When a severe bug or security vulnerability occurs in CKafka, the system will perform kernel minor version upgrade during the maintenance time and send upgrade notifications through the Message Center and SMS.
  - Scenario 2: When a CKafka cluster is migrated due to cluster configuration upgrade, storage capacity expansion/reduction or CKafka version upgrade, the system will automatically upgrade the cluster's kernel to the latest minor version.

- Manual upgrade **(kernel minor version + open-source Kafka version)**

  You can also manually upgrade the kernel minor version and open-source Kafka version in the console.



## Notes

- Cluster switch will be required after version upgrade is completed (that is, the instance may be disconnected for seconds). We recommend you use applications configured with an automatic reconnection feature and conduct the switch during the instance maintenance time.
- Instances can be upgraded from an earlier version to a later one but cannot be downgraded.
- During minor version upgrade, the system will automatically detect the minor version, and you cannot select a target version.
- If an instance is upgraded to a compatible version, no billing changes will be caused.



## Directions

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Click **Instance List** on the left sidebar and click the **ID/Name** of the target instance to enter the basic information page.
3. In the **Basic Info** module, click **Upgrade Version** on the right of the instance version, and set the target version and upgrade time.
   ![](https://qcloudimg.tencent-cloud.cn/raw/3e504214b48b9a7d8a4965b3c1e7603c.png)
   - Upgrade the kernel minor version:
     - Current Version: The current kernel version.
     - Target Version: The latest broker version is upgraded to by default. The system will automatically detect the minor version. If the **Upgrade Minor Version** button is grayed out, the instance is already on the latest minor version. For differences between kernel minor versions, see [here](https://intl.cloud.tencent.com/document/product/597/48385).
     - Execution Time: You can select **Immediate execution** or **Custom time** (any time within the next 24 hours). We recommend you select a time during off-peak hours.
   - Upgrade the Kafka version:
     - Current Version: The current Kafka version.
     - Target Version: Select the target Kafka version. For differences between Kafka versions, see [DOWNLOAD](https://kafka.apache.org/downloads).
     - Execution Time: You can select **Immediate execution** or **Custom time** (any time within the next 24 hours). We recommend you select a time during off-peak hours.
4. Click **OK** to submit the upgrade task.
5. Select the **Event Center** tab at the top of the page, and you can see a record of instance version upgrade.
   ![](https://qcloudimg.tencent-cloud.cn/raw/c68eaca94229e9589fa03a1743d289a4.png)
6. Click **View Details** in the **Operation** column of the record to view the detailed upgrade task progress.
![](https://qcloudimg.tencent-cloud.cn/raw/401662af979fd49586b091ac13880aae.png)
7. Return to the instance list page. You can see that the status of the instance has changed to **Changing configurations...**, and you can also view the upgrade progress.

   

