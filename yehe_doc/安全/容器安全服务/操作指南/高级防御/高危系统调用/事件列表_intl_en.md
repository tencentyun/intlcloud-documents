The high-risk syscall feature provides the lists of risky syscall events and allowlist policies. The event list module displays the high-risk syscall check results.

## Filtering and Refreshing Events
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **High-risk Syscalls** > **Event list** on the left sidebar.
2. On the **Event list** page, click the search box and search for high-risk syscall events by keyword such as process path, syscall name, or container name.
<img src="https://qcloudimg.tencent-cloud.cn/raw/d887206396af19054c4f56325d14b065.png" style="zoom:67%;" />
3. On the **Event list** page, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the event list.

## Exporting the Event List
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **High-risk Syscalls** > **Event list** on the left sidebar.
2. On the **Event list** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target high-risk syscall event and click ![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png) to export it.
>? Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) in the **Operation** column to select multiple ones.

![](https://qcloudimg.tencent-cloud.cn/raw/ce51f00ba22b0db7cb01c227997d6697.png)

## Changing the Event Status[](id:GGSJZT)
Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **High-risk Syscalls** > **Event list** on the left sidebar.
### Method 1
On the **Event list** page, you can mark a high-risk syscall event as processed or ignore or delete it.
 - Mark as processed: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target high-risk syscall event and click **Mark as processed** > **OK**.
>? It's recommended to handle the event by following "Solution" in the event details and mark it as processed.

 - Ignore: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target high-risk syscall event and click **Ignore** > **OK**.
>? Only the selected events are ignored. Alerts will be triggered when the same events occur again.

 - Delete: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target high-risk syscall event and click **Delete** > **OK**.
>! The selected event record will no longer be displayed in the console and cannot be recovered once deleted. Proceed with caution.

### Method 2
1. On the **Event list** page, click **Process now** to add events in the **Pending resolved** status to the allowlist, mark them as processed, or ignore them.
![](https://qcloudimg.tencent-cloud.cn/raw/2aa94ceab0bac709eb5bc8146630f7bc.png)
2. Click **OK** or **Cancel**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e33549678793b4a78d6d514d26056aed.png" style="zoom:67%;" />
3. On the **Event list** page, click **Unignore** or **Delete** to unignore or delete events in the **Ignored** status.
>?
>- As an event will be in the **Pending resolved** status once unignored, you need to click **OK** for confirmation.
>- The event record will no longer be displayed in the console and cannot be recovered once deleted. Proceed with caution.

4. On the **Event list** page, click **Delete** to delete events in the **Processed** status.
>? The event record will no longer be displayed in the console and cannot be recovered once deleted. Proceed with caution.

## Viewing Event Details
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **High-risk Syscalls** > **Event list** on the left sidebar.
2. On the **Event list** page, click ![](https://main.qcloudimg.com/raw/5b9eac8b014539648daf1ade48e3188a.png)	 on the left of the **Process path** to view the event description.
![](https://qcloudimg.tencent-cloud.cn/raw/21228f213aa46631578bf9d952e177c2.png)
3. On the **Event list** page, click **View details**.
![](https://qcloudimg.tencent-cloud.cn/raw/e980a7d0cda21dac2893d0409f22319e.png)
4. The **Event details** page displays the event details, process information, parent process information, and event description. You can mark the event as processed, ignore it, or add it to the allowlist.
>? For detailed directions on how to mark an event as processed or ignore or delete it, see [Changing the Event Status](#GGSJZT).

5. On the **Event details** page, click **Add to allowlist** and confirm the conditions (process path and syscall name) and the scope.
![](https://qcloudimg.tencent-cloud.cn/raw/0b7cdf02ac7f0553a6b11d2b0bc5e786.png)
 - Conditions: **Process path** and **Syscall name**, which cannot be changed.
 ![](https://qcloudimg.tencent-cloud.cn/raw/8201d9392753e845481639089ca5f921.png)
 - Scope: **All images** or **Specified images**. Click ![](https://main.qcloudimg.com/raw/37d813d17a69271ce31b3233ad0a949e.png) or ![](https://main.qcloudimg.com/raw/be9e47bccb644d8a099149bac4aef1e0.png) to select or delete the target specified image.
>? You can press Shift to select multiple ones.

![](https://qcloudimg.tencent-cloud.cn/raw/b772f89d79bdb22c7a5e2c7c055627da.png)
6. After selecting the target content, click **Set** or **Cancel**.

## Custom List Management
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Advanced Prevention** > **High-risk Syscalls** > **Event list** on the left sidebar.
2. On the **Event list** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
3. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/8c1c28081017758e9aec6116ddc0ef79.png" style="zoom:67%;" />

### Key fields in the list
1. First occurred: The time when an alert is first triggered by the syscall event. By default, the system aggregates the same alert events not processed.
2. Last occurred: The time when an alert is last triggered by the aggregated alert events. You can click the sort button on the right to sort the events in the list in chronological or reverse chronological order.
3. Events: Total number of alerts triggered by the syscall event within the aggregation period.
4. Execution result: **Blocked successfully**, **Failed to block**, **Allowed**, or **Alert**. You can quickly filter events in the list by action execution result.
5. Status: **Processed**, **Ignored**, **Pending resolved**, or **Allowed**. You can quickly filter events in the list by status.
