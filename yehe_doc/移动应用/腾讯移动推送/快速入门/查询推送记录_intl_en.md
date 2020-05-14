## Operation Scenarios
This document describes how to query push records (such as message ID, title, content, sending time, and operation) in the TPNS Console.


## Directions
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **User Operation** > **Mobile Push** > **Push Record** on the left sidebar.
2. On the push record page, click **Detailed Data**.
3. On the detailed data page, data in each process of push delivery is displayed in the form of funnels. The funnels for Android and iOS are different.

**Android:**

 - TPNS channel
   - Planned: number of devices to which the message will be pushed through the TPNS channel when the push condition is met.
   - Sent: number of devices maintaining a persistent connection to the TPNS backend server.
   - Arrived: number of devices at which the message successfully arrived.
   - Displayed: number of devices on which the message was successfully displayed.
   - Tapped: number of devices on which the message was successfully tapped.
   - Dismissed: number of devices on which a message was dismissed.
   - Arrival rate: arrivals/actual pushes.
   - Click rate: number of devices where the notification panel is tapped/number of devices at which the notification message arrives.
   
 - Vendor channel
   - Planned: number of devices to which the message will be pushed through a vendor channel when the push condition is met.
   - Sent: number of messages pushed to the vendor server which returned a success.
   - Arrived: number of devices at which the message successfully arrived.
   - Arrival rate: arrivals/actual pushes.
   
>1. The number of "displayed", "tapped", or "dismissed" messages cannot be returned for vendor channels.
2. The arrival data is for reference only. For the Huawei channel, you need to configure the arrival callback by yourself. For more information, please see [Guide for Getting Arrival Callback Through Vendor Channels](https://intl.cloud.tencent.com/document/product/1024/35246).

**iOS:**

 - Scheduled delivery: number of valid devices (including the devices whose notification panel is disabled) filtered out by the target audience selected by the push.
 - APNs receipts: number of messages that are delivered to APNs for which APNs returns a success (for devices whose notification panel is disabled, APNs will also return a success).
 - Arrivals: number of deduplicated devices at which the message arrives (you need to confirm the completion of the [preparations for integration](https://intl.cloud.tencent.com/document/product/1024/30730). This item is not supported for devices below iOS 10).
 - Tapped: number of devices on which the message was successfully tapped.
 - Click rate: clicks/arrived devices.
