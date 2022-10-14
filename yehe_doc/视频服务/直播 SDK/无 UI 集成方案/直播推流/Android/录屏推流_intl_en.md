## Overview
Publishing from screen means using hosts’ phones as the source for live streaming. It may be combined with local camera preview and is used in scenarios such as game streaming and mobile application demonstration. Tencent Cloud’s LiteAVSDK offers the screen sharing capability via `V2TXLivePusher`. 
>? By adding a floating window to display the image of the local camera, you can include camera preview into the streams published from the screen.

![](https://qcloudimg.tencent-cloud.cn/raw/9b1e9e834cc16a1e5bf6d821e3b2d2da.png)

## Restrictions
- Screen recording is supported in Android 5.0 and above.
- Floating windows need to be enabled manually on some mobile phones and systems.

## Sample Code

| Platform |                         GitHub Address                          |
| :------: | :----------------------------------------------------------: |
| iOS | [LivePushScreenViewController.m](https://github.com/LiteAVSDK/Live_iOS/blob/main/MLVB-API-Example-OC/Basic/LivePushScreen/LivePushScreenViewController.m) |
| Android | [LivePushScreenActivity.java](https://github.com/LiteAVSDK/Live_Android/blob/main/MLVB-API-Example/Basic/LivePushScreen/src/main/java/com/tencent/mlvb/livepushscreen/LivePushScreenActivity.java) |
| Flutter | [live_screen_push.dart](https://github.com/LiteAVSDK/Live_Flutter/blob/main/Live-API-Example/lib/page/push/live_screen_push.dart) |


## Integration
[](id:step1)
### Step 1. Download SDK development kit

[Download](https://www.tencentcloud.com/document/product/1071/38150) the SDK and follow the instructions in [SDK Integration](https://www.tencentcloud.com/document/product/1071/38156) to integrate the SDK into your application.

[](id:step2)
### Step 2. Configure License Authorization for SDK
1. Obtain license authorization：
    - If you have obtained the relevant license authorization，Need to Get License URL and License Key in [Cloud Live Console](https://console.tencentcloud.com/live/license)
    ![](https://qcloudimg.tencent-cloud.cn/raw/a6b24e8677c514ee1721d38893fd9ca2.png)
    - If you have not yet obtained the license authorization，Please reference [Adding and Renewing Licenses](https://www.tencentcloud.com/document/product/1071/38546) to make an application.
2.  Before your App calls SDK-related functions (it is recommended in the Application class), set the following settings:
```java
public class MApplication extends Application {

@Override
public void onCreate() {
    super.onCreate();
    String licenceURL = ""; // your licence url
    String licenceKey = ""; // your licence key
    V2TXLivePremier.setEnvironment("GDPR");  // set your environment
    V2TXLivePremier.setLicence(this, licenceURL, licenceKey);
    V2TXLivePremier.setObserver(new V2TXLivePremierObserver() {
            @Override
            public void onLicenceLoaded(int result, String reason) {
                Log.i(TAG, "onLicenceLoaded: result:" + result + ", reason:" + reason);
            }
        });
}
```

>! **The packageName configured in the license must be the same as the application itself, otherwise the push stream will fail.**

[](id:step3)
### Step 3. Add Activity

Paste the following activity in the manifest file (no need to add it if it exists in the project code).

```xml
<activity 
    android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity" 
    android:theme="@android:style/Theme.Translucent"/>
```

[](id:step4)
### Step 4. Create a stream publishing object
Create a **V2TXLivePusher** object, which will be responsible for publishing operations.

```java

// Specify the corresponding live broadcast protocol as RTMP, which does not support mic connection
V2TXLivePusher mLivePusher = new V2TXLivePusherImpl(this, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTMP);
```

[](id:step5)
### Step 5. Start stream publishing
Use [startScreenCapture](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusher__android.html#acd14289e3bbf2708f23e61348136d9f9) to start screen recording，and use V2TXLivePusher::[startPush](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusher__android.html#ab4f8adaa0616d54d6ed920e49377a08a) to pushing
>? if you choose `RTMP` protocol to push in [Step4](#step4)，The generate of the push URL, please refer to [RTMP URL](https://www.tencentcloud.com/document/product/267/7977)。

```java
// The push stream can be started according to the push stream protocol. RTMP cannot connect to the microphone. It should use rtmp:// to connect to the microphone.
String url = "rtmp://test.com/live/streamid?txSecret=xxxxx&txTime=xxxxxxxx";
mLivePusher.startMicrophone();
mLivePusher.startScreenCapture();
int ret = mLivePusher.startPush(url);
if (ret == V2TXLIVE_ERROR_INVALID_LICENSE) {
    Log.i(TAG, "startRTMPPush: license verification failed");
}
```
>!
> - **Reason for returning V2TXLIVE_ERROR_INVALID_LICENSE?** 
> If the `startPush` interface returns `V2TXLIVE_ERROR_INVALID_LICENSE`, it means that your license verification failed, please check the url and key set in [Step 2: Configure the SDK for license authorization](#step2).
> - **startScreenCapture** is used to start screen recording, which is a built-in feature of the Android system. For security reasons, before screen recording starts, Android will pop up a window asking users whether to start screen recording, and you should agree.


[](id:step6)
### Step 6. Set watermarks
Call [setWatermark](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusher__android.html#a4f56a5a937d87e5b1ae6f77c5bab2335) in `V2TXLivePusher` to add a watermark to videos output by the SDK. The position of the watermark is determined by the `(x, y, scale)` parameter passed in.

- The watermark image must be in PNG rather than JPG format. The former carries opacity information, which allows the SDK to better address the image aliasing issue (changing the extension of a JPG image to PNG won’t work).
- The `(x, y, scale)` parameter specifies the normalized coordinates of the watermark relative to the resolution of the published video. For example, if the resolution of the published video is 540 x 960, and `(x, y, scale)` is set to `（0.1, 0.1, 0.1）`, the actual pixel coordinates of the watermark will be (540 x 0.1, 960 x 0.1). The width of the watermark will be the video width x 0.1, and the height will be scaled automatically.

```java 
// Set a video watermark 
mLivePusher.setWatermark(BitmapFactory.decodeResource(getResources(),R.drawable.watermark), 0.03f, 0.015f, 1f); 
```

[](id:step7)
### Step 7. Set video quality
Call `setVideoQuality` in `V2TXLivePusher` to set the quality of videos watched by audience. The encoding parameters set determine the quality of videos presented to audience. The local video watched by the host is the original HD version that has not been encoded or compressed, and is therefore not affected by the settings. For details, please see [Setting Video Quality](https://www.tencentcloud.com/document/product/1071/41861).

[](id:step8)
### Step 8. Inform hosts of poor network conditions
Connecting phones to Wi-Fi does not necessarily guarantee network conditions. In case of poor Wi-Fi signal or limited bandwidth, the network speed of a Wi-Fi connected phone may be slower than that of a phone using 4G. Hosts should be informed when their network conditions are bad and be prompted to switch to a different network.    
![](https://main.qcloudimg.com/raw/faaef46a80988270d3ddc96ec4e578b9.png)  

You can capture the **V2TXLIVE_WARNING_NETWORK_BUSY** event using [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLiveCode__android.html) in `V2TXLivePusherObserver`. The event indicates poor network conditions for hosts, which result in stuttering for audience. When this event occurs, you can send a UI message about poor network conditions to hosts, as shown above.
<dx-codeblock>
::: objectiveC objectiveC
@Override
public void onWarning(int code, String msg, Bundle extraInfo) {
    if (code == V2TXLiveCode.V2TXLIVE_WARNING_NETWORK_BUSY) {
        showNetBusyTips(); // Show a “network busy” message
    }
} 
:::
</dx-codeblock>

[](id:step9)
### Step 9. Set the orientation
In most cases, hosts stream while holding their phones vertically, and audience watch videos in portrait resolutions (e.g., 540 × 960). However, there are also cases where hosts hold phones horizontally, and ideally, audience should watch videos in landscape resolutions (960 × 540), as shown below: 
    

By default, `V2TXLivePusher` outputs videos in portrait resolutions. You can output landscape-mode videos to audience by modifying a parameter of the [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a2695806cb6c74ccce4b378d306ef0a02) API.

```java 
mLivePusher.setVideoQuality(mVideoResolution, isLandscape ? V2TXLiveVideoResolutionModeLandscape : V2TXLiveVideoResolutionModePortrait);   
```

[](id:step10)
### Step 10. Stop publishing streams
As there can be only one `V2TXLivePusher` object running at a time, make sure that you release all the resources when stopping publishing.
```java
// Stop screen sharing and release the resources
public void stopPublish() {
    mLivePusher.stopScreenCapture();
    mLivePusher.setObserver(null);
    mLivePusher.stopPush();
}
```

## Event Handling

### Listening for events
The SDK listens for publishing events and errors via the [V2TXLivePusherObserver](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusherObserver__android.html) delegate. See [V2TXLiveCode](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLiveCode__android.html) for a detailed list of events and error codes.

### Errors
An error indicates that the SDK encountered a serious problem that made it impossible for stream publishing to continue.

| Event ID | Code | Description |
| :------------------------------------ | :---- | :------------------------------- |
|V2TXLIVE_ERROR_FAILED                  | -1 | A common error not yet classified |
| V2TXLIVE_ERROR_INVALID_PARAMETER       | -2 | An invalid parameter was passed in during API calling. |
|V2TXLIVE_ERROR_REFUSED                 | -3 | The API call was rejected.  |
|V2TXLIVE_ERROR_NOT_SUPPORTED           | -4 | The API cannot be called.  |
|V2TXLIVE_ERROR_INVALID_LICENSE         | -5 | Failed to call the API due to invalid license.  |
|V2TXLIVE_ERROR_REQUEST_TIMEOUT         | -6 | The server request timed out.  |
|V2TXLIVE_ERROR_SERVER_PROCESS_FAILED   | -7 | The server could not handle your request.  |

### Warnings
A warning indicates that the SDK encountered a problem whose severity level is warning. Warning events trigger tentative protection or recovery logic and can often be resolved.

| Event ID                                       | Code  | Description                                                     |
| :-------------------------------------------- | :---- | :----------------------------------------------------------- |
|V2TXLIVE_WARNING_NETWORK_BUSY                  |  1101|  Bad network connection: data upload blocked due to limited upstream bandwidth. |
|V2TXLIVE_WARNING_VIDEO_BLOCK                   |  2105|  Stuttering during video playback.  |
|V2TXLIVE_WARNING_CAMERA_START_FAILED           | -1301|  Failed to turn the camera on.  |
|V2TXLIVE_WARNING_CAMERA_OCCUPIED               | -1316| The camera is occupied. Try a different camera. |
|V2TXLIVE_WARNING_CAMERA_NO_PERMISSION          | -1314| No access to the camera. This usually occurs on mobile devices and may be because the user denied the access. |
|V2TXLIVE_WARNING_MICROPHONE_START_FAILED       | -1302| Failed to turn the mic on. |
|V2TXLIVE_WARNING_MICROPHONE_OCCUPIED           | -1319| The mic is occupied. This occurs when, for example, the user is having a call on the mobile device. |
|V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION      | -1317| No access to the mic. This usually occurs on mobile devices and may be because the user denied the access. |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED  | -1309|  The system does not support screen sharing.  |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED   | -1308|  Failed to start screen recording. If this occurs on a mobile device, it may be because the user denied the access.  |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED    | -7001|  Screen recording was stopped by the system.  |
