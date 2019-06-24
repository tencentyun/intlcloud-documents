## Operation Scenario
There are two callback modes:
- Normal callback: You can customize the callback URL. After an event is completed, the system sends an HTTP request to this URL, which contains the notification information.
- Reliable callback: After an event is completed, the VOD system inputs the notifications into a built-in message queue, then the APP will retrieve the notifications in the queue through a web service endpoint. We recommend this mode for reliable notifications.

You can set the callback mode based on your needs. After the video is processed, VOD will send a callback notification as specified. 

## Steps

1. Log in to the [VOD Console](https://console.cloud.tencent.com/video) and click **Callback Settings** in the left sidebar to go to the callback configuration page.
2. Click [Settings].
 ![](https://main.qcloudimg.com/raw/1d7e83faf7e1cbd60987f16c221bee64.png)
3. Configure the following parameters:
 - Callback mode: Select normal callback or reliable callback.
 - Callback URL: This parameter is visible only when the **Callback Mode** is **Normal Callback**. Set the callback URL that receives the callback.
 - Callback event: Select the events you want to receive callbacks from, such as completion of video uploading, transcoding, stitching, editing, deleting and clipping, changing task flow status, generating image sprites for screenshots, and taking a point-in-time video screenshot. Specifically, the callbacks for task flow status change, completion of video clipping and editing are required. For more information, click the corresponding callback event icon.
