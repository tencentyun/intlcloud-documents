Tencent Cloud CSS console provides the relay feature. If you cannot use your live streaming source to push or you want to use on-demand videos for live streaming, you can use the relay feature to quickly pull contents from an existing live streaming source or videos and then push them to the destination URL, with no need for live push.
![](https://main.qcloudimg.com/raw/8f0b044ce2104efdc1ed835287b9b683.png)

## Prerequisites
- You have activated [CSS](https://intl.cloud.tencent.com/product/css) and logged in to the CSS console.
- You have added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970) in the console.

## Notes
- You can create up to **20** relay tasks.
- The relay feature is charged based on the **duration of relay tasks**. For details, see [Relay](https://intl.cloud.tencent.com/document/product/267/41059).
- Relay only pulls and pushes contents. **Please ensure that the contents have been authorized and comply with the laws and regulations for distribution. If the contents infringe relevant rights or violate regulations, CSS will suspend related features and reserve the right to take legal action**.

[](id:create)
## Creating Task
1. Go to **CSS Toolkit** > **[Relay](https://console.cloud.tencent.com/live/tools/relay)**, and click **Create Task**.
![](https://qcloudimg.tencent-cloud.cn/raw/4328e092758efd15d6436837dc618f50.png)
2. Enter the basic information of the task:
![](https://qcloudimg.tencent-cloud.cn/raw/018e81846aa6bad9686fdb7884889b5c.png)
<table>
<tr><th width="15%">Configuration Item</th><th>Description</th>
<tr>
<td>Task Description</td>
<td>Custom task description.</td>
</tr><tr>
<td>Execution Time</td>
<td>The default execution time is from the <code>current time</code> to <code>24 hours later</code>. You can select a time range not longer than 7 days, and the start time cannot be later than 1 year from the current time. <br>Suppose the current time is 2021-3-24 11:50:01. <ul style="margin:0"><li/>You can select a time range between 2021-3-24 11:50:01 and 2022-3-30 11:50:01.<li/>The end time cannot be later than 2022-3-30 11:50:01.</ul></td
</tr><tr>
<td>Region</td>
<td><ul style="margin:0"><li/>You can select a region for the task. You can choose North China (Beijing), East China (Shanghai), South China (Guangzhou), Southeast Asia (Singapore), Southeast Asia (Thailand), Northeast Asia (Korea), and South Asia (India). <li/><b>If you select “Random”, the system will automatically assign the nearest region. </b></ul></td>
</tr><tr>
<td>Event Callback Notification</td>
<td>Enter a callback URL for receiving relay task event notifications. </td>
</tr></table>

3. Select **Live streaming** or **Video on demand** as the content type:
   - If you select **Live streaming**, you need to enter only **1** live streaming source URL.
   ![](https://qcloudimg.tencent-cloud.cn/raw/319311810174f09ac2286f7ff5350250.png)
   - If you select **Video on demand**:
      - You can enter **multiple** (max 30) source URLs.
      - You can select **Repeat** or **Specified** (min: 1; max: 100) for the playback count.
      ![](https://qcloudimg.tencent-cloud.cn/raw/8a94ddbcc7dc2c612ce39e35e0e0b379.png)
>? 
>- The system will stop the relay task either when the playback count reaches the specified value or when the task reaches its end time.
>- Changing task information:
    - If you change the playback count, the current playback will be counted as 1 when the new value is applied.
    - If you change both the source URL and playback count, the current playback will not be counted and the new value will be applied, regardless of whether you choose to apply the change after the current video ends or now.
    - If you change the destination URL, the playback count will be reset.
4. Enter a destination URL for receiving the content.
   1. Click **Address Generator** to enter the URL generation page.
   ![](https://qcloudimg.tencent-cloud.cn/raw/59b8cf4d58770d201190db7404f6b5ad.png)
   2. Select an existing push domain name, enter the `Appname`, `StreamName`, and expiration time, and click **Confirm** to generate a push URL, which will be auto-filled as **Destination Address**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b01df24dffa14c35350048ae7fd3cfef.png)
    >! The URL expiration time must be later than the task end time. If you change the destination URL after the task starts, it will stop and restart.
5. Click **Save**.

## Managing Tasks
[](id:view)
### Viewing task details
In the [task list](https://console.cloud.tencent.com/live/tools/relay), find your task, and click its description/ID to view task details in the pop-up.
![](https://qcloudimg.tencent-cloud.cn/raw/8fa3d70b6fe0d961048cc508ea72ca4b.png)

>? You can click **Edit** or **Disable** to [modify](#change) or [disable](#disable) a task.

[](id:change)
### Modifying a task
1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), find the task you want to modify, and click **Edit**.
![](https://qcloudimg.tencent-cloud.cn/raw/97b07fc0d224a06fe268cdc1177102e3.png)
2. Modify the task information, and then click **Save**.
>!
>- You cannot change the region or content type.
>- When modifying the task end time, make sure that the destination URL is valid until the task ends. Modifying the destination URL will cause the task to stop and restart.

![](https://qcloudimg.tencent-cloud.cn/raw/d950a8029e1944e9029445dd8e428933.png)
3. Compare the information before and after change in the pop-up:
  - Changes in the following example include **Task Description**, **Execution Time**, **Event Callback Notification**, and **Playback Count**:
![](https://qcloudimg.tencent-cloud.cn/raw/4cadcabeef99828ab4be144040cbfd19.png)
  - If the source URLs for **Video on demand** are changed, you need to select whether to apply the change **After the current video ends** (default) or **Now**. After the changes take effect, relay will restart from the first source URL.
![](https://qcloudimg.tencent-cloud.cn/raw/9591b91b7e5e307860c9ea2244b4e14e.png)
   - If **Destination Address** is changed, the system will remind you that after you click **Confirm**, the current relay task will **stop and restart**.
![](https://qcloudimg.tencent-cloud.cn/raw/0a7e04f65ae8bbdd9cb7ef3bc0ece656.png)
4. After checking, click **Confirm**.

[](id:copy)
### Copying a task
1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), find the relay task you want to copy, and click **Copy**. You will be directed to the task creation page.
![](https://qcloudimg.tencent-cloud.cn/raw/28a0a3542ab9ab838d26dfc565f321d1.png)
2. The information of the copied task will be auto-filled. You can [modify](#create) it as needed.
3. Click **Save** to create a new relay task.



[](id:reboot)
### Restarting a task
Restarting a task will **not change its status**. An ongoing task will be **restarted from the beginning**. Perform the following to restart a task:

1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), find the relay task you want to restart, and click **Restart**.
2. In the pop-up, click **Restart**.
![](https://qcloudimg.tencent-cloud.cn/raw/d1b03e226297e44cbb7504d57c54af4f.png)

[](id:disable)
### Disabling a task
If you disable a task, **the task will stop**. You can click **Enable** to start it again. Perform the following to disable a task:

1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), find the relay task you want to disable, and click **Disable**.
2. In the pop-up, click **Disable**.
![](https://qcloudimg.tencent-cloud.cn/raw/c3acfb89f425b50ba53a8d63075091d8.png)


[](id:enable)
### Enabling a task
If you enable a task, **the task will start from the beginning**. Perform the following to enable a task:

1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), find the relay task you want to enable, and click **Enable**.
2. In the pop-up, click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/77417a9c8406fe9d763c4d3960d98b21.png)

[](id:delete)

### Deleting a task
Deleted tasks **cannot be recovered**. Perform the following to delete a task:

1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), find the relay task you want to delete, and click **Delete**.
2. In the pop-up, click **Delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/44a15ad52bfc81f62c0aa907cdc7eb5c.png)

[](id:batch)
### Batch operations
You can delete, disable, and enable relay tasks in batches (**max: 10**).
1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), select the relay tasks you want to delete, disable, or enable.
2. Click **Batch Operation**, and select **Delete**, **Disable**, or **Enable**.
![](https://qcloudimg.tencent-cloud.cn/raw/6b93d5c3af7ec83d9a56840a40a2073a.png)
3. In the pop-up, confirm the information and click **Delete**, **Disable**, or **Enable**.
![](https://qcloudimg.tencent-cloud.cn/raw/5874636c548a4733281cd33eaca35abe.png)

   
