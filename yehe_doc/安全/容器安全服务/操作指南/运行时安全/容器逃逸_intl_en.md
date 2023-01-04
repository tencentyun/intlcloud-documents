## Event List
### Viewing the set status
1. Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Runtime Security** > **Container Escape** on the left sidebar.
2. On the **Container Escape** page, the security status module displays whether a container escape event exists, and if so, we recommend you process it immediately.
![](https://qcloudimg.tencent-cloud.cn/raw/dc9d08d9ec367ec819dcb0a61c2af51f.png)
3. On the **Container Escape** page, the monitoring status module displays the container escape event types that can be checked by the system. Toggle on ![](https://main.qcloudimg.com/raw/9053f4e9bc709aa720fccd5045eb8cd0.png) to customize the monitoring status.
![](https://qcloudimg.tencent-cloud.cn/raw/d0fe285fafbd73d4065a36c193a5aecb.png)

### Viewing the list of container escapes
Log in to the [TCSS console](https://console.cloud.tencent.com/tcss) and click **Runtime Security** > **Container Escape** on the left sidebar.
#### Filtering and refreshing container escapes
1. On the **Container Escape** page, click the search box and search for container escape events by keyword such as container name, image name, or server name.
<img src="https://qcloudimg.tencent-cloud.cn/raw/b19c1d9c0658ad27984d1589855574a9.png" style="zoom:67%;" />
2. On the **Container Escape** page, click ![](https://main.qcloudimg.com/raw/84b6cc4d2eabf9ed7fc0bea43503bb1d.png) on the right of the **Operation** column to refresh the container escape events.

#### Exporting a container escape
On the **Container Escape** page, click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target container escape event and click ![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png) to export it.
>? You can click ![](https://main.qcloudimg.com/raw/08dfa220659d6576a39a981e61ad02e2.png) to select multiple events and click ![](https://main.qcloudimg.com/raw/24d375a75e4ee95c77910d101f7203dd.png) to batch export them.

![](https://qcloudimg.tencent-cloud.cn/raw/c5f7bf070aaac81e3933b36b2608dbad.png)

#### Event status processing[](id:RQTYCL)
On the **Container Escape** page, you can mark a container escape event as processed or ignore or delete it.
 - Mark as processed: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target container escape event and click **Mark as processed** > **OK**.
>? It's recommended to handle the event by following "Solution" in the event details and mark it as processed.

 - Ignore: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target container escape event and click **Ignore** > **OK**.
>? Only the selected events are ignored. Alerts will be triggered when the same events occur again.

 - Delete: Click ![](https://main.qcloudimg.com/raw/21ff3bd68750cb41c5ce662a24629cb3.png) to select the target container escape event and click **Delete** > **OK**.
>! The selected event record will no longer be displayed in the console and cannot be recovered once deleted. Proceed with caution.

#### Viewing list details
1. On the **Container Escape** page, click ![](https://main.qcloudimg.com/raw/5b9eac8b014539648daf1ade48e3188a.png)	 on the left of **Event type** to view the event description.
![](https://qcloudimg.tencent-cloud.cn/raw/55be2cd48f10bec2681aef24f561d254.png)
2. On the **Container Escape** page, click the **Container name/ID** or **Image name/ID** to enter the asset management list.
![](https://qcloudimg.tencent-cloud.cn/raw/0c7ddf9ca7e670bd68e1f7c1ac40516f.png)
3. On the **Container Escape** page, click **View details** to pop up the drawer on the right, which displays the event details, process information, and event description.
![](https://qcloudimg.tencent-cloud.cn/raw/9f2ae57ec282c64db85f5cfb3a5bbdbc.png)
4. On the **Container Escape** page, the event status can be **Processed**, **Ignored**, or **Pending resolved**. You can manipulate events in different statuses as follows:
  - Processed: Click **Delete** and click **OK** in the pop-up window.
>? The event record will no longer be displayed in the console and cannot be recovered once deleted. Proceed with caution.

 ![](https://qcloudimg.tencent-cloud.cn/raw/7851f056134ee7ba34070978d4591610.png)
 - Pending resolved: Click **Process now** to mark the event as processed or ignore or delete it. For detailed directions, see [Event status processing](#RQTYCL).
 ![](https://qcloudimg.tencent-cloud.cn/raw/1a2f3ccfc9fdcd0306531d75dcf6067e.png)
 - Ignored: Click **Unignore** or **Delete** to turn the event into the **Pending resolved** status or delete it.
 ![](https://qcloudimg.tencent-cloud.cn/raw/34f9ed1a51566e6d6e2be599d6dad5ff.png)

#### Custom list management
1. On the **Container Escape** page, click ![](https://main.qcloudimg.com/raw/d42b27540eef9bf90a9e30f96b500bf3.png) to pop up the **Custom List Management** window.
2. In the pop-up window, select the target type and click **OK**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/d8987179fdfe42c9bf0dab66ba3124f1.png" style="zoom:67%;" />

**Fields in the list**
 1. Event type: Type of the container escape event, which can be host file access escape, mount namespace escape, program privilege escalation, privileged container startup escape, sensitive path mounts, or syscall escape.
 2. First occurred: The time when an alert is first triggered by the escape event.
>? By default, the system aggregates the same escape events not processed.

 3. Last occurred: The time when an alert is last triggered by the aggregated alert events. You can click the sort button on the right to sort the events in the list in chronological or reverse chronological order.
 4. Events: Total number of alerts triggered by the escape event within the aggregation period.
 5. Status: **Processed**, **Ignored**, **Pending resolved**, or **Allowed**. You can quickly filter events in the list by status.


## Escape Allowlist
When troubleshooting a container escape alert, for example, if a business container requires startup in privileged mode, sensitive path mounting, or other configuration that will trigger an escape alert, you can add the alert event to the allowlist or create an allowlist on the **Allowlist policies** tab.


### Adding an alert event to the allowlist
1. On the [**Container Escape**](https://console.cloud.tencent.com/tcss/runtime/containerEscape) page, click **Process**, select **Add to allowlist**, and click **OK** to allow an alert event.
>! If you are sure that this container escape event is normal, add the images associated with the container to the allowlist. **This kind of escape events will not trigger alerts any more**.

![](https://qcloudimg.tencent-cloud.cn/raw/482784c4e4f0650617b3b35e47aeb702.png)
2. On the **Add allowed images** page, the escape alert type and source image associated with the alert event are selected by default. You can add allowed event types and images to be added to the allowlist and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/bed053709a62c73c0216cae06ca7deea.png)
3. To add all images to the allowlist for an event type, click **Monitoring settings** on the right of the **Monitoring status** and adjust the event type with monitoring enabled.
![](https://qcloudimg.tencent-cloud.cn/raw/16d1b18ee77e5818a33d3a6aba5f1500.png)

### Allowlist policies
You can batch add images to the allowlist on the **Allowlist policies** tab to avoid further alerts.

#### Adding to the allowlist
1. On the [**Container Escape**](https://console.cloud.tencent.com/tcss/runtime/containerEscape) > **Allowlist policies** page, click **Add allowed policies**.
![](https://qcloudimg.tencent-cloud.cn/raw/000e71aedf1d0e3047f16c7d6ffe38a7.png)
2. On the **Add allowed images** page, select allowed event types and images and click **OK**.
![](https://qcloudimg.tencent-cloud.cn/raw/b3a8bf772b963f5318d991c94e2c7b8e.png)
3. The list of allowlist policies can be managed based on the image ID. It displays the allowed event types of each image. For example, if three images are added to the allowlist, their records will be updated in the list.

#### Editing the allowlist
- Edit the allowlist for an image
 1. On the [**Container Escape**](https://console.cloud.tencent.com/tcss/runtime/containerEscape) > **Allowlist policies** page, click the **Edit allowed types** in the **Operation** column of the target image.
![](https://qcloudimg.tencent-cloud.cn/raw/1930560d8fa2c60d19afb21445c27153.png)
 2. In the **Edit allowed event types** pop-up window, change the allowed event types and click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/0c02eb191332725be4650f7980dbd27f.png)

- Edit the allowlist for multiple images
To change the allowed event types **to the same types** for multiple images, take the following steps:
 1. On the [**Container Escape**](https://console.cloud.tencent.com/tcss/runtime/containerEscape) > **Allowlist policies** page, select one or multiple images and click **Edit allowed types** in the top-left corner.
![](https://qcloudimg.tencent-cloud.cn/raw/2e2b7029c9614be3f024ba6b00dab193.png)
 2. In the **Edit allowed event types** pop-up window, change the allowed event types and click **Save**.
>! After the event type is changed for the selected images, the previously set event type will be cleared.

![](https://qcloudimg.tencent-cloud.cn/raw/1e346509dfa4b1ffd77e404a25e46b20.png)

#### Deleting an image from the allowlist
1. On the [**Container Escape**](https://console.cloud.tencent.com/tcss/runtime/containerEscape) > **Allowlist policies** page, delete one or multiple allowed images.
  - Deleting an allowed image: Select the target image and click **Delete** in the **Operation** column.
![](https://qcloudimg.tencent-cloud.cn/raw/a8ec5bc35f0768b72b4d8740df1846a0.png)
 - Batch deleting allowed images: Select one or multiple images and click **Delete** in the top-left corner.
![](https://qcloudimg.tencent-cloud.cn/raw/fa5fc264deb84bda9c2bdff4866dce01.png)
2. In the pop-up window, click **OK**.
>! Alerts will be triggered when this kind of escape events occur again.
