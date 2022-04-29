Tencent Cloud CSS console provides the relay feature. If you cannot use your live streaming source to push or you want to use on-demand videos for live streaming, you can use the relay feature to quickly pull contents from an existing live streaming source or videos and then push them to the destination URL, with no need for live push.
![](https://main.qcloudimg.com/raw/8f0b044ce2104efdc1ed835287b9b683.png)

## Prerequisites
- You have activated [CSS](https://cloud.tencent.com/product/css) and logged in to the CSS console.
- You have added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970) in the console.

## Limits
- You can create up to **20** relay tasks.
- The relay feature is charged based on the **duration of relay tasks**. For details, see [Relay](https://intl.cloud.tencent.com/document/product/267/41059).
- Relay only pulls and pushes contents. **Please ensure that the contents have been authorized and comply with the laws and regulations for distribution. If the contents infringe relevant rights or violate regulations, CSS will suspend related features and reserve the right to take legal action**.

[](id:create)
## Creating a Task
1. Go to **CSS Toolkit** > **[Relay](https://console.cloud.tencent.com/live/tools/relay)**, and click **Create Task**.
![](https://qcloudimg.tencent-cloud.cn/raw/f41c7a329a9fed7a901bca252a973f35.png)
2. Enter the basic information of the task:
![](https://qcloudimg.tencent-cloud.cn/raw/d10fb06aba921e27791441a112039586.png)
<table>
<tr><th width="15%">Configuration Item</th><th>Description</th>
<tr>
<td>Task Description</td>
<td>Provide a description of the task.</td>
</tr><tr>
<td>Execution Time</td>
<td>The default execution time is from the <code>current time</code> to <code>24 hours later</code>. You can select a time range not longer than 7 days, and the start time cannot be later than 1 year from the current time. <br>Suppose the current time is 2021-3-24 11:50:01. <ul style="margin:0"><li/>You can select a time range between 2021-3-24 11:50:01 and 2022-3-30 11:50:01.<li/>The end time cannot be later than 2022-3-30 11:50:01.</ul></td
</tr><tr>
<td>Event Callback Notification</td>
<td>Enter a callback URL for receiving relay task event notifications. </td>
</tr></table>
3. Provide the content source information.
      - Region: Random (Chinese mainland), North China region (Beijing), East China (Shanghai), South China (Guangzhou), Southeast Asia (Singapore), Southeast Asia (Bangkok), Northeast Asia (Seoul), South Asia (Mumbai), Hong Kong
      - If you select **Random (Chinese mainland)**, the system will assign a region that is nearby.
4. For **Content Type**, you can select **Live streaming** or **Custom video path**.
   - **Live streaming**:
     - Enter a live streaming URL (**only one** is allowed).
   ![](https://qcloudimg.tencent-cloud.cn/raw/6795d964f41e63fa90f0c09e3ddcf060.png)
     - If you select **Enable backup**, when the system fails to pull content from the primary source, it will automatically switch to the backup source. After the primary recovers, you need to manually switch back. Backup sources support only loop of a single video.
   - **Custom video path**:
      - You can enter **multiple** (max 30) source URLs.
      - Select **Repeat** to repeat the playback indefinitely or **Specified** to specify the number of times (1-100) to play the content.
      ![](https://qcloudimg.tencent-cloud.cn/raw/154e880ea3f2a60eef9031c7cba11510.png)
>? 
>- The system will stop the relay task either when the playback count reaches the specified value or when the task reaches its end time.
>- After modifying a task:
     - If you change only the playback count, after the new value is applied, the count will start from 2.
	  - If you change both the source URL and playback count, after the new configuration takes effect (whether immediately or after the current playback ends), the count will start from 1.
	  - If you change the destination URL, the playback count will be reset.
5. Enter a destination URL for receiving the content.
   1. Click **Address Generator** to enter the URL generation page.
   ![](https://qcloudimg.tencent-cloud.cn/raw/9724d77727e21ba1798485d03d6e3246.png)
   2. Select an existing push domain name, enter the `Appname`, `StreamName`, and expiration time, and click **Confirm** to generate a push URL, which will be auto-filled as **Destination Address**.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b1b6f0b832bacb15b281d71fc653afb0.png)
> !Make sure the URL expiration time is later than the task end time. If you change the destination after the task starts, it will stop and restart.
6. Click **Save**.


## Managing Tasks
[](id:view)
### Viewing task details
In the [task list](https://console.cloud.tencent.com/live/tools/relay), find your task, and click its description/ID to view task details in the pop-up window.
![](https://qcloudimg.tencent-cloud.cn/raw/c2bad33a6a735a218fa79b98f3738275.png)

>? You can click the buttons at the bottom of the pop-up window to edit the task, switch inputs, restart the task, or disable the task.

### Viewing task status
In the [task list](https://console.cloud.tencent.com/live/tools/relay), find your task, and click its description/ID to view its execution status in the pop-up window.

![](https://qcloudimg.tencent-cloud.cn/raw/cd498cb1fd678e39b0942383c278e82b.png)

<table>
<thead><tr><th>Task Status</th><th>Field Value</th><th>Description</th></tr></thead>
<tbody><tr>
<td>Not started</td>
<td>Inactive</td>
<td>The task has not started yet.</td>
</tr><tr>
<td rowspan=2>Valid</td>
<td>Active</td>
<td>The task has started and is executed as expected.</td>
</tr><tr>
<td>Inactive</td>
<td>The task has started but is not executed as expected.</td>
</tr><tr>
<td>Disabled</td>
<td>Inactive</td>
<td>The task is disabled.</td>
</tr><tr>
<td>Expired</td>
<td>Inactive</td>
<td>The task has expired.</td>
</tr>
</tbody></table>



[](id:change)
### Modifying a task
1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), find the task you want to modify, and click **Edit**.
![](https://qcloudimg.tencent-cloud.cn/raw/a0a83bf06f9b5ae9743b68b19e4c40cd.png)
2. Modify the task information, and then click **Save**.
 - You cannot change the region or content type.
 - When modifying the task end time, make sure that the destination URL is valid until the task ends. Modifying the destination URL will cause the task to stop and restart.
![](https://qcloudimg.tencent-cloud.cn/raw/d950a8029e1944e9029445dd8e428933.png)
3. In the pop-up window, check the information before and after the change:
   - Suppose you modified the **start time, end time, and playback count** of a task. You would see the following information in the pop-up window:
![](https://qcloudimg.tencent-cloud.cn/raw/4cadcabeef99828ab4be144040cbfd19.png)
   - If the source URLs for **Custom video path** are changed, you need to select whether to apply the change **After the current video ends** (default) or **Now**. After the changes take effect, relay will restart from the first source URL.
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
2. In the pop-up window, click **Restart**.
![](https://qcloudimg.tencent-cloud.cn/raw/d1b03e226297e44cbb7504d57c54af4f.png)

[](id:disable)
### Disabling a task
If you disable a task, **the task will stop**. You can click [Enable](#enable) to start it again. Perform the following to disable a task:

1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), find the relay task you want to disable, and click **Disable**.
2. In the pop-up window, click **Disable**.
![](https://qcloudimg.tencent-cloud.cn/raw/c3acfb89f425b50ba53a8d63075091d8.png)


[](id:enable)
### Enabling a task
If you enable a task, **the task will start from the beginning**. Perform the following to enable a task:

1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), find the relay task you want to enable, and click **Enable**.
2. In the pop-up window, click **Confirm**.
![](https://qcloudimg.tencent-cloud.cn/raw/77417a9c8406fe9d763c4d3960d98b21.png)

[](id:delete)
### Deleting a task
Deleted tasks **cannot be recovered**. Perform the following to delete a task:

1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), find the relay task you want to delete, and click **Delete**.
2. In the pop-up window, click **Delete**.
![](https://qcloudimg.tencent-cloud.cn/raw/44a15ad52bfc81f62c0aa907cdc7eb5c.png)

[](id:batch)
### Batch operations
You can delete, disable, and enable **up to 10 relay tasks** at a time.
1. In the [task list](https://console.cloud.tencent.com/live/tools/relay), select the relay tasks you want to delete, disable, or enable.
2. Click **Batch Operation**, and select **Delete**, **Disable**, or **Enable**.
![](https://qcloudimg.tencent-cloud.cn/raw/7401eade6f5e04b9eadf71e04211f6e0.png)
3. In the pop-up window, confirm the information and click **Delete**, **Disable**, or **Enable**.
![](https://qcloudimg.tencent-cloud.cn/raw/5874636c548a4733281cd33eaca35abe.png)

   
## Auto-Deleting Expired Tasks

A task expires after its end time. If you have too many relay tasks, you may fail to create new ones. To avoid this, you can enable auto-delete for the system to delete expired tasks automatically at the specified time. Deleted tasks cannot be recovered.

1. Go to **CSS Toolkit** > **[Relay](https://console.cloud.tencent.com/live/tools/relay)**, and click **Set** in the **Expired** area.
2. Click ![](https://qcloudimg.tencent-cloud.cn/raw/7ed257d05a4283dc233ef406520187b4.png) to enable auto-delete.
3. Specify a period (1-24 hours) to retain expired tasks before they are deleted.
![](https://qcloudimg.tencent-cloud.cn/raw/4d579b1d0776ea22b5d994e3b7357ea3.png)



