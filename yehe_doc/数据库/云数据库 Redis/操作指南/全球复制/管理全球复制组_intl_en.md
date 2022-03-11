You can manage a created replication group as needed in your actual Ops use cases. Specifically, you can set read-only instances as master instances, switch the roles of master and read-only instances, remove instances, or delete the replication group.

## Prerequisites
- You have [created a global replication group](https://intl.cloud.tencent.com/document/product/239/45603), and it is in **Running** status.
- You have [added an instance to the replication group](https://intl.cloud.tencent.com/document/product/239/45603), and the instance is in **Running** status.

## Setting Read-Only Instance as Master Instance
You can set a read-only instance in a replication group as a master instance for data writes. This change only updates the instance configuration without causing data migration. The entire process takes approximately three minutes.

For detailed directions, see the following steps:
1. In the [replication group list](https://console.cloud.tencent.com/redis/replication), click <img src="https://qcloudimg.tencent-cloud.cn/raw/3a815073e7ccf4206decf7b522a40ccd.png" style="zoom: 67%;" /> before the name of the target replication group to show its instance list.
2. Find the target read-only instance and click **Set to Master** in its **Operation** column.
> !You can set a ready-only instance as a master instance only if there are at least two read-only instance replicas in the replication group.
> 
![](https://qcloudimg.tencent-cloud.cn/raw/10f9f36c3f5e7c18ccd598673d3c9e74.png)
3. Read the prompt carefully in the **Set to Master** pop-up window and click **OK**.
In the instance list of the replication group, the **instance status** changes to **switching instance role**, and the **instance role** will change to **master instance** after the switch.

## Setting Master Instance as Read-Only Instance
You can also set a master instance added to a replication group to a read-only instance as detailed below.
![](https://qcloudimg.tencent-cloud.cn/raw/7a29d5abcaf379062fb011e8bfb33f37.png)

## [Switching Instance Role](id:qhsljs)
You can switch the master instance only in the disaster recovery use case; that is, there is only one master instance and one read-only instance in the replication group. Usually, the replication group will become inaccessible for one minute during the switch as shown below.
![](https://qcloudimg.tencent-cloud.cn/raw/cd56064d296acbed44024cb33829158d.png)
> !When data is synced to the new master instance (the original read-only instance), it is still available for read access.

See the following steps for how to switch the master instance:
1. In the [replication group list](https://console.cloud.tencent.com/redis/replication), click <img src="https://qcloudimg.tencent-cloud.cn/raw/3a815073e7ccf4206decf7b522a40ccd.png" style="zoom: 67%;" /> before the name of the target replication group to show its instance list.
2. Find the target read-only instance and click **Switch with Master Instance** in its **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/b20ca448e8061ff1d472e026ed0093d8.png)
3. Read the prompt carefully in the **Switch with Master Instance** pop-up window and click **OK**.
4. Both the master and read-only instances in the replication group enter the **switching with master instance** status. Wait for the switch to complete and then you can see that the original master instance is read-only, while the original read-only instance is now the master instance.

## Removing Instance from Replication Group
You can remove an instance from the replication group. The removed instance will stop syncing data from other instances in the replication group.

See the following steps for how to remove an instance from a replication group:
1. In the [replication group list](https://console.cloud.tencent.com/redis/replication), click <img src="https://qcloudimg.tencent-cloud.cn/raw/3a815073e7ccf4206decf7b522a40ccd.png" style="zoom: 67%;" /> before the name of the target replication group to show its instance list.
2. Find the target instance and click **Remove from Replication Group** in its **Operation** column.
> !You cannot remove an instance if it is the only master instance in the replication group where read-only instances exist.
3. In the **Remove from Replication Group** pop-up window, confirm the instance information.
If the instance to be removed is a master instance, you need to select a **removal mode** and click **OK**.
   - **Remove now**: In this mode, the system disconnects data sync within the replication group immediately, without waiting for other nodes to complete data sync from this master instance. Some data may be lost.
   - **Upon data sync completion**: In this mode, the system sets the master instance as read-only, waits for other nodes in the replication group to complete data sync from it, disconnects the replication between it and all other nodes in the replication group, removes it from the replication group, cancels its read-only status, and then enables its write access.
4. In the instance list of the replication group, the **instance status** changes to **removing instance**. Wait for the removal to complete.

## Deleting Replication Group
You need to remove all instances in a replication group before you can delete it.

1. In the [replication group list](https://console.cloud.tencent.com/redis/replication), select the target replication group and click **Delete Replication Group** in its **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/a3d9cc9c83d7fb18fba127720d00d417.png)
2. In the **Delete Replication Group** pop-up window, confirm the replication group information and click **OK**.

