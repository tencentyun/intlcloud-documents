## Operation Scenarios
You can set the callback mode based on your actual needs. After video processing is completed, the system will submit the processing result and status to the specified address in the specified mode. Callback modes include:
- Normal callback: you can configure a custom callback URL. After an event is completed, the system will send an HTTP request to this URL, which contains the notification content.
- Reliable callback: after an event is completed, the VOD system will put the notifications into a built-in message queue, and then the application server will get and consume the notifications in the queue through a server API. If the requirement for event notification reliability is high, you are recommended to use this mode.



## Directions

1. Log in to the [VOD Console](https://console.cloud.tencent.com/vod) and click **Callback Settings** on the left sidebar to enter the "Callback Settings" page.
2. Click **Settings** to configure the callback.
![](https://main.qcloudimg.com/raw/e5e84c0a0b7b7a855396e9a5576cf859.png)
3. Configure the following parameters based on your actual needs:
 - Callback Mode: select normal callback or reliable callback.
 - Callback URL: this parameter is visible only if the callback mode is set to **Normal Callback**. Please set the address at which the application backend receives callbacks based on your actual needs.
 - Callback Event: select the events for which you want to receive callbacks, including completion of video upload, transcoding, image sprite generating, splicing, deletion, editing, time point screencapturing, and clipping as well as task flow status change.
 >
 >- Among them, task flow status change, video editing completion, and video clipping completion are default callback events.
 >- You can click <img src="https://main.qcloudimg.com/raw/a710a753ba2162f8913e180be4c93269.png"/> to the right of the desired callback event to view the corresponding documentation.
