Tencent Cloud CSS console provides relay feature. If you cannot use your live streaming source to push or you want to use on-demand videos for live streaming, you can use the relay feature to quickly pull contents from an existing live streaming source or videos and then push them to the destination URL, with no need for live push.

![](https://main.qcloudimg.com/raw/8f0b044ce2104efdc1ed835287b9b683.png)

## Prerequisites
- You have activated [CSS](https://cloud.tencent.com/product/css) and logged in to the CSS console.
- You have added a [push domain name](https://intl.cloud.tencent.com/document/product/267/35970) in the console.

## Notes
- You can create up to **20** relay tasks.
- Using the relay feature will incur **costs by duration**. For details, please see [Billing Overview of Relay](https://intl.cloud.tencent.com/document/product/267/41059).
- Relay only pulls and pushes contents. **Please ensure that the contents have been authorized and comply with the laws and regulations for distribution. If the contents infringe relevant rights or violate regulations, CSS will suspend related features and reserve the right to legal action**.

[](id:create)
## Creating a Task
1. Select **CSS Toolkit** > **[Relay](https://console.intl.cloud.tencent.com/live/tools/relay)]**, and click **Create Task**.
![](https://main.qcloudimg.com/raw/192994e09ae8fd0c84ccef009f6c404f.png)
2. Enter the basic information of the task:
![](https://main.qcloudimg.com/raw/0d166562b4d7b0dcdbdc03d70aff6e6b.png)
<table>
<tr><th width="15%">Configuration Item</th><th>Description</th>
<tr>
<td>Task Description</td>
<td>Custom task description.</td>
</tr><tr>
<td>Execution Time</td>
<td>It is from the <code>current time</code> to <code> 24 hours later</code> by default. You can select an end time within 1 year from now, and the execution period is up to 7 days. <br>Suppose the current time is March 30, 2021 11:50:01. <ul style="margin:0"><li/>You can select March 24, 2022 11:50:01 and March 30, 2022 11:50:01 for example.<li/>The end time cannot exceed March 30, 2022 11:50:01.</ul></td
</tr><tr>
<td>Region</td>
<td><ul style="margin:0"><li/>You can select a region for the task. You can choose North China (Beijing), East China (Shanghai), South China (Guangzhou), Southeast Asia (Singapore), Southeast Asia (Thailand), Northeast Asia (Korea), and South Asia (India). <li/><b>If you select “Random”, the system will automatically assign the nearest region. </b></ul></td>
</tr><tr>
<td>Event Callback Notification</td>
<td>Enter a callback URL for receiving relay task event notifications. </td>
</tr></table>
3. Select the **Live streaming** or **Video on demand** as the content type:
	- If you select **Live streaming**, you need to enter only **1** live streaming source URL.
	![](https://main.qcloudimg.com/raw/2b3ca982581457e36e6d485363fd6028.png)
	- If you select **Video on demand**:
		- You can enter **multiple** (max: 30) source URLs.
		- You can select **Repeat** or **Specified** (min: 1; max: 100) for the playback count.
		![](https://main.qcloudimg.com/raw/d050d37b821aa6ebcac3de2a868c81f8.png)
>? 
>- The system will stop the relay task either when the playback count reaches the specified value or when the task reaches its end time.
>- Changing task information:
			- If you change the playback count, the current playback will be counted as 1 when the new value is applied.
			- If you change both the source URL and playback count, the current playback will not be counted and the new value will be applied, no matter you choose to apply the change after the current video ends or now.
			- If you change the destination URL, the playback count will be reset. 
4. Enter a destination URL for receiving the content.
	1. Click **Address Generator** below the destination URL to enter the URL generation page.
	![](https://main.qcloudimg.com/raw/9217ecb6839744654c7ff6db8e3df0d3.png)
	2. Select an existing push stream name, enter the `Appname`, `StreamName` and expiration time. Then click **Confirm** to generate a push URL, which will be entered as the destination URL automatically.
	![](https://main.qcloudimg.com/raw/332c5a44df1d5ff46f86c0e9a7a8ea63.png)
	 > !The URL expiration time should be greater than the task end time. If the destination URL is changed after the task starts, it will stop and restart.
5. After completing the configuration, click **Save**.


## Managing Tasks
[](id:view)
### Viewing task details
In the [task list](https://console.intl.cloud.tencent.com/live/tools/relay), select the target task, click the corresponding “Task Description/ID”, and then you can view its details in the pop-up.
![](https://main.qcloudimg.com/raw/0c0d0531e56b16a236440fe0776d5a37.png)

>? You can click **Edit** or **Disable** to [modify](#change) or [disable](#disable) a task.

[](id:change)
### Modifying a task
1. In the [task list](https://console.intl.cloud.tencent.com/live/tools/relay), select the task you have created successfully and click **Edit** on the right to modify it.
![](https://main.qcloudimg.com/raw/f172a1e547aac1fd73ee4383a018109b.png)
2. Modify the task information, and then click **Save**.
   > !
   > - You cannot change the region and content type.
   > - When modifying the task end time, you need to ensure that the destination URL is valid until the task ends. Modifying the destination URL will cause the task to stop and restart.
   > 
![](https://main.qcloudimg.com/raw/26d36fc23562b687d22dc94dbf2c71e5.png)
3. Compare the information before and after change in the pop-up:
  - Changes in the following example include **Task Description**, **Execution Time**, **Event Callback Notification**, and **Playback Count**:
![](https://main.qcloudimg.com/raw/e3884170153b6482fc14b882ae9b5a74.png)
  - When changes include the source URLs of **Video on demand**, you need to select to apply the change **After the current video ends** or **Now**. If you don’t choose, the default operation is to apply it **After the current video ends**. After change, relay will restart from the beginning of the new source URLs.
![](https://main.qcloudimg.com/raw/1ceca6602a70abb24b7f69fbfbf39233.png)
	- When the changes include **Destination Address**, you will be notified that after you confirm the changes, the current relay task will **stop and restart**.
![](https://main.qcloudimg.com/raw/3f252444ee99cb85dc5627a658196a04.png)
4. After checking the information, click **Confirm** to modify it.

[](id:copy)
### Copying a task
1. In the [task list](https://console.intl.cloud.tencent.com/live/tools/relay), select the target task, click **Copy** on the right to enter the page for creating a relay task.
![](https://main.qcloudimg.com/raw/404679520530b20f5747bf690c733255.png)
2. Paste the information in the new page. You can [modify](#create) the copied task information. 
3. Click **Save** to create a new relay task.



[](id:reboot)
### Restarting a task
Restarting a task will **not change its status**. An ongoing task will be **restarted from the beginning**. Perform the following to restart a task:

1. In the [task list](https://console.intl.cloud.tencent.com/live/tools/relay), select the target relay task, and click **Restart** on the right.
2. In the confirmation pop-up, click **Restart**.
![](https://main.qcloudimg.com/raw/cfd3357df62a14fb628403b3f0149ce9.png)

[](id:disable)
### Disabling a task
After disabling a task, **the task will stop** and you need to [enable](#enable) it to restart the task. Perform the following to restart a task:

1. In the [task list](https://console.intl.cloud.tencent.com/live/tools/relay), select the target relay task and click **Disable** on the right.
2. In the confirmation pop-up, click **Disable**.
![](https://main.qcloudimg.com/raw/f4d68a5a27f958723227d36c39fda20b.png)


[](id:enable)
### Enabling a task
After enabling a task, **the task will restart from the beginning**. Perform the following to enable a task:

1. In the [task list](https://console.intl.cloud.tencent.com/live/tools/relay), select the target relay task which was disabled, and click **Enable** on the right.
2. In the confirmation pop-up, click **Confirm**.
![](https://main.qcloudimg.com/raw/2db6188689cce4b8ac524877988b28b5.png)

[](id:delete)
### Deleting a task
Deleted tasks **cannot be recovered**. Perform the following to delete a task:

1. In the [task list](https://console.intl.cloud.tencent.com/live/tools/relay), find the target relay task, click **Delete** on the right.
2. In the confirmation pop-up, click **Delete**.
![](https://main.qcloudimg.com/raw/7428ba2c79d4fda180ce7a0e5d887d38.png)

[](id:batch)
### Batch operations
You can delete, disable, and enable relay tasks in batch (**max: 10**).
1. In the [task list](https://console.intl.cloud.tencent.com/live/tools/relay), check the tasks to process.
2. Select **Delete**, **Disable**, or **Enable** as the operation type.
![](https://main.qcloudimg.com/raw/26e9449f4abe937679e6decc3d7895c9.png)
3. In the confirmation pop-up, and click **Delete**, **Disable**, or **Enable**.
![](https://main.qcloudimg.com/raw/8b30604e230cb0b8cd7d253d19daee5d.png)

   
