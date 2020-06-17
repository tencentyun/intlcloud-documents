## Operation Scenarios
This document describes how to query push records (such as message ID, title, content, sending time, and operation) in the TPNS Console.


## Directions
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **User Operation** > **Mobile Push** > **Push Record** on the left sidebar.
2. On the **Push Record** page, click **View Details** (only displaying push records within one month).
3. On the detailed data page, data in each process of push delivery is displayed in the form of funnels. The funnels for Android and iOS are different.

**Android:**
![](https://main.qcloudimg.com/raw/e8f1cd83d57f62d5ff622502bee20b35.png)

 - TPNS channel
   - Scheduled: number of devices to which the message will be pushed through the TPNS channel when the push condition is met.
   - Sent: number of devices maintaining a persistent connection to the TPNS backend server.
   - Arrived: number of devices at which the message successfully arrives.
   - Displayed: number of devices on which the message is successfully displayed.
   - Tapped: number of devices on which the message is successfully tapped.
   - Dismissed: number of devices on which a message is dismissed.
   - Arrival rate: arrived/sent.
   - Click rate: number of devices where the notification bar is tapped/number of devices at which the notification message arrives.
   
 - Vendor channel
   - Scheduled: number of devices to which the message will be pushed through a vendor channel when the push condition is met.
   - Sent: number of devices to which the message is pushed through the vendor channel and the vendor server returns a success.
   - Arrived: number of devices at which the message arrives.
   - Arrival rate: arrived/sent.
   
>1. The number of "displayed", "tapped", or "dismissed" messages cannot be returned for vendor channels.
2. The arrival data is for reference only. For the Huawei channel, you need to configure the arrival callback by yourself. For more information, please see [Guide for Getting Arrival Callback Through Vendor Channels](https://intl.cloud.tencent.com/document/product/1024/35246).

**Push timeliness analysis**
After a push task starts, according to different time granularities:

- Minute granularity: the cumulative number of deduplicated devices for the corresponding metric per minute within 1 hour
- Hour granularity: the cumulative metric statistics per hour in 24 hours or 72 hours.

According to different metrics:
- Sent: number of devices to which the message is successfully delivered in the specified time period.
- Arrived: number of devices at which the message arrives in the specified time period.
- Displayed: number of devices on which the message is displayed in the specified time period.
- Tapped: number of devices on which the message is tapped in the notification bar in the specified time period.
- Dismissed: number of devices on which a message is dismissed in the specified time period.

>1. The "displayed", "tapped", and "dismissed" metrics are only supported for the TPNS channel.
2. Timeliness statistics are not available for pushes to one single device account and to device account list.
3. The statistics of timeliness metrics are slightly ahead of the statistics in the push funnel, and it is normal if you see small differences in the pushing process.

**iOS:**
![](https://main.qcloudimg.com/raw/e9fe41491d5d631c9270525ae554b9a2.png)

 - Scheduled: number of valid devices (including the devices whose notification bar is disabled) filtered out by the target audience selected by the push.
 - APNs received: number of messages that are delivered to APNs for which APNs returns a success (for devices whose notification bar is disabled, APNs will also return a success).
 - Arrived: number of deduplicated devices at which the message arrives (you need to confirm the completion of the [preparations for integration](https://intl.cloud.tencent.com/document/product/1024/30730). This item is not supported for devices below iOS 10).
 - Tapped: number of devices on which the message is successfully tapped.
 - Click rate: clicks/arrived devices.


 **Push timeliness analysis**

After a push task starts, according to different time granularities:
- Minute granularity: the cumulative number of deduplicated devices for the corresponding metric per minute within 1 hour
- Hour granularity: the cumulative metric statistics per hour in 24 hours or 72 hours.

According to different metrics:
- APNs received: number of devices on which the message is received by APNs in the specified time period.
- Arrived: number of devices at which the message arrives in the specified time period.
- Tapped: number of devices on which the message is tapped in the notification bar in the specified time period.

>1. Timeliness statistics are not available for pushes to one single device account and to device account list.
2. The statistics of timeliness metrics are slightly ahead of the statistics in the push funnel, and it is normal if you see small differences in the pushing process.
