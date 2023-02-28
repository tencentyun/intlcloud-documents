## Overview
A snapshot is a file that contains the data of a specified CVD instance at a specified time point, which can be used for data backup and recovery. CVD provides the snapshot feature for system disks and data disks to mitigate data losses caused by misoperations by end users.

Currently, snapshots are created automatically for the system and data disks of each CVD instance between 2:00 AM and 4:00 AM every day. Created snapshots are displayed in the snapshot list. The creation process does not affect the normal use of CVD instances.

## Directions 
### Rolling back a snapshot
When a data error occurs or data is lost, you can roll back the snapshot data, so that data in the CVD instance can be restored to the status when the snapshot is created.
1. Log in to the [CVD console](https://console.cloud.tencent.com/cvd).
2. On the **Desktop List** page, select the target CVD instance and click **Desktop ID** on the left to enter the CVD instance details page.
![](https://qcloudimg.tencent-cloud.cn/raw/cf162b99cc9906d089784471715b5942.png)
3. On the CVD instance details page, select the **Snapshots** tab on the right of the topbar. Then, select the target snapshot and click **Roll back** in the **Operation** column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/714c8ee5fd25976c48807196be62fab6.png)
4. Confirm the rollback, which will clear the current data of the CVD instance. Read the notes, toggle on **Force shut down**, and click **Confirm**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/42ae311db2c39da8dee02425e8a0983b.png" style="zoom:50%;" />

### Deleting a saved snapshot
Snapshots are deleted automatically after three days. If you are sure that certain snapshots are no longer needed, you can manually delete them to release virtual resources.
1. Log in to the [CVD console](https://console.cloud.tencent.com/cvd).
2. On the **Desktop List** page, find the target CVD instance and click the **Desktop ID** on the left to enter the CVD instance details page.
![](https://qcloudimg.tencent-cloud.cn/raw/bde5a7b80bbd1dc82ec7186abb55a35e.png)
3. On the CVD instance details page, select the **Snapshots** tab on the right of the topbar. Then, select the target snapshot and click **Delete** in the **Operation** column on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/3afa22f0e3c0a814b18799aa62ed3392.png)
4. Deleted snapshots cannot be recovered. If you are sure about deleting a snapshot, select **I have read the following: Deleted snapshots cannot be recovered. Please ask the user to back up their data first.** and click **Confirm**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c9ad3f50bdf42ef3a8f12dbe8a4f10d2.png" style="zoom:69%;" />

