## Overview
This document describes how to query push records (containing the message ID, title, content, sending time, and operation information) in the Tencent Push Notification Service console.


## Directions
1. Log in to the [Tencent Push Notification Service console](https://console.cloud.tencent.com/tpns), and click **Message Management** > **Task List** in the left sidebar.
2. On the task list page, click **View Details**. (Currently, only push records within the last month are saved.)
![](https://main.qcloudimg.com/raw/90cdb3f17a614ff43ab0fd8dbb3f5994.png)
3. On the **Detailed Data** page, the data from each push process is displayed in funnel format. Android and iOS data funnels are different.

**Android terminals:**
![](https://main.qcloudimg.com/raw/e8f1cd83d57f62d5ff622502bee20b35.png)

 - Tencent Push Notification Service channel
   - Attempted: Of available devices in the push target devices, the number of valid devices that have connected to the server within 90 days and enabled the application's notification bar messages.
   Sent To: Number of available devices to which the message was successfully delivered through the Tencent Push Notification Service channel out of the attempted devices.
   - Reached: Number of devices that received the message.
   - Clicked: Number of devices on which the message was clicked.
   - Cleared: Number of devices on which the notification was dismissed
   - Reach Rate: Reached/Sent to.
   - Click Rate: Clicked/Reached.

 - Vendor channel
   - Attempted: Total number of devices through the vendor channel with the notification bar enabled in the push target devices.
   - Sent To: Pushed to vendor server and the server returned success.
   - Reached: Number of devices that received the message.
   - Clicked: Number of devices on which the message was clicked.
   - Reach Rate: Reached/Sent to.
   - Click Rate: Clicked/Reached.

>?
>1. The number of "cleared" messages cannot be returned for vendor channels.
>2. The arrival data is for reference only. For the Huawei and Meizu channels, you need to configure the arrival callback by yourself. For more information, see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246).

**Push time analysis**
![](https://main.qcloudimg.com/raw/29272f4bbc158909fb2143a57736e48d.png)
According to different time dimensions after the push task is started:

- By minute: Number of unique devices for each metric per minute within one hour.
- By hour: Total number of devices for each metric per hour within 24 hours or 72 hours.

By different metrics:
- Sent To: Number of devices to which the message is successfully delivered in the specified period.
- Reached Devices: Number of devices that received the push message within a specified period.
- Clicked: Number of devices on which the push message was clicked within a specified period.
- Cleared: Number of devices on which the notification was dismissed within a specified period.

>!
>1. The "Cleared" metric is only supported for the Tencent Push Notification Service channel.
>2. Push time analysis is not supported for single-device/account pushes or device/account list pushes.
>3. The statistics of timeliness metrics are slightly ahead of the statistics in the push funnel, and it is normal if you see small differences in the pushing process.

**iOS:**
![](https://main.qcloudimg.com/raw/e9fe41491d5d631c9270525ae554b9a2.png)

Tencent Push Notification Service channel:
 - Attempted: Available devices in the push target devices (excluding devices with the notification bar disabled).
 - Sent To: Actual number of messages successfully delivered by the device through the Tencent Push Notification Service channel.
 - Reached: Number of unique devices that received push messages.
 - Clicked: Number of devices on which the message was clicked.
 - Click Rate: Clicked/Reached devices.
 >?
 >- If no click data is reported after the message is clicked in the notification bar, check whether the application is integrated with XGMTACloud.framework.
 >-The Tencent Push Notification Service channel only takes effect in SDK for iOS 1.2.8.0 and above.

![](https://main.qcloudimg.com/raw/8806e2d1dae2a77a0b1693446de05333.png)
APNs channel:

 - Attempted: Available devices in the push target devices (excluding devices with the notification bar disabled).
 - Sent To: Actual number of messages successfully delivered by the device through the APNs channel.
 - Reached: Unique devices that received push messages (make sure you have completed the [integration procedure](https://intl.cloud.tencent.com/document/product/1024/30730). iOS 10 and below versions do not support this statistic item).
 - Clicked: Number of devices on which the message was clicked.
 - Click Rate: Clicked/Reached devices.
 >? If no click data is reported after the message is clicked in the notification bar, check whether the application is integrated with XGMTACloud.framework.


 **Push time analysis**
 ![](https://main.qcloudimg.com/raw/d3bca553a792b165e1e45e3bbed0b957.png)

According to different time dimensions after the push task is started:
- By minute: Number of unique devices for each metric per minute within one hour.
- By hour: Total number of devices for each metric per hour within 24 hours or 72 hours.

By different metrics:
- Sent To: Number of push messages sent to the APNs or Tencent Push Notification Service channel within a specified period.
- Reached Devices: Number of devices that received the push message within a specified period.
- Clicked: Number of devices on which the push message was clicked within a specified period.

>!
>1. Push time analysis is not supported for single-device/account pushes or device/account list pushes.
>2. The statistics of timeliness metrics are slightly ahead of the statistics in the push funnel, and it is normal if you see small differences in the pushing process.
