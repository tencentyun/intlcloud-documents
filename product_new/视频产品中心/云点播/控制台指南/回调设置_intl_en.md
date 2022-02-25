## Overview
You can set the callback mode based on your actual needs. After video processing is completed, the system will submit the processing result and status to the specified address via the specified mode. Callback modes include:
- Normal callback: you can configure a custom callback URL. After an event is completed, the system will send an HTTP request to this URL, which contains the notification content.
- Reliable callback: after an event is completed, the VOD system will put the notifications into a built-in message queue, and then the application server will get and consume the notifications in the queue through a server API. If the requirement for event notification reliability is high, you are recommended to use this mode.



## Directions

1. Log in to the [VOD console](https://console.cloud.tencent.com/vod) and click **Callback Settings** on the left sidebar.
2. Click **Set** to configure the callback.
![](https://main.qcloudimg.com/raw/ec6cca4bdcd52698e1c7b795c5d3ad7a.png)
3. Configure the following parameters based on your actual needs:
 - Event Notification Method: select Normal Callback or Reliable Callback.
 - Callback URL: this parameter is displayed only if the event notifcation method is set to **Normal Callback**. Set the address at which the application backend receives callbacks based on your actual needs.
 - Event Notification: select the events for which you want to receive callbacks, including video upload completion, video deletion, video composition completion, WeChat publishing completion, task flow status change, and video editing completion.
 >?
 >- Among them, task flow status change, video composition completion, and video editing completion are selected by default.
 >- You can click <img src="https://main.qcloudimg.com/raw/a710a753ba2162f8913e180be4c93269.png"/> to the right of the desired callback event to view the corresponding documentation.
