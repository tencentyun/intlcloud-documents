You can execute events for a channel while it’s running by adding events to the plan of the channel. StreamLive will perform the specified action at the specified time.

## Viewing events
On the **Channel Management** page, click the name of the channel for which you want to configure events and select the **Plan** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/1dd3eebf1e4e7714c29a1302d65a514b.png)
![](https://qcloudimg.tencent-cloud.cn/raw/907a629dac8736d4780d411f2988d33f.png)

## Creating an event
Click **Create Event**. Currently, the following event types are supported:
- Input Switch: Change the input of a running channel
- Time Record: Record a specific segment of a running channel’s output

### Creating an Input Switch event
<img src="https://qcloudimg.tencent-cloud.cn/raw/8136ad53ef809a22070e80f29a86cf84.png" style="zoom:80%;" />

- **Event Type**: Select **Input Switch**.
- **Input Attachment**: From the inputs that have been bound to the channel, select one to change to.
- **Event Name**: Enter the event name, which can be up to 32 characters long, can contain numbers, underscores, and letters, and must be unique across the channel.
- **Start Type**: Select **Fixed Time** or **Immediate**. Fixed Time: Execute the event at a specified time (UTC), which must be at least 10 seconds later than the event configuration time. Immediate: Execute the event immediately.

### Creating a Time Record event
<img src="https://qcloudimg.tencent-cloud.cn/raw/395c7b5bc4023a9160ada53913eea58c.png" style="zoom:80%;" />

- **Event Type**: Select **Time Record**.
- **Event Name**: Enter the event name, which can be up to 32 characters long, can contain numbers, underscores, and letters, and must be unique across the channel.
- **OutputGroupName**: Select the output group to record. You can view the output groups of a channel on the **Output Group Setting** page.
- **ManifestName**: Enter the name of the manifest file generated (you don’t need to include .m3u8 or .mpd in the name).
- **DestinationUrl**: Enter the COS address to save the file.
- **Timing**: Enter the time period (UTC) to record.

## Deleting an event
Find the event to delete, click **Delete** in the **Operation** column, and then click **Confirm** in the pop-up window. You can delete an event that hasn’t been executed or has finished, but not one that is being executed.
![](https://qcloudimg.tencent-cloud.cn/raw/dae329be1090cbeb1b1705fe98fdef3d.png)