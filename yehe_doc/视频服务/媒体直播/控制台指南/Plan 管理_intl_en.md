You can execute events for a channel while it’s running by adding events to the plan of the channel. StreamLive will perform the specified action at the specified time.

## Viewing events
On the**Channel** page, click the name of the channel for which you want to configure events and select the **Plan** tab.
![](https://qcloudimg.tencent-cloud.cn/raw/56bfba4ce4744f143c35d1e354137ec2.png)


## Creating an event
Click **Create Event**. Currently, the following event types are supported:
- **Input Switch**：Change the input of a running channel.
- **Time Record**: Record a specific segment of a running channel’s output.
- **SCTE-35 Time Signal**：Configure a SCTE-35 time_signal event. 
- **SCTE-35 Splice Insert**：Configure a SCTE-35 splice_insert event. 
- **SCTE-35 Return to Network**：Configure a SCTE-35 return to network event. 

### Creating an Input Switch event
![](https://qcloudimg.tencent-cloud.cn/raw/1d3a818301802f9756723b7613530ff0.png)
- **Event Type**：Select **Input Switch**.
- **Event Name**：Enter the event name, which can be up to 32 characters long, can contain numbers, underscores, and letters, and must be unique across the channel.
- **Start Type**：Select **Fixed Time** or **Immediate**. Fixed Time: Execute the event at a specified time (UTC), which must be at least 10 seconds later than the event configuration time. Immediate: Execute the event immediately.
- **Input Attachment**：From the inputs that have been bound to the channel, select one to change to.


### Creating a Time Record event
![](https://qcloudimg.tencent-cloud.cn/raw/fb95ca51acbcb52561e06323c7585f74.png)
- **Event Type**：Select **Time Record**.
- **Event Name**：Enter the event name, which can be up to 32 characters long, can contain numbers, underscores, and letters, and must be unique across the channel.
- **OutputGroupName**：Select the output group to record. You can view the output groups of a channel on the **Output Group Setting** page.
- **ManifestName**：Enter the name of the manifest file generated (you don’t need to include .m3u8 or .mpd in the name).
- **DestinationUrl**：Enter the COS address to save the file.
- **Timing**：Enter the time period (UTC) to record.


For SCTE-35 event, you can refer to the **SCTE STANDARD - SCTE 35 2022**
### Creating a SCTE-35 Time Signal event
![](https://qcloudimg.tencent-cloud.cn/raw/8131d583336c1a07c561ed63b184c011.png)
- **Event Type**：Select **SCTE-35 Time Signal**.
- **Event Name**：Enter the event name, which can be up to 32 characters long, can contain numbers, underscores, and letters, and must be unique across the channel.
- **Start Type**：Select **Fixed Time** or **Immediate**. Fixed Time: Execute the event at a specified time (UTC), which must be at least 10 seconds later than the event configuration time. Immediate: Execute the event immediately.

Click **Add** to create several SCTE-35 Descriptors。
![](https://qcloudimg.tencent-cloud.cn/raw/700fe3d0d3b8ff43354bad9eba9481a2.png)
For each SCTE-35 Descriptor, you can set following information: 
![](https://qcloudimg.tencent-cloud.cn/raw/7d6b78592a0dc65f6d8ccb788621c6f0.png)

- **Segmentation Event ID**：A 32-bit unique segmentation event identifier. Please enter an integer between 0 and 4294967295.
- **Segmentation Event Cancel Indicator**：Indicates that a previously sent segmentation event, identified by segmentation_event_id, has been cancelled.
- **Delivery Restrictions**：Correspond to SCTE-35 web_delivery_allowed, no_regional_blackout, archive_allowed, device_restrictions parameter.
- **Segmentation Duration**：The duration of the segment in 90kHz ticks. Please enter an integer between 0 and 1099511627775.
- **Segmentation UPID Type**：Correspond to SCTE-35 segmentation_upid_type parameter. Please enter an integer between 0 and 255.
- **Segmentation UPID**：Correspond to SCTE-35 segmentation_upid parameter. Please enter a string which can contain up to 255 characters. Segmentation UPID can be empty only when Segmentation UPID Type is 0.
- **Segmentation Type ID**：Correspond to SCTE-35 segmentation_type_id parameter. Please enter an integer between 0 and 255.
- **Segment Num**：Correspond to SCTE-35 segment_num parameter. Please enter an integer between 0 and 255.
- **Segments Expected**：Correspond to SCTE-35 segment_expected parameter. Please enter an integer between 0 and 255.
- **Subsegment Num**：Correspond to SCTE-35 sub_segment_num parameter. Please enter an integer between 0 and 255.
- **Subsegments Expected**：Correspond to SCTE-35 sub_segments_expected parameter. Please enter an integer between 0 and 255.

### Creating a SCTE-35 Splice Insert event
![](https://qcloudimg.tencent-cloud.cn/raw/60de004766d426563b929e69579345f2.png)
- **Event Type**：Select **SCTE-35 Splice Insert**.
- **Event Name**：Enter the event name, which can be up to 32 characters long, can contain numbers, underscores, and letters, and must be unique across the channel.
- **Start Type**：Select **Fixed Time** or **Immediate**. Fixed Time: Execute the event at a specified time (UTC), which must be at least 10 seconds later than the event configuration time. Immediate: Execute the event immediately.
- **Splice Event ID**：A 32-bit unique segmentation event identifier. Please enter an integer between 0 and 4294967295.
- **Duration**：The duration of the segment in 90kHz ticks. Please enter an integer between 0 and 8589934591.

### Creating a SCTE-35 Return to Network event
![](https://qcloudimg.tencent-cloud.cn/raw/66fc49414496b2dc5caf4fb5cc7bf7d2.png)
- **Event Type**：Select **SCTE-35 Return to Network**.
- **Event Name**：Enter the event name, which can be up to 32 characters long, can contain numbers, underscores, and letters, and must be unique across the channel.
- **Start Type**：Select **Fixed Time** or **Immediate**. Fixed Time: Execute the event at a specified time (UTC), which must be at least 10 seconds later than the event configuration time. Immediate: Execute the event immediately.
- **Splice Event ID**：A 32-bit unique segmentation event identifier for SCTE-35 splice_insert. Please enter an integer between 0 and 4294967295.

## Deleting an event
Find the event to delete, click **Delete** in the **Operation** column, and then click **Confirm** in the pop-up window. You can delete an event that hasn’t been executed or has finished, but not one that is being executed.
![](https://qcloudimg.tencent-cloud.cn/raw/6a12ab835292e5ceb7af23a849991ce7.png)