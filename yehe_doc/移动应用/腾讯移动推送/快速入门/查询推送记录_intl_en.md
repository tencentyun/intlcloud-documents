## Operation Scenarios
This document describes how to query push records (such as message ID, title, content, sending time, and operation) in the TPNS Console.


## Directions
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **User Operation** > **Mobile Push** > **Push Record** on the left sidebar.
2. On the push record page, click **Detailed Data**.
3. On the detailed data page, data in each process of push delivery is displayed in the form of funnels. The funnels for Android and iOS are different.

**Android:**
 - Self-built channel
   - Planned: number of devices to which the message will be pushed through a self-built channel when the push condition is met.
   - Sent: number of devices maintaining a persistent connection to the TPNS backend server.
   - Arrived: number of devices at which the message successfully arrived.
   - Displayed: number of devices on which the message was successfully displayed.
   - Tapped: number of devices on which the message was successfully tapped.
   - Dismissed: number of devices on which a message was dismissed.
 - Vendor-specific channel
   - Planned: number of devices to which the message will be pushed through a vendor-specific channel when the push condition is met.
   - Sent: number of messages pushed to the vendor server which returned a success.
   - Arrived: number of devices at which the message successfully arrived.
   
>1. The number of "displayed", "tapped", or "dismissed" messages cannot be returned for vendor-specific channels.
2. The arrival data is for reference only. For the Huawei channel, you need to configure the arrival callback by yourself. For more information, please see [Guide for Getting Arrival Callback Through Vendor-Specific Channels](https://intl.cloud.tencent.com/document/product/1024/35246).

**iOS:**
 - Planned: number of devices to which the message will be pushed when the push condition is met.
 - Received by APNs: number of messages that successfully arrived at APNs for which APNs returned a success.
 - Arrived: number of devices at which the message successfully arrived.
 - Tapped: number of devices on which the message was successfully tapped.
