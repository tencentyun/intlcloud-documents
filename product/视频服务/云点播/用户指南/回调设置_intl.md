## Operation Scenario
There are following modes of callback:
- Normal callback: You can customize the callback URL. After an event is completed, the system sends an HTTP request to this URL, which contains the notification content.
- Reliable callback: After an event is completed, the VOD system puts the notification content into the built-in queue, and the app service consumes the notification in the queue through the server API. This mode is recommended if the requirement for event notification reliability is high.

You can set the callback mode based on actual needs. After the video-related processing is completed, the system will submit the processing result and status to the specified address in the specified method.

## Steps

1. Log in to the [VOD Console](https://console.cloud.tencent.com/video) and click **Callback Settings** in the left navigation pane to go to the callback configuration page.
2. Click [Set].
 ![](https://main.qcloudimg.com/raw/1d7e83faf7e1cbd60987f16c221bee64.png)
3. Configure the following parameters based on actual needs:
 - Callback mode: Select normal callback or reliable callback.
 - Callback URL: This parameter is visible only if **Callback Mode** is set to **Normal Callback**. Please set the app backend address that receives the callback based on actual needs.
 - Callback event: Select the events for which to receive callbacks, including: callback on video upload completion, callback on task flow status change, callback on video transcoding completion, Callback on completion of video image sprite screenshot, callback on video stitching completion, callback on video deletion completion, callback on video editing completion, callback on completion of point-in-time video screenshot, and callback on video clipping completion. Among them, the callbacks upon task flow status change, video clipping completion, and video editing completion are required events. For more information, click the corresponding callback event icon.
