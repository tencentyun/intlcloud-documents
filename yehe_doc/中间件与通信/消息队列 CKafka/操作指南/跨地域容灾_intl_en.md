## Overview

For applications with high requirements of service continuity, data reliability, and compliance, CKafka Pro Edition provides intra-instance replication and migration solutions by deploying disaster recovery systems across regions. When the primary system fails, the business will be switched over to the disaster recovery system, helping you avoid system failures caused by the regional disaster, enhance your capability to deliver continued services at low costs, and improve data reliability.

>?
>- Currently, only CKafka Pro Edition instances can provide the cross-region disaster recovery capability.
>- The cross-region disaster recovery feature is now available in Guangzhou, Beijing, and Tokyo regions. Users in other regions can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to use this feature.

## Prerequisites

You need to first select a target region other than the production environment for disaster recovery and create a CKafka instance with the same specifications as the source instance’s in this region. For details, see [Creating Instance](https://intl.cloud.tencent.com/document/product/597/39718).

## Directions

### Creating a cross-region disaster recovery task

1. Log in to the [CKafka Console](https://console.cloud.tencent.com/ckafka).
2. Select **Cross-region Disaster Recovery** on the left sidebar and click **Create Task**.
3. On the page that appears, enter the task name and select the source and target instances.
   ![](https://main.qcloudimg.com/raw/3ca26629164ab4cdbef1d38a500f6123.png)
4. Click **Submit**, and you can view the created task on the **Cross-region Disaster Recovery** page.
>? Data sync will automatically start in real time after the task is created. You can refer to the steps described in [viewing task progress](#1) to view the data sync progress.
>
![](https://main.qcloudimg.com/raw/f996a826d7e68ff742d986542c0d37c2.png)


### Viewing task progress[](id:1)

1. On the **[Cross-region Disaster Recovery](https://console.cloud.tencent.com/ckafka/backup?rid=4)** page, click the task name to enter the task details page.
2. Select the **Sync Progress** tab to view the data sync progress.
   - **Data Sync**: this tab shows the sync progress of each topic.
   ![](https://main.qcloudimg.com/raw/702b0d604083215382582cb780f0a967.png)
   - **Metadata Sync**: this tab shows the sync progress of each topic, ACL policy, user, and consumer group.
   ![](https://main.qcloudimg.com/raw/0a9689adf89ce1373c4183fd006c5631.png)

### Pausing a task

On the **[Cross-region Disaster Recovery](https://console.cloud.tencent.com/ckafka/backup?rid=4)** page, click **Pause** in the **Operation** column to pause the task.

### Resuming a task

On the **[Cross-region Disaster Recovery](https://console.cloud.tencent.com/ckafka/backup?rid=4)** page, click **Resume** in the **Operation** column to resume the paused task.

### Deleting a task

>!A task cannot be recovered once deleted. Please proceed with caution.

On the **[Cross-region Disaster Recovery](https://console.cloud.tencent.com/ckafka/backup?rid=4)** page, click **Delete** in the **Operation** column to delete the task.

