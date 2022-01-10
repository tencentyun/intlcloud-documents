## Overview

For applications with high requirements for service continuity, data reliability, and compliance, **CKafka Pro Edition** provides the data sync feature to help enhance your capability to deliver continued services and improve data reliability. This feature supports two task types: data sync and cross-region disaster recovery, as detailed below.

- **Data sync**: it syncs data at the topic level and supports data transfer and automatic sync between any topics of different CKafka instances.

- **Cross-region disaster recovery**: it syncs data at the instance level and supports data replication and migration between instances in different regions, where all data and metadata of the instances will be synced.

>?Currently, only CKafka Pro Edition instances support the data sync feature.

## Directions

### Creating data sync task

<dx-tabs>

::: Data sync

**Prerequisites**: you need to first create the target instance and topic. <br>

**Directions:**

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka/index?rid=1).

2. Select **Data Sync** on the left sidebar, select the **region**, and click **Create**.

3. Enter the task name in the **Create Task** pop-up window and select **Data sync** as the task type.

   ![](https://qcloudimg.tencent-cloud.cn/raw/cacc6ebc0a8b25628a487baa7cd3407f.png)

4. Click **Next**, select the source instance region, source instance, and source topic, and select the **data types to be synced**.
> ?
> - When metadata needs to be synced, if two parameters don't meet the conditions, the sync cannot be performed.
> - If the number of partitions of the target topic is greater than that of the source topic, the partitions cannot be synced.
> - If the numbers of replicas of the source and target topics are different, the replicas cannot be synced.
>
![](https://qcloudimg.tencent-cloud.cn/raw/c2032b7f9aa8a323164ec5b2652a13c9.png)

5. Click **Next** and select the target instance region, target instance, and target topic.

   ![](https://qcloudimg.tencent-cloud.cn/raw/5da39dcc94d8ceabd4c4b94bf365929a.png)

6. Click **Submit** to complete the task creation. You can view the created data sync task on the **Data Sync** page.
> ?After the task is successfully created, data sync will start automatically, and the data will be replicated in real time. You can view the data sync progress as instructed in [Viewing sync progress](https://intl.cloud.tencent.com/document/product/597/32556).
>
![](https://qcloudimg.tencent-cloud.cn/raw/25a04cb7d37e54000702b4d0df93f7c6.png)



:::

::: Cross-region disaster recovery

**Prerequisites**: you need to first select a target region other than the production environment for disaster recovery and create a CKafka instance with the same specifications as the source instance in this region. For more information, see [Creating Instance](https://intl.cloud.tencent.com/document/product/597/39718).<br>
**Directions:**

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Select **Cross-region Disaster Recovery** on the left sidebar and click **Create Task**.
3. Enter the task name and select the source and target instances.
   ![img](https://main.qcloudimg.com/raw/3ca26629164ab4cdbef1d38a500f6123.png)
4. Click **Submit**, and you can view the created cross-region disaster recovery task on the **Data Sync** page.
> ?After the task is successfully created, data sync will start automatically, and the data will be replicated in real time. You can view the data sync progress as instructed in [Viewing task progress](https://intl.cloud.tencent.com/document/product/597/32556).

:::
</dx-tabs>

### Viewing sync progress

Prerequisites: a data sync task has been created.

1. On the **[Data Sync](https://console.cloud.tencent.com/ckafka/backup)** page, click the "ID" of the target task to enter the task's basic information page.
2. Select the **Sync Progress** tab to view the data sync progress.
   - **Data Sync**: this tab shows the sync progress of each topic.
     ![img](https://main.qcloudimg.com/raw/702b0d604083215382582cb780f0a967.png)
   - **Metadata Sync**: this tab shows the sync progress of each topic, ACL policy, user, and consumer group.
     ![img](https://main.qcloudimg.com/raw/0a9689adf89ce1373c4183fd006c5631.png)

### Pausing task

>?A running task can be paused. If you find that the data sync service affects the normal use of CKafka, you can pause data sync.

On the **[Data Sync](https://console.cloud.tencent.com/ckafka/backup)** page, click **Pause** in the **Operation** column to pause the task.

### Resuming task

>?A paused task can be resumed to continue syncing data from where the sync paused.

On the **[Data Sync](https://console.cloud.tencent.com/ckafka/backup)** page, click **Resume** in the **Operation** column to resume the paused task.

### Deleting task

>!
> - Deleting a task means stopping data sync without affecting the synced data and relevant CKafka instances.
> - A task cannot be recovered once deleted. Proceed with caution.

On the **[Data Sync](https://console.cloud.tencent.com/ckafka/backup)** page, click **Delete** in the **Operation** column to delete the task.

