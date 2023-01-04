This document describes the event list of the reverse shell feature.

## Filtering and Refreshing Events
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Runtime Security** > **Reverse Shell** > **Event list** on the left sidebar.
2. On the **Event list** page, click the search box and search for reverse shell events by keyword such as process name or parent process name.
<img src="https://qcloudimg.tencent-cloud.cn/raw/d638226da41c8ab75f2c9b328e95e967.png" style="zoom:67%;" />
3. On the **Event list** page, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the list of reverse shell events.

## Exporting the Event List
On the **Event list** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target reverse shell event and click ![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png) to export it.
>? You can click ![](https://main.qcloudimg.com/raw/08dfa220659d6576a39a981e61ad02e2.png) to select multiple events and click ![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png) to batch export them.

![](https://qcloudimg.tencent-cloud.cn/raw/1e66b5e216c669017e0811c7bc91f04f.png)

## Event Status Processing[](id:SJZTCL)
On the **Event list** page, you can mark a reverse shell event as processed or ignore or delete it.
 - Mark as processed: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target reverse shell event and click **Mark as processed** > **OK**.
>? It's recommended to handle the event by following "Solution" in the event details and mark it as processed.

 - Ignore: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target reverse shell event and click **Ignore** > **OK**.
>? Only the selected events are ignored. Alerts will be triggered when the same events occur again.

 - Delete: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target reverse shell event and click **Delete** > **OK**.
>! The selected event record will no longer be displayed in the console and cannot be recovered once deleted. Proceed with caution.

## Viewing List Details
1. On the **Event list** page, click ![](https://main.qcloudimg.com/raw/5b9eac8b014539648daf1ade48e3188a.png)	 on the left of the **Event type** to view the event description.
![](https://qcloudimg.tencent-cloud.cn/raw/fd5f572f826c9fddc790e279133dfdbf.png)
2. On the **Event list** page, click the **Container name/ID** or **Image name/ID** to enter the asset management list.
![](https://qcloudimg.tencent-cloud.cn/raw/c22322d25976bdfd7df7a58b7e1ba3a1.png)
3. On the **Event list** page, click **View details** to pop up the drawer on the right, which displays the event details, process information, parent process information, and event description.
![](https://qcloudimg.tencent-cloud.cn/raw/d72ee15c6ff9aa0bf1afc4a1fd005073.png)
4. On the **Event list** page, the event status can be **Processed**, **Ignored**, or **Pending resolved**. You can manipulate events in different statuses as follows:
 - Processed/Allowed: Click **Delete** and click **OK** in the pop-up window.
>? The event record will no longer be displayed in the console and cannot be recovered once deleted. Proceed with caution.

 ![](https://qcloudimg.tencent-cloud.cn/raw/58f1b9063155c272c68dbe8e028e157e.png)
 - Pending resolved: Click **Process now** to mark the event as processed, ignore or delete it, or add it to the allowlist. For detailed directions, see [Event Status Processing](#SJZTCL).
 - Ignored: Click **Unignore** or **Delete** to turn the event into the **Pending resolved** status or delete it.
![](https://qcloudimg.tencent-cloud.cn/raw/7576f77d59d6a9a109f079536985162a.png)

## Custom List Management
1. On the **Event list** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
2. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/c6d4593f5d192cc388d221ff5de1db61.png" style="zoom:67%;" />

### Key fields in the list
1. First occurred: The time when an alert is first triggered by the reverse shell event.
>? By default, the system aggregates the same alert events not processed.

2. Last occurred: The time when an alert is last triggered by the aggregated alert events. You can click the sort button on the right to sort the events in the list in chronological or reverse chronological order.
3. Events: Total number of alerts triggered by the reverse shell event within the aggregation period.
4. Status: **Processed**, **Ignored**, **Pending resolved**, or **Allowed**. You can quickly filter events in the list by status.