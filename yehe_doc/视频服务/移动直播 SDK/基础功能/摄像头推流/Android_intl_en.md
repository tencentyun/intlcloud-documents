## Overview

Camera publishing refers to the process of collecting video and audio data from the mobile phone’s camera and mic, encoding the data, and publishing it to cloud-based live streaming platforms. Tencent Cloud’s LiteAVSDK provides the camera publishing capability via `V2TXLivePusher`. The figure below shows the UI for camera publishing operations in the Video Cloud Toolkit app.
![#800px](https://main.qcloudimg.com/raw/52ee09ae4039d24f39e3cf8110e632c7.jpg)

## Notes
**Testing on real devices:** the SDK uses a lot of audio and video APIs of the Android system, most of which cannot be used on emulators. Therefore, we recommend that you test your project on a real device.

## Sample Code
| Platform |                         GitHub Address                          |           Key Class            |
| :------: | :----------------------------------------------------------: | :-------------------------: |
|   iOS    | [GitHub](https://github.com/tencentyun/LiteAVProfessional_iOS/blob/master/Demo/TXLiteAVDemo/LivePusherDemo/CameraPushDemo/CameraPushViewController.m) | CameraPushViewController.m  |
| Android  | [GitHub](https://github.com/tencentyun/LiteAVProfessional_Android/blob/master/Demo/livepusherdemo/src/main/java/com/tencent/liteav/demo/livepusher/camerapush/ui/CameraPushMainActivity.java) | CameraPushMainActivity.java |


## Feature Integration

[](id:step1)
### 1. Download the SDK

[Download](https://intl.cloud.tencent.com/document/product/1071/38150) the SDK and follow the instructions in [SDK Integration](https://intl.cloud.tencent.com/document/product/1071/38156) to integrate the SDK into your application.

[](id:step2)
### 2. Configure a license for the SDK
Click [Get License](https://console.cloud.tencent.com/live/license) to obtain a trial license. You will get two strings: a license URL and a decryption key.
Before you use the features of the Enterprise Edition SDK in your application, complete the following configurations (preferably in the application class):
```java
public class MApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        String licenceURL = ""; // The license URL obtained
        String licenceKey = ""; // The license key obtained
        TXLiveBase.getInstance().setLicence(this, licenceURL, licenceKey);
    }
}
```

[](id:step3)

### 3. Initialize the `V2TXLivePusher` component

Create a `V2TXLivePusher` object, which will be responsible for most of the publishing operations.

```java   
V2TXLivePusher mLivePusher = new V2TXLivePusherImpl(this, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTMP); // Set the live streaming protocol to RTMP
```

[](id:step4)
### 4. Enable camera preview  

Before enabling camera preview, you must first provide the SDK with a `TXCloudVideoView` object to display video images. Given that `TXCloudVideoView` is inherited from `FrameLayout` in Android, you can:
1. Add a video rendering control in the XML file:    
```xml  
<com.tencent.rtmp.ui.TXCloudVideoView   
              android:id="@+id/pusher_tx_cloud_view"  
              android:layout_width="match_parent" 
              android:layout_height="match_parent" /> 
```
2. Call `startCamera` in `V2TXLivePusher` to enable camera preview for your mobile phone. 
```java     
// Enable preview for the local camera    
TXCloudVideoView mPusherView = (TXCloudVideoView) findViewById(R.id.pusher_tx_cloud_view); 
mLivePusher.setRenderView(mPusherView);
mLivePusher.startCamera(true);
```

[](id:step5)
### 5. Start and stop publishing streams  

After enabling camera preview, you can call [startPush](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#ab4f8adaa0616d54d6ed920e49377a08a) in `V2TXLivePusher` to start stream publishing.  
<dx-codeblock>
::: java java
// Start publishing streams
String rtmpURL = "rtmp://test.com/live/xxxxxx"; // Enter your RTMP URL for stream publishing  
int ret = mLivePusher.startPush(rtmpURL.trim());  
if (ret == V2TXLIVE_ERROR_INVALID_LICENSE) {    
    Log.i(TAG, "startRTMPPush: license verification failed");  
}       
:::
</dx-codeblock>

Call [stopPush](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#af07c1dcff91b43a2309665b8663ed530) in `V2TXLivePusher` to stop publishing streams.
```java 
// Stop publishing streams
mLivePusher.stopPush();
```
>!If you have enabled camera preview, please disable it when you stop publishing streams.  

- **How can I obtain a valid push URL?** 
To generate a publishing URL, activate CSS, and go to the [**CSS console** > **CSS Toolkit** > **Address Generator**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator). For more information, see [Push/Pull URL](https://intl.cloud.tencent.com/document/product/1071/39359). 
![](https://main.qcloudimg.com/raw/7110d39cdb464b789bd68301f4de7ebe.png)   
- **Why is `V2TXLIVE_ERROR_INVALID_LICENSE` returned?**    
If the `startPush` API returns `V2TXLIVE_ERROR_INVALID_LICENSE`, it means your license verification failed. Please check your configuration against [Step 2. Configure a license for the SDK](#step2).   

[](id:step6)

### 6. Publish audio-only streams    
If your live streaming scenarios involve audio only, you can skip [Step 4](#step4), or call `stopCamera` before `startPush`.

```java     
V2TXLivePusher mLivePusher = new V2TXLivePusherImpl(this, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTMP); // Set the live streaming protocol to RTMP
mLivePusher.startMicrophone();
String rtmpURL = "rtmp://test.com/live/xxxxxx"; // Enter your RTMP URL for stream publishing  
int ret = mLivePusher.startPush(rtmpURL.trim());  
```

>? If you publish audio-only streams but no streams can be pulled from an RTMP, FLV, or HLS playback URL, there is a problem with your line configuration, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for help.  

[](id:step7)
### 7. Set video quality  
Call [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a2695806cb6c74ccce4b378d306ef0a02) in `V2TXLivePusher` to set the quality of videos watched by audience. The encoding parameters set determine the quality of videos presented to audience. The local video seen by the host is the original version that has not been encoded or compressed, and is therefore not affected by the settings. For details, please see [Set Video Quality](https://intl.cloud.tencent.com/zh/document/product/1071).

[](id:step8)

### 8. Set the beauty filter style and skin brightening and rosy skin filters    
![](https://main.qcloudimg.com/raw/21f45fcbf3334cd1abb45df43f476b2f.png)
Call [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) in `V2TXLivePusher` to get a `TXBeautyManager` instance to set beauty filters.

#### Beauty filter style
The SDK has three built-in beauty filter algorithms, each corresponding to a beauty filter style. Choose one that best fits your product positioning. For the definitions of the styles, see `TXLiveConstants.java`.
<table><tr>
<th>Beauty Filter Style</th><th>Description</th>
</tr><tr>
<td>BEAUTY_STYLE_SMOOTH</td>
<td>The smooth style, which features more obvious skin smoothing effects and is suitable for live shows</td>
</tr><tr>
<td>BEAUTY_STYLE_NATURE</td>
<td>The natural style, which retains more facial details and is more natural</td>
</tr><tr>
<td>BEAUTY_STYLE_PITU</td>
<td>The Pitu style, which uses the beauty filter algorithm developed by YouTu Lab. Its effect is between the smooth style and the natural style: it retains more skin details than the smooth style and delivers more obvious skin smoothing effects than the natural style.</td>
</tr></table>

You can call the `setBeautyStyle` API of `TXBeautyManager` to set the beauty filter style.
<table>
<tr><th>Item</th><th width=51%>Configuration</th><th>Description</th></tr>
</tr><tr>
<td>Beauty filter strength</td>
<td>Via the <code>setBeautyLevel</code> API in `TXBeautyManager`</td>
<td>Value range: 0-9. `0` means the filter is disabled. The greater the value, the stronger the filter.</td>
</tr><tr>
<td>Skin brightening filter strength</td>
<td>Via the <code>setWhitenessLevel</code> API in `TXBeautyManager`</td>
<td>Value range: 0-9. `0` means the filter is disabled. The greater the value, the stronger the filter.</td>
</tr><tr>
<td>Rosy skin filter strength</td>
<td>Via the <code>setRuddyLevel</code> API in `TXBeautyManager`</td>
<td>Value range: 0-9. `0` means the filter is disabled. The greater the value, the stronger the filter.</td>
</tr></table>

[](id:step9)
### 9. Set color filters   
![](https://main.qcloudimg.com/raw/0aaf20c77878ef137f2edb693ff79451.png)
- Call [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) in `V2TXLivePusher` to get a [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__android.html) instance to set color filters.
- Call the `setFilter` API in `TXBeautyManager` to set color filters. Color filters are a technology that adjusts the color tone of sections of an image. For example, it may lighten the yellow sections of an image to achieve the effect of skin brightening, or add warm tones to a video to give it a refreshing and soft boost.   
- Call the `setFilterStrength` API in `TXBeautyManager` to set the strength of a color filter. The higher the strength, the more obvious the effect. 

Based on our experience of operating Now Live, it’s not enough to use the `setBeautyStyle` API in `TXBeautyManager` to set the beauty filter style alone. The `setBeautyStyle` API must be used together with `setFilter` in order to produce richer effects. Given this, our designers have developed 17 built-in color filters and integrated them into the [demo](https://github.com/tencentyun/MLVBSDK/tree/master/Android/Demo). 

```java 
// Select a color filter file to use   
Bitmap filterBmp = decodeResource(getResources(), R.drawable.filter_biaozhun);  
mLivePusher.getBeautyManager().setFilter(filterBmp);   
mLivePusher.getBeautyManager().setFilterStrength(0.5f);  
```

[](id:step10)
### 10. Manage devices

`V2TXLivePusher` provides a series of APIs for the control of devices. You can call `getDeviceManager` to get a `TXDeviceManager` instance for device management. For detailed instructions, please see [TXDeviceManager API](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__android.html).
![](https://main.qcloudimg.com/raw/ffebf9941de52db8ee1f9e52c073fe38.png)

[](id:step11)
### 11. Set the mirror effect for audience    

Call [setRenderMirror](http://doc.qcloudtrtc.com/group__V2TXLivePusher__android.html#afd909d85fd0dda0db4078692b319681f) in `V2TXLivePusher` to set the mirror mode of the camera, which affects the way video images are presented to audience. By default, the local image seen by the host is flipped when the front camera is used, which creates the same effect as a mirror does. If you call the API to enable the mirror mode for audience, the image seen by audience will be the same as that seen by the host.
![](https://main.qcloudimg.com/raw/e9841250668a9057d638ee67d0b0afee.png)   

[](id:step12)
### 12. Publish streams in landscape mode    

In most cases, hosts stream while holding their phones vertically, and audience watch videos in portrait resolutions (e.g., 540 x 960). However, hosts also hold phones horizontally sometimes, and ideally, audience should be able to watch videos in landscape resolutions (960 x 540), as shown below: 
![](https://main.qcloudimg.com/raw/b1e58275542aac52fb861745d95246cc.png)    
By default, `V2TXLivePusher` outputs videos in portrait resolutions. You can have it output landscape-mode videos to audience by modifying the parameters of `setVideoQuality`.

```java 
mLivePusher.setVideoQuality(mVideoResolution, isLandscape ? V2TXLiveVideoResolutionModeLandscape : V2TXLiveVideoResolutionModePortrait);   
```

### 13. Set audio effects

Call `getAudioEffectManager` in `V2TXLivePusher` to get a `TXAudioEffectManager` instance, which can be used to mix background music and set in-ear monitoring, reverb, and other audio effects. Background music mixing means mixing into the published stream the music played by the host’s phone so that audience can also hear the music.
![](https://main.qcloudimg.com/raw/95d4dd681affd0ea54cffdb854f6a3ab.png)

- Call the `enableVoiceEarMonitor` API in [TXAudioEffectM1anager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__android.html) to enable in-ear monitoring, which allows hosts to hear their vocals in earphones when they sing.
- Call the `setVoiceReverbType` API in `TXAudioEffectManager` to add reverb effects such as karaoke, hall, husky, and metal. The effects are applied to the videos watched by audience.
- Call the `setVoiceChangerType` API in `TXAudioEffectManager` to add voice changing effects such as little girl and middle-aged man to enrich host-audience interaction. The effects are applied to the videos watched by audience.

![](https://main.qcloudimg.com/raw/a90a110e2950568b9d7cd6bef8e0893b.png)
>? For detailed instructions, please see [TXAudioEffectManager API](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__android.html).

### 14. Set watermarks  

Call [setWatermark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__android.html#a4f56a5a937d87e5b1ae6f77c5bab2335) in `V2TXLivePusher` to add a watermark to videos output by the SDK. The position of the watermark is determined by the `(x, y, scale)` parameter passed in.

- The watermark image must be in PNG rather than JPG format. The former carries opacity information, which allows the SDK to better address the image aliasing issue (changing the extension of a JPG image to PNG won’t work).
- The `(x, y, scale)` parameter specifies the normalized coordinates of the watermark relative to the resolution of the published video. For example, if the resolution of the published video is 540 x 960, and `(x, y, scale)` is set to `（0.1, 0.1, 0.1）`, the actual pixel coordinates of the watermark will be (540 x 0.1, 960 x 0.1). The width of the watermark will be the image width x 0.1, and the height will be scaled automatically.

```java 
// Set a video watermark
mLivePusher.setWatermark(BitmapFactory.decodeResource(getResources(),R.drawable.watermark), 0.03f, 0.015f, 1f);
```

### 15. Inform hosts of poor network conditions 
Hosts should be informed when their network conditions are bad and be prompted to check their network.    
You can capture the **V2TXLIVE_WARNING_NETWORK_BUSY** event using [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__android.html#abd54414cbd5d52c096f9cc090cfe1fec) in `V2TXLivePusherObserver`. The event indicates poor network conditions for hosts, which result in stuttering for audience. When the event occurs, you can send a UI message about poor network conditions to hosts.
<dx-codeblock>
:::java java 
@Override
public void onWarning(int code, String msg, Bundle extraInfo) {
    if (code == V2TXLiveCode.V2TXLIVE_WARNING_NETWORK_BUSY) {
        showNetBusyTips(); // Show a “network busy” message
    }
} 
:::
</dx-codeblock>

## Event Handling

### Listening for events
The SDK listens for publishing events and errors via the [V2TXLivePusherObserver](http://doc.qcloudtrtc.com/group__V2TXLivePusherObserver__android.html) delegate. See [V2TXLiveCode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLiveCode__android.html) for a detailed list of events and error codes.

### Error events
The SDK detected some serious issues, which make it impossible for stream publishing to continue.

| Event ID | Code | Description |
| :------------------------------------ | :---- | :------------------------------- |
|V2TXLIVE_ERROR_FAILED                  | -1 | A common error not yet classified |
|V2TXLIVE_ERROR_INVALID_PARAMETER       | -2 | An invalid parameter was passed in during API calling. |
|V2TXLIVE_ERROR_REFUSED                 | -3 | The API call was rejected.  |
|V2TXLIVE_ERROR_NOT_SUPPORTED           | -4 | The API cannot be called.  |
|V2TXLIVE_ERROR_INVALID_LICENSE         | -5 | Failed to call the API due to invalid license.  |
|V2TXLIVE_ERROR_REQUEST_TIMEOUT         | -6 | The server request timed out.  |
|V2TXLIVE_ERROR_SERVER_PROCESS_FAILED   | -7 | The server could not handle your request.  |

### Warning events
The SDK detected some warning events. Warning events trigger tentative protection or recovery logic and can often be resolved.

| Event ID                                       | Code  | Description                                                     |
| :-------------------------------------------- | :---- | :----------------------------------------------------------- |
|V2TXLIVE_WARNING_NETWORK_BUSY                  |  1101|  Bad network connection: data upload blocked due to limited upstream bandwidth. |
|V2TXLIVE_WARNING_VIDEO_BLOCK                   |  2105|  Latency during video playback.  |
|V2TXLIVE_WARNING_CAMERA_START_FAILED           | -1301|  Failed to turn the camera on.  |
|V2TXLIVE_WARNING_CAMERA_OCCUPIED               | -1316| The camera is occupied. Try using another camera. |
|V2TXLIVE_WARNING_CAMERA_NO_PERMISSION          | -1314| No permission to access the camera. This usually occurs on mobile devices and may be because the user denied the permission. |
|V2TXLIVE_WARNING_MICROPHONE_START_FAILED       | -1302| Failed to turn the mic on. |
|V2TXLIVE_WARNING_MICROPHONE_OCCUPIED           | -1319| The mic is occupied. This occurs when, for example, the user is having a call on the mobile device. |
|V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION      | -1317| No permission to access the mic. This usually occurs on mobile devices and may be because the user denied the permission. |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED  | -1309|  The system does not support screen sharing.  |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED   | -1308|  Failed to start screen recording. If this occurs on a mobile device, it may be because the user denied the permission.  |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED    | -7001|  Screen recording was stopped by the system.  |
