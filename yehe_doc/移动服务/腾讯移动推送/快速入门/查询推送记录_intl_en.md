## Operation Scenarios
This document describes how to query push records (such as message ID, title, content, sending time, and operation) in the TPNS Console.


## Directions
1. Log in to the [TPNS Console](https://console.cloud.tencent.com/tpns) and select **Message Push** on the left sidebar.
2. On the push record page, click **View Details** (currently, only push records in the last month are retained).
![](https://main.qcloudimg.com/raw/21e42a2a123df32d4b9f3a70bf165db3.png)
3. On the detailed data page, data in each process of push delivery is displayed in the form of funnels. The funnels for Android and iOS are different.

**Android:**
![](https://main.qcloudimg.com/raw/e8f1cd83d57f62d5ff622502bee20b35.png)

 - TPNS channel
   - Attempted: the number of available devices online in the last 90 days with the notification bar enabled out of the push target devices.
   - Sent: the number of available devices to which the message was successfully delivered through the TPNS channel out of the attempted devices.
   - Reached: the number of devices that received the message.
   - Clicked: the number of devices on which the message was clicked.
   - Cleared: the number of devices on which the notification was dismissed.
   - Reach rate: reached/sent.
   - Click rate: the number of devices on which the message was clicked/the number of devices which the notification reached.

 - Vendor channel
   - Attempted: the total number of devices with the notification bar enabled and using vendor channels out of the push target devices.
   - Sent: the number of devices to which the message was pushed through the vendor channel and the vendor server returns a success.
   - Reached: the number of devices that received the message
   - Clicked: the number of devices on which the message was clicked.
   - Reach rate: reached/sent.
   - Click rate: the number of devices on which the message was clicked/the number of devices which the notification reached
   

>?
1. The number of "cleared" messages cannot be returned for vendor channels.
2. The arrival data is for reference only. For the Huawei and Meizu channels, you need to configure the arrival callback by yourself. For more information, please see [Guide for Getting Arrival Callback Through Vendor Channels](https://intl.cloud.tencent.com/document/product/1024/35246).

**Push time analysis**
![](https://main.qcloudimg.com/raw/29272f4bbc158909fb2143a57736e48d.png)
After a push task starts, according to different time granularities:

- By minute: the number of unique devices for each metric per minute within 1 hour.
- By hour: the total number of devices for each metric per hour within 24 hours or 72 hours.

According to different metrics:
- Sent: the number of devices to which the message was successfully delivered in the specified time period.
- Reached devices: the number of devices at which the message arrived in the specified time period.
- Clicked: the number of devices on which the push message was clicked within a specified period.
- Cleared: the number of devices on which the notification was dismissed within a specified period.

>!
1. The "cleared" metric is only supported for the TPNS channel.
2. Push time analysis is not supported for single-device/account pushes or device/account list pushes.
3. The statistics of time metrics are slightly ahead of the statistics in the push funnel, and it is normal if you see small differences in the pushing process.

**iOS:**
![](https://main.qcloudimg.com/raw/e9fe41491d5d631c9270525ae554b9a2.png)

 - Attempted: the number of available devices in the push target devices (including opt-out devices).
 - Sent: the number of devices to which the message was successfully delivered through the APNs or TPNS channel (opt-out devices can also return success)
 - Reached: the number of unique devices that received push messages (make sure you have completed the [integration procedure](https://intl.cloud.tencent.com/document/product/1024/30730). iOS 10 and below versions do not support this statistic item.)
 - Clicked: the number of devices on which the message was clicked.
 - Click rate: clicked/reached devices.


 **Push time analysis**

 ![](https://main.qcloudimg.com/raw/d3bca553a792b165e1e45e3bbed0b957.png)

After a push task starts, according to different time granularities:
- By minute: the number of unique devices for each metric per minute within 1 hour.
- By hour: the total number of devices for each metric per hour within 24 hours or 72 hours.

According to different metrics:
- Sent: the number of devices that received the message through the APNs or TPNS channel within a specified period.
- Reached: the number of devices at which the push message arrived within a specified period.
- Clicked: the number of devices on which the push message was clicked within a specified period.

>!1. Push time analysis is not supported for single-device/account pushes or device/account list pushes.
2. The statistics of timeliness metrics are slightly ahead of the statistics in the push funnel, and it is normal if you see small differences in the pushing process.
