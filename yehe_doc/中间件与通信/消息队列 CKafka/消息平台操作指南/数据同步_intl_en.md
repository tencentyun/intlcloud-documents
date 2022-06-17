## Overview

For applications with high requirements for service continuity, data reliability, and compliance, **CKafka Pro Edition** provides the data sync feature to help enhance your capability to deliver continued services and improve data reliability. This feature supports two task types: data sync and cross-region disaster recovery, as detailed below.

- **Data sync**: It syncs data at the topic level and supports data transfer and automatic sync between any topics of different CKafka instances.
- **Cross-region disaster recovery**: It syncs data at the instance level and supports data replication and migration between instances in different regions, where all data and metadata of the instances will be synced.

>?Currently, the data sync feature is only available for CKafka Pro Edition instances but not Standard Edition instances.

## Directions

### Creating data sync task

<dx-tabs>

::: Data sync

**Prerequisites**: You need to first create the target instance and topic. <br>

**Directions:**

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka/index?rid=1).
2. Select **Data Sync** on the left sidebar, select the **region**, and click **Create**.
3. Enter the task name in the **Create Task** pop-up window and select **Data sync** as the task type.
   ![](https://qcloudimg.tencent-cloud.cn/raw/cacc6ebc0a8b25628a487baa7cd3407f.png)
4. Click **Next**, select the **Source Instance Region**, **Source Instance**, **Source Topic**, **Type of Data to Be Synced**, and set the topic offset.
> ?
>
> - When metadata needs to be synced, if two parameters don't meet the conditions, the sync cannot be performed.
> - The partition count cannot be synced as the partition count of the target topic is greater than that of the source topic.
> - The replica count cannot be synced as the replica count of the source topic differs from that of the target topic.
> 
 ![](https://qcloudimg.tencent-cloud.cn/raw/cf9a60e1cacd47eaf3bcd8341760295e.png)
5. Click **Next** and select the **Target Instance Region**, **Target Instance**, and **Target Topic**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/9401e31c5e14316e79e656537fe2ddfc.png)
6. Click **Submit** to complete the task creation. You can view the created data sync task on the **Data Sync** page.
> ?Data sync will automatically start in real time after the task is created. You can view the data sync progress as instructed in [Viewing task progress](#msg).
> 
![](https://qcloudimg.tencent-cloud.cn/raw/e25942e24feb2d9049ff13e524f09cd3.png)



:::

::: Cross-region disaster recovery

**Prerequisites:** You need to first select a target region other than the production environment for disaster recovery and create a CKafka instance with the same specification as the source instance in this region. For detailed directions, see [Creating Instance](https://intl.cloud.tencent.com/document/product/597/39718).<br>
**Directions:**

1. Log in to the [CKafka console](https://console.cloud.tencent.com/ckafka).
2. Select **Cross-region Disaster Recovery** on the left sidebar and click **Create Task**.
3. Enter the task name in the **Create Task** pop-up window and select **Cross-region disaster recovery** as the task type.
   ![](https://qcloudimg.tencent-cloud.cn/raw/c3117152a6a342beb229096903cc0cd1.png)
   1. Click **Next**, select the **Source Instance Region** and **Source Instance**, and set the topic offset.
![](https://qcloudimg.tencent-cloud.cn/raw/963fd63baf46122ea6400d1d2f1ba88f.png)
   2. Click **Next** and select the **Target Instance Region** and **Target Instance**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/c1253b13b7d294376a92901505cee925.png)
4. Click **Submit**, and you can view the created task on the **Data Sync** page.
>?Data sync will automatically start in real time after the task is created. You can view the data sync progress as instructed in [Viewing task progress](#msg).


:::
</dx-tabs>

[](id:msg)
### Viewing task progress

Prerequisites: A data sync task has been created.

1. On the **[Data Sync](https://console.cloud.tencent.com/ckafka/backup)** page, click the ID of the target task to enter the task details page.
2. Select the **Sync Progress** tab to view the data sync progress.
   - **Data Sync**: This tab shows the sync progress of each topic.
![](https://qcloudimg.tencent-cloud.cn/raw/fbae3f58ab5474c5315ba1372dee3e40.png)
   - **Metadata Sync**: This tab shows the sync progress of each topic, ACL policy, user, and consumer group.
     ![img](https://main.qcloudimg.com/raw/0a9689adf89ce1373c4183fd006c5631.png)

### Pausing task

>?A running task can be paused. If you find that the data sync service affects the normal use of CKafka, you can pause data sync.

On the **[Data Sync](https://console.cloud.tencent.com/ckafka/backup)** page, click **Pause** in the **Operation** column of the target task to pause the task.

### Resuming task

>?A paused task can be resumed to continue syncing data from where the sync paused.

On the **[Data Sync](https://console.cloud.tencent.com/ckafka/backup)** page, click **Resume** in the **Operation** column of the to target task to resume the task.

### Deleting task

>!
>
>- Deleting a task means stopping data sync without affecting the synced data and relevant CKafka instances.
>- A task cannot be recovered once deleted. Proceed with caution.

On the **[Data Sync](https://console.cloud.tencent.com/ckafka/backup)** page, click **Delete** in the **Operation** column of the target task to delete the task.
