The file tampering feature provides the lists of monitored events and configured rules. The event list module displays the file tampering check results.

## Filtering and Refreshing Events
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Event list** on the left sidebar.
2. On the **Event list** page, click the search box and search for file tampering check results by keyword such as filename, process path, or hit rule.
<img src="https://qcloudimg.tencent-cloud.cn/raw/fc7fc91e52bebb5f969b5c12272590bc.png" style="zoom:67%;" />
3. On the **Event list** page, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the event list.

## Exporting the Check Result
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Event list** on the left sidebar.
2. On the **Event list** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target file tampering event and click ![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png) to export it.
>? Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) in the **Operation** column to select multiple ones.

![](https://qcloudimg.tencent-cloud.cn/raw/8b46bfb8b5523323e80733930741e07a.png)

## Changing the Event Status[](id:GGSJZT)
 Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Event list** on the left sidebar.
### Method 1
On the **Event list** page, you can mark a file tampering event as processed or ignore or delete it.
 - Mark as processed: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target file tampering event and click **Mark as processed** > **OK**.
>? It's recommended to handle the event by following "Solution" in the event details and mark it as processed.

 - Ignore: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target file tampering event and click **Ignore** > **OK**.
>? Only the selected events are ignored. Alerts will be triggered when the same events occur again.

 - Delete: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target file tampering event and click **Delete** > **OK**.
>! The selected event record will no longer be displayed in the console and cannot be recovered once deleted. Proceed with caution.

### Method 2
1. On the **Event list** page, click **Process now** to add events in the **Pending resolved** status to the allowlist, mark them as processed, or ignore them.
![](https://qcloudimg.tencent-cloud.cn/raw/de700c84c843802ab84e238553f0f822.png)
2. Click **OK** or **Cancel**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/9557f6c0a523e975916719a908bacad0.png" style="zoom:67%;" />
3. On the **Event list** page, click **Unignore** or **Delete** to unignore or delete events in the **Ignored** status.
>?
>- As an event will be in the **Pending resolved** status once unignored, you need to click **OK** for confirmation.
>- The event record will no longer be displayed in the console and cannot be recovered once deleted. Proceed with caution.

4. On the **Event list** page, click **Delete** to delete events in the **Processed** status.
>? The event record will no longer be displayed in the console and cannot be recovered once deleted. Proceed with caution.

## Viewing Event Details
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Event list** on the left sidebar.
2. On the **Event list** page, click ![](https://main.qcloudimg.com/raw/5b9eac8b014539648daf1ade48e3188a.png)	 on the left of the **Process path** to view the event description.
![](https://qcloudimg.tencent-cloud.cn/raw/2fa068b2172603e41a1153d7acf811c9.png)
3. On the **Event list** page, click **View details**.
![](https://qcloudimg.tencent-cloud.cn/raw/c33701ba34aee6a6e4a41b479eb3ff9c.png)
4. The **Event details** page displays the event details, process information, parent process information, and event description. You can mark the event as processed, ignore it, or add it to the allowlist.
>? For detailed directions on how to mark an event as processed or ignore or delete it, see [Changing the Event Status](#GGSJZT).

5. On the **Event details** page, click **Add to allowlist** to enter the **Copy rule** page, where you need to configure the basic information and rules and specify the scope.
![](https://qcloudimg.tencent-cloud.cn/raw/b2ab31e707910df7dafb73a3dd5aa8ce.png)
  - Basic information: Enter the rule name of the event. Toggle on or off ![](https://main.qcloudimg.com/raw/9053f4e9bc709aa720fccd5045eb8cd0.png) to enable or disable rule check.
>? This rule will no longer be executed once disabled.

![](https://qcloudimg.tencent-cloud.cn/raw/39fbe01f3d7cd5dccdb18771401069b4.png)
  - Configure rules: Enter the process path and accessed file path to be allowed and select the action. Click **Add** or **Delete** to add or delete a rule.	
>?
>- You can configure up to 30 rules.
>- Actions to be executed include:
>  - Block: Once a rule is hit, the process will be blocked and the event details will be recorded.
>  - Alert: Trigger alerts about the event, allow running of the process and log the event details.
>  - Allow: When a rule is hit, the process will be automatically allowed without being recorded.

   - Images: **All images** or **Specified images**. Click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png) or ![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png) to select or delete the target specified image.
>? You can press Shift to select multiple ones.

 ![](https://qcloudimg.tencent-cloud.cn/raw/704efb8f62b39b4b90de11d090e09b79.png)
6. After selecting the target content, click **Set** or **Cancel**.

## Custom List Management
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **File Tampering** > **Event list** on the left sidebar.
2. On the **Event list** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
3. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a6a48e3b3054ba43c9dc493f0cdf41f5.png" style="zoom:67%;" />

### Key fields in the list
1. First occurred: The time when an alert is first triggered by the file tampering event. By default, the system aggregates the same alert events not processed.
2. Last occurred: The time when an alert is last triggered by the aggregated alert events. You can click the sort button on the right to sort the events in the list in chronological or reverse chronological order.
3. Events: Total number of alerts triggered by the file tampering event within the aggregation period.
4. Execution result: **Blocked successfully**, **Failed to block**, **Allowed**, or **Alert**. You can quickly filter events in the list by action execution result.
5. Status: **Processed**, **Ignored**, **Pending resolved**, or **Allowed**. You can quickly filter events in the list by status.
