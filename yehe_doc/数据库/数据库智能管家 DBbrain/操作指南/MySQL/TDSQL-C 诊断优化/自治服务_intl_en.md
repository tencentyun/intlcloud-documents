## Feature Description

DBbrain's database autonomy service the supports automatic throttling and killing. After it is enabled, when a large number of SQL operations are performed on your database instances, cache penetration occurs, or your database instances use a lot of resources, the Autonomy Center will automatically trigger an autonomy event to fix the exception, with no human intervention required.

> ?
> - This feature is currently supported only for TencentDB for MySQL instances in Chongqing and Chengdu regions and will be available in other regions in the future.
> - Only the automatic throttling and killing feature is currently supported, and more autonomy features will be supported in the future.
> - Autonomy is currently triggered based on thresholds, and autonomy based on smart calculation will be supported in the next version.

## Overview

Log in to the [DBbrain console](https://console.cloud.tencent.com/dbbrain/analysis) and select **Performance Optimization** on the left sidebar. On the displayed page, select a database type and an instance at the top, and select the **Autonomy Center** tab.

## Configuring the Autonomy Feature 

1. Log in to your database account to perform a verification.
   To configure database autonomy, you need to log in to your database instance first; otherwise, you can only view the autonomy data but cannot modify the configuration.
2. Click **Autonomy Configuration** in the top-right corner to enter the Autonomy Center configuration page.
3. When you enable database autonomy for the first time, you need to configure an event notification first, so that you will be promptly notified when an autonomy operation is triggered.  
   - The autonomy service adopts a built-in policy template for event notifications, which is automatically loaded when you configure an autonomy policy for your instance for the first time. Therefore, you can modify only the recipient, notification method, and sending frequency but not the instance information in this policy. If you need to modify more items, copy the built-in policy and customize it in a new policy.
   - After database autonomy is disabled for your database instance, no more autonomy event notifications will be triggered.  
  - In **Event Notification** > **Sending Policy** > **Autonomy Policy**, copy the built-in policy and then configure **Associate Instance**, **Rule**, and other information as needed in a new policy.
4. After setting the autonomy parameters, click **Save**.
 - Automatic Throttling and Killing: After it is selected, threads and sessions that meet the criteria will be killed automatically.
 - Throttling Scenario: Currently, only **Trigger threshold** is supported.
 - Threshold Configuration: Set the condition for the trigger threshold.
    - CPU and Sessions: Set the CPU utilization and the number of database sessions, which can be in **and** or **or** relationship for judgment. 
    - Trigger Condition: Set the duration of the event in **CPU and Sessions** before an operation is triggered.
    In the above figure, when the CPU utilization reaches 60% and the number of active database sessions reaches 15, and the event lasts 2 minutes, throttling will be triggered.
 - Abnormal SQL Killing: After it is selected, abnormal SQL sessions will be automatically killed (to specify the killing rule, go to **Advanced Rule**).
 - Throttling Period and Concurrency: Set the **Throttling Period**, **Max Concurrency**, and **The throttling task lasts for up to**. If the **Max Concurrency** is set to **0**, all SQL statements will be throttled.
 - Advanced Rule: You can set to throttle, kill, or release statements with specified keywords. Unless necessary, we recommend you not enable this option; otherwise, if the keywords or killing conditions you set happen to be used in an unusually high number of intended SQL statements, the autonomy effect may be affected.
5. After the configuration is completed, database autonomy will be enabled by default, and it is toggled on as shown on the homepage.

## Viewing the Autonomy Feature

### Viewing real-time monitoring data

After database autonomy is enabled, you can check out the real-time autonomy monitoring view as shown below. Select a time range to get the details of triggered autonomy events. You can also click a triggered event to directly view its **Autonomy Task Details**.

### Viewing the autonomy event timeline

1. Select a time range to display the list of autonomy events triggered in the time range.
2. Click an autonomy event to unfold it and view the autonomy tasks triggered within the event.
3. Click **Details** to view the event record.
4. On the **Task Details** page, you can view the session snapshot, reference monitoring data, and SQL execution record.
5. You can terminate running autonomy events if you no longer need the autonomy service.
After an autonomy event is triggered, the **Terminate** button will be displayed at different levels. Click **Terminate** in the event row to terminate all autonomy tasks under the event, or click **Terminate** next to **Details** in the **Operation** column to terminate a specific autonomy task.
You can also go to the details page and click **Terminate Task** to terminate the task.
6. In the pop-up window, click **OK**.
   Only running autonomy events can be terminated, while subsequent autonomy events will still be triggered normally.

### Viewing the distribution of autonomy tasks

After you enable an autonomy event, the autonomy tasks displayed in the distribution chart will be automatically counted.
The number and proportion of autonomy tasks of each type triggered in the selected time range will be automatically refreshed and counted.

