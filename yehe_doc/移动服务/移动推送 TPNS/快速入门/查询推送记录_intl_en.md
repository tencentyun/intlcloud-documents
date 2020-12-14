## Overview
This document describes how to query push records (such as message ID, title, content, sending time, and operation) in the TPNS Console.


## Directions
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Push Management** > **Task List** on the left sidebar.
2. Enter the task list page and click **View Details** (currently, only push records within the last month are retained).
![](https://main.qcloudimg.com/raw/90cdb3f17a614ff43ab0fd8dbb3f5994.png)
3. On the details page, data in each process of push delivery is displayed in the form of funnels. The funnels for Android and iOS are different.

**Android:**
![](https://main.qcloudimg.com/raw/e8f1cd83d57f62d5ff622502bee20b35.png)
 - TPNS channel
   - Attempted: of available devices in the push target devices, the number of valid devices that have connected to server within 90 days and enabled the application's notification bar messages.
   - Sent To: number of available devices to which the message was successfully delivered through the TPNS channel out of the attempted devices.
   - Reached: number of devices that received the message.
   - Clicked: number of devices on which the message was clicked.
   - Cleared: number of devices on which the notification was dismissed
   - Reach Rate: reached/sent to.
   - Click Rate: clicked/reached.

 - Vendor channel
   - Attempted: total number of devices through the vendor channel with the notification bar enabled in the push target devices.
   - Sent To: pushed to vendor server and the server returned success.
   - Reached: number of devices that received the message.
   - Clicked: number of devices on which the message was clicked.
   - Reach Rate: reached/sent to.
   - Click Rate: clicked/reached.

>?
>1. The number of "cleared" messages cannot be returned for vendor channels.
>2. The arrival data is for reference only. For the Huawei and Meizu channels, you need to configure the arrival callback by yourself. For more information, please see [Acquisition of Vendor Channel Arrival Receipt](https://intl.cloud.tencent.com/document/product/1024/35246).

**Push time analysis**
![](https://main.qcloudimg.com/raw/29272f4bbc158909fb2143a57736e48d.png)
According to different time dimensions after the push task is started:
- By minute: number of unique devices for each metric per minute within 1 hour.
- By hour: total number of devices for each metric per hour within 24 hours or 72 hours.

By different metrics:
- Sent To: number of devices to which the message is successfully delivered in the specified period.
- Reached Devices: number of devices that received the push message within a specified period.
- Clicked: number of devices on which the push message was clicked within a specified period.
- Cleared: number of devices on which the notification was dismissed within a specified period.

>!
>1. The "Cleared" metric is only supported for the TPNS channel.
>2. Push time analysis is not supported for single-device/account pushes or device/account list pushes.
>3. The statistics of timeliness metrics are slightly ahead of the statistics in the push funnel, and it is normal if you see small differences in the pushing process.

**iOS:**
![](https://main.qcloudimg.com/raw/e9fe41491d5d631c9270525ae554b9a2.png)

TPNS channel:
 - Attempted: available devices in the push target devices (excluding opt-out devices).
 - Sent To: actual number of messages successfully delivered by the device through the TPNS channel.
 - Reached: number of unique devices that received push messages.
 - Clicked: number of devices on which the message was clicked.
 - Click Rate: clicked/reached devices.
 >?
 >- If no click data is reported after the message is clicked in the notification bar, please check whether the application is integrated with `XGMTACloud.framework`.
 >- The TPNS channel only takes effect in SDK for iOS 1.2.8.0 and above.


APNs channel:

 - Attempted: available devices in the push target devices (excluding opt-out devices).
 - Sent To: actual number of messages successfully delivered by the device through the APNs channel.
 - Reached: unique devices that received push messages (make sure you have completed the [integration procedure](https://intl.cloud.tencent.com/document/product/1024/30730). iOS 10 and below versions do not support this statistic item).
 - Clicked: number of devices on which the message was clicked.
 - Click Rate: clicked/reached devices.
 >?If no click data is reported after the message is clicked in the notification bar, please check whether the application is integrated with `XGMTACloud.framework`.


**Push time analysis**
 ![](https://main.qcloudimg.com/raw/d3bca553a792b165e1e45e3bbed0b957.png)

According to different time dimensions after the push task is started:
- By minute: number of unique devices for each metric per minute within 1 hour.
- By hour: total number of devices for each metric per hour within 24 hours or 72 hours.

By different metrics:
- Sent To: number of push messages sent to the APNs or TPNS channel within a specified period.
- Reached: number of devices that received the push message within a specified period.
- Clicked: number of devices on which the push message was clicked within a specified period.

>!
>1. Push time analysis is not supported for single-device/account pushes or device/account list pushes.
>2. The statistics of timeliness metrics are slightly ahead of the statistics in the push funnel, and it is normal if you see small differences in the pushing process.
