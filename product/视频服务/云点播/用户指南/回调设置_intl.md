## Operation Scenario
The callback has the following modes:
- Normal callback: You can customize the callback URL. After an event is completed, the system sends an HTTP request to this URL, which contains the notification information.
- Reliable callback: After an event is completed, the VOD system puts the notifications into a built-in message queue, then the APP will retrieve the notification in the queue through a web service endpoint. We recommend this mode for higher notification.

You can set the callback mode based on your needs. The API will process the video you have sent then revoke the callback URL by the API method you are calling to send you the response.
## Steps

1. Log in to the [VOD Console](https://console.cloud.tencent.com/video) and click **Callback Settings** in the left navigation pane to go to the callback configuration page.
2. Click [Set].
 ![](https://main.qcloudimg.com/raw/1d7e83faf7e1cbd60987f16c221bee64.png)
3. Configure the following parameters:
 - Callback mode: Select normal callback or reliable callback.
 - Callback URL: This parameter is visible only when the **Callback Mode** is **Normal Callback**. Please set the callback URL that receives the callback based on actual needs.
 - Callback event: Select the events you want to receive callbacks from, including the completion of video uploading, transcoding, stitching, editing, deleting and clipping, changing task flow status, generating image sprites for screenshots, and taking a point-in-time video screenshot. Specifically, the callbacks for task flow status change, completion of video clipping and editing are required. For more information, click the corresponding callback event icon.
