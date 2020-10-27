## Feature
Camera push refers to the process of collecting images from the camera of the mobile phone and voice from the microphone, encoding the video and audio data, and pushing the data to the livestreaming cloud platform. Tencent Cloud LiteAVSDK calls the `V2TXLivePusher` API to provide the camera push capability. The figure below shows the interfaces for camera push operations demonstrated in the LiteAVSDK demo.
![](https://main.qcloudimg.com/raw/f4df6e007076f4629629f5d75f14d86d.png)

## Sample Code

| Platform | GitHub URL | Key Class |
|:---------:|:--------:|:---------:|
| iOS | [Github](https://github.com/tencentyun/LiteAVInternational) | CameraPushMainViewController.m |
| Android | [Github](https://github.com/tencentyun/LiteAVInternational) | CameraPusherActivity.java |


## Feature Interfacing

### 1. Download the SDK

[Download](https://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_International_Android_lastest.zip) the SDK and follow the instructions in the [SDK integration guide](https://intl.cloud.tencent.com/document/product/1071/38156) to embed the SDK in your application project.

<span id="step2"></span>

### 2. Configure a license for the SDK

Click [Apply for a License](https://console.cloud.tencent.com/live/license) to obtain the license for testing. You will receive two strings. One is the license URL, and the other is the decryption key.

Before you call the LiteAVSDK features in your app, we recommend that you complete the following configurations in `Application`:

```
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // Obtained licence URL
        String licenceKey = ""; // Obtained licence key
        TXLiveBase.getInstance().setLicence(this, licenceURL, licenceKey);
    }
}
```

### 3. Initialize the V2TXLivePusher component
First, create a `V2TXLivePusher ` instance. Later, this instance can be used to implement all the following push-related capabilities, including starting or stopping stream push, starting or stopping data collection from the camera, starting or stopping data collection from the microphone, starting or stopping headphone monitoring, setting the voice quality, and setting the image quality.

```
V2TXLivePusher txLivePusher = new V2TXLivePusherImpl(mContext);
```

### 4. Enable camera preview

You can call the `setRenderView` API in `V2TXLivePusher` to enable the camera preview for the mobile phone. You must provide a view object for previewing images for the `setRenderView` API.

```
<com.tencent.rtmp.ui.TXCloudVideoView   
    android:id="@+id/video_view"  
    android:layout_width="match_parent" 
    android:layout_height="match_parent" /> 
```
Set render view:

```
TXCloudVideoView videoView = (TXCloudVideoView) findViewById(R.id.video_view);
txLivePusher.setRenderView(videoView);
```

### 5. Start and stop stream push
If you have called the `setRenderView` API to enable camera preview, you can call the `startPush` API of `V2TXLivePusher` to start pushing streams.

```
// Enter your RTMP URL for stream push.
String rtmpURL = "rtmp://test.com/live/xxxxxx"; 
// Start collecting data from the camera.
txLivePusher.startCamera();
// Start collecting data from the microphone.
txLivePusher.startMicrophone();
// Start push streams.
txLivePusher.startPush(rtmpURL);
```

After you complete stream push, you can call the `stopPush` API of `V2TXLivePusher` to stop stream push.

```
// Stop pushing streams
txLivePusher.stopPush();
```

-  **How can I obtain a valid push URL？**

After you activate the LVB service, you can choose LVB console > Auxiliary tools > [URL generator](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) to generate a push URL. For more information, see [Push/Pull URL](https://intl.cloud.tencent.com/document/product/267/31059).
![](https://main.qcloudimg.com/raw/cf62d6a6e117bdb9a8d3ca68bf20a5c4.png)

- **Why is “-5” returned?**
If the `startPush` API returns “-5”, license verification has failed. In this case, check whether any problem occurred in [Step 2. Configure a license for the SDK](#step2).


### 6. Push pure audio streams
If you only need to push pure audio streams, perform the following operations:

```
String rtmpURL = "rtmp://test.com/live/xxxxxx"; // Enter your RTMP URL for stream push.
// Start collecting data from the microphone.
txLivePusher.startMicrophone();
// Start push streams.
txLivePusher.startPush(rtmpURL);
```

### 7. Set the video resolution
You can call the `setVideoQuality` API of `TXLivePusherV2` to set the video resolution, aspect ratio, and portrait or landscape mode for the audience.

```
// Select the portrait mode and set the aspect ratio to 1280x720. The first parameter is the video resolution, and the second parameter is the portrait or landscape mode.
txLivePusher.setVideoQuality(V2TXLiveVideoResolution_1280x720, V2TXLiveVideoResolutionMode_Portrait];
```

### 8. Set the beauty filter, whitening, and rosy skin effects.

```
/* 
* With the beauty manager, you can use the following features:
* - Set the following cosmetic effects: beauty style, whitening, ruddy, big eyes, slim face, V-shape face, chin, short face, small nose, bright eyes, white teeth, remove eye bags, remove wrinkles, remove laugh lines.
* - Adjust the hairline, eye spacing, eye corners, mouth shape, nose wings, nose position, lip thickness, and face shape.
* - Set animated effects such as face widgets (materials).
* - Add makeup effects.
* - Recognize gestures.
*/
TXBeautyManager beautyManager = txLivePusher.getBeautyManager();
beautyManager.setBeautyLevel(6);
```

### 9. Control camera behaviors

`TXLivePusherV2` provides an API to obtain the video device manager, `TXVideoDeviceManager`, which is used to control camera behaviors.

| API Function | Description | Remarks |
|---------|---------|---------|
| switchCamera | Switch between the front and rear cameras. |  |
| enableCameraFlash | Enable or disable the flash. | This function is valid only when the current camera is a rear camera.|
| getCameraZoomMaxRatio | Get max zoom ratio. |  |
| setCameraZoomRatio | Adjust the zoom ratio. | The valid range of the zoom ratio is 1 - `getCameraZoomMaxRatio`. Default: 1. |
| setCameraFocusPosition | Set the focus position. | To use this setting, `enableCameraAutoFocus` must be used to disable auto focus.|

### 10. Set the mirror effect on the audience side
You can call the `setEncoderMirror` API of `V2TXLivePusher` to set the mirror effect on the audience side. This mirror effect is different from that on the host side. When the host uses the front camera for livestreaming, the view seen by the host is inverted by the SDK by default. Therefore, the host’s display is like looking in a mirror. `setEncoderMirror` only affects the mirror effect on the audience side.


### 11. Set the audio quality
```
// Pay attention to the calling sequence：
// You must set the audio quality before pushing streams. Otherwise, the audio quality setting does not take effect.
txLivePusher.setAudioQuality(V2TXLiveDef.V2TXLiveAudioQuality.V2TXLiveAudiOQuality_Music);
txLivePusher.startPush();
```

### 12. Set the background music (BGM), voice changing effect, and reverb effect.
```
/**    
* With the audio effect manager, you can use the following features:
* - Adjust the volume of human voice collected by the microphone.
* - Set the reverb and voice changing effects.
* - Start the headphone monitor, and set the volume of the headphone monitor.
* - Add the BGM, and adjust the playback effect of BGM.
*/
TXAudioEffectManager manager = txLivePusher.getAudioEffectManager();
```

### 13. Set the logo watermark

You can call the `setWatermark ` API of `V2TXLivePusher ` to allow the SDK to add a watermark to the pushed video stream. 

- The SDK requires that the watermark image be in png format, instead of jpg, because the png format provides the transparency information and allows the SDK to better address the image aliasing issue. If a jpg image is modified in the Windows system, its extension does not take effect.
- `x,y` is the normalized coordinates of the watermark image relative to the resolution of the pushed video. If the resolution of the pushed video is 540 × 960, and  set to (0.1, 0.1, 0.1, 0.0), the actual pixel coordinates of the watermark are: 540 × 0.1, 960 × 0.1, Watermark width × 0.1, Automatically calculated watermark height.

```java
Bitmap bitmap = decodeResource(getResources(), R.drawable.filter_water);
txLivePusher.setWatermark(bitmap, 0.1f, 0.1f, 0.1f);
```

## Event Handling

### 1. Event listening

The SDK uses the `V2TXLivePusherObserver`proxy to set the pusher callback. By setting the callback, you can monitor some callback events of `V2TXLivePusher `, including the player status, volume callback, statistics, warnings, and error messages. 

```
txLivePusher.setObserver(new V2TXLivePusherObserver());
```

### 2. Normal events
The table below lists the events you will be notified of upon each successful push. If “0” is received, the related event is called successfully.

| Event ID                 |    Value  |  Description                    |
| :-------------------  |:-------- |  :------------------------ |
|V2TXLIVE_OK            | 0 | Successfully called the push event. |

### 3. Error events 
The push cannot continue because the SDK detected a critical problem. For example, when the user revokes the camera permission for the app, the camera cannot be started.

| Error ID                      | Value | Description       |
| ------------------------------ | ---- | ----------- |
| V2TXLIVE_ERROR_FAILED            | -1   | Failed.   |
| V2TXLIVE_ERROR_INVALID_PARAMETER | -2   | Invalid parameter.|
| V2TXLIVE_ERROR_REFUSED           | -3   | Refused.   |
| V2TXLIVE_ERROR_NOT_SUPPORTED     | -4   | Not supported.|
| V2TXLIVE_ERROR_INVALID_LICENSE   | -5   | Invalid license.|

```
@Override
public void onError(int code, String msg, Bundle extraInfo) {
    // doSomething
}
```

### 4.  Warning events 
The SDK detects some warning events. These events can trigger tentative protection logic or restoration logic. Warnings can often be recovered from.

| Warning ID                 |    Value  |  Description                    |
| :-------------------  |:-------- |  :------------------------ |
|V2TXLIVE_WARNING_NETWORK_BUSY            |  1101| Poor network connection. Data upload is blocked because the upstream bandwidth is too low.|
|V2TXLIVE_WARNING_VIDEO_BLOCK           | 2105 | Video lag occurs. |
| V2TXLIVE_WARNING_CAMERA_START_FAILED  | -1301 | Failed to start the camera.  |
| V2TXLIVE_WARNING_CAMERA_OCCUPIED      | -1316 | Camera occupied.          |
| V2TXLIVE_WARNING_CAMERA_NO_PERMISSION | -1314 | No permission to access the camera. This error often occurs on a mobile device when the permission is revoked by the user. |
| V2TXLIVE_WARNING_MICROPHONE_START_FAILED  | -1302 | Failed to start the microphone. |
| V2TXLIVE_WARNING_MICROPHONE_OCCUPIED      | -1319 | Microphone occupied. For example, if a mobile device has an ongoing call, the attempt to start the microphone will fail. |
| V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION | -1317 | No permission to access the microphone. This error often occurs on a mobile device when the permission is revoked by the user.|

```
@Override
public void onWarning(int code, String msg, Bundle extraInfo) {
    // doSomething
}
```
