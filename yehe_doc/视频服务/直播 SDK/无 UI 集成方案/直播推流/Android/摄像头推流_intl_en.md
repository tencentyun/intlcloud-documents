## Overview

Publishing from camera refers to the process of collecting video and audio data from the mobile phone’s camera and mic, encoding the data, and publishing it to cloud-based live streaming platforms. Tencent Cloud’s LiteAVSDK provides the camera publishing capability via `V2TXLivePusher`.The following is the relevant GUI that demonstrating camera push stream in the SDK API-Example project:
![](https://qcloudimg.tencent-cloud.cn/raw/0357b68e338a45ebcccca25918250169.png)

## Notes
**Testing on real devices:** The SDK uses a lot of audio and video APIs of the Android system, most of which cannot be used on emulators. Therefore, we recommend that you test your project on a real device.

## Sample Code
| Platform |                         GitHub Address                          |           Key Class            |
| :------: | :----------------------------------------------------------: | :-------------------------: |
| iOS | [Github](https://github.com/LiteAVSDK/Live_iOS/blob/main/MLVB-API-Example-OC/Basic/LivePushCamera/LivePushCameraViewController.m) | LivePushCameraViewController.m |
| Android | [Github](https://github.com/LiteAVSDK/Live_Android/blob/main/MLVB-API-Example/Basic/LivePushCamera/src/main/java/com/tencent/mlvb/livepushcamera/LivePushCameraActivity.java) | LivePushCameraActivity.java |
| Flutter | [Github](https://github.com/LiteAVSDK/Live_Flutter/blob/main/Live-API-Example/lib/page/push/live_camera_push.dart) | live_camera_push.dart |

## Integration

[](id:step1)

### 1. Download the SDK

[Download](https://www.tencentcloud.com/document/product/1071/38150) the SDK and follow the instructions in [SDK Integration](https://www.tencentcloud.com/document/product/1071/38156) to integrate the SDK into your application.

[](id:step2)
### 2. Configure License Authorization for SDK
1. Obtain license authorization：
    - If you have obtained the relevant license authorization, need to Get License URL and License Key in [Cloud Live Console](https://console.tencentcloud.com/live/license)
    ![](https://qcloudimg.tencent-cloud.cn/raw/a6b24e8677c514ee1721d38893fd9ca2.png)
    - If you have not yet obtained the license authorization, please reference [Adding and Renewing Licenses](https://www.tencentcloud.com/document/product/1071/38546) to make an application.
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

[](id:step3)
### 3. Initialize the `V2TXLivePusher` component

Create a `V2TXLivePusher` object, which will be responsible for publishing operations.

```java   
// Specify the corresponding live broadcast protocol as RTMP, which does not support mic connection
V2TXLivePusher mLivePusher = new V2TXLivePusherImpl(this, V2TXLiveDef.V2TXLiveMode.TXLiveMode_RTMP);
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
mLivePusher.startMicrophone();
```

[](id:step5)
### 5. Start and stop publishing
1. After calling `startCamera` to enable camera preview, you can call the [startPush](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusher__android.html#ab4f8adaa0616d54d6ed920e49377a08a) API in `V2TXLivePusher` to start publishing. >? if you choose `RTMP` protocol to push in [Step3](#step3)，the generate of the push URL, please refer to [RTMP URL](https://www.tencentcloud.com/document/product/1071/39359)。
```java
//This URL does not support co-anchoring. The stream is published to a live streaming CDN.
String url = "rtmp://test.com/live/streamid?txSecret=xxxxx&txTime=xxxxxxxx";
int ret = mLivePusher.startPush(url);
if (ret == V2TXLIVE_ERROR_INVALID_LICENSE) {
    Log.i(TAG, "startRTMPPush: license verification failed");
}     
```
> - **Reason for returning V2TXLIVE_ERROR_INVALID_LICENSE?** 
> If the `startPush` interface returns `V2TXLIVE_ERROR_INVALID_LICENSE`, it means that your license verification failed, please check the url and key set in [Step 2: Configure the SDK for license authorization](#step2).

2. Call [stopPush](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusher__android.html#af07c1dcff91b43a2309665b8663ed530) in `V2TXLivePusher` to stop publishing streams
```java
//Stop publishing
mLivePusher.stopPush();
```


[](id:step6)
### 6. Publish audio-only streams    
If your live streaming scenarios involve audio only, you can skip [Step 4](#step4) or call `stopCamera` before `startPush`.

```java     
mLivePusher.startMicrophone();
// The push stream can be started by passing in the corresponding URL according to the push stream protocol. The RTMP protocol starts with rtmp://, and this protocol does not support the connection of microphones.
String url = "rtmp://test.com/live/streamid?txSecret=xxxxx&txTime=xxxxxxxx";
int ret = mLivePusher.startPush(url);
```

>? If you publish audio-only streams but no streams can be pulled from an RTMP, FLV, or HLS playback URL, there is a problem with your line configuration, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for help.  

[](id:step7)
### 7. Set video quality  
Call [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusher__android.html#a2695806cb6c74ccce4b378d306ef0a02) in `V2TXLivePusher` to set the quality of videos watched by audience. The encoding parameters set determine the quality of videos presented to audience. The local video watched by the host is the original HD version that has not been encoded or compressed, and is therefore not affected by the settings. For details, please see [Setting Video Quality](https://www.tencentcloud.com/document/product/1071/41861).

[](id:step8)
### 8. Set the beauty filter style and skin brightening and rosy skin effects    

Call [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusher__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) in `V2TXLivePusher` to get a `TXBeautyManager` instance to set beauty filters.

#### Beauty filter style
The SDK has three built-in beauty filter algorithms, each corresponding to a beauty filter style. Choose one that best fits your product positioning. For the definitions, see `TXLiveConstants.java`.
<table><tr>
<th>Beauty Filter Style</th><th>Description</th>
</tr><tr>
<td>BEAUTY_STYLE_SMOOTH</td>
<td>The smooth style, which features more obvious skin smoothing effects and is suitable for live showrooms</td>
</tr><tr>
<td>BEAUTY_STYLE_NATURE</td>
<td>The natural style, which retains more facial details and is more natural</td>
</tr><tr>
<td>BEAUTY_STYLE_PITU</td>
<td>The Pitu style, which uses the beauty filter algorithm developed by YouTu Lab. Its effect is between the smooth style and the natural style, that is, it retains more skin details than the smooth style and delivers more obvious skin smoothing effects than the natural style.</td>
</tr></table>

You can call the `setBeautyStyle` API of `TXBeautyManager` to set the beauty filter style.
<table>
<tr><th>Item</th><th width=51%>Configuration</th><th>Description</th></tr>
</tr><tr>
<td>Beauty filter strength</td>
<td>Via the <code>setBeautyLevel</code> API in `TXBeautyManager`</td>
<td>Value range: 0-9. `0` means the filter is disabled. The greater the value, the more obvious the effect.</td>
</tr><tr>
<td>Skin brightening filter strength</td>
<td>Via the <code>setWhitenessLevel</code> API in `TXBeautyManager`</td>
<td>Value range: 0-9. `0` means the filter is disabled. The greater the value, the more obvious the effect.</td>
</tr><tr>
<td>Rosy skin filter strength</td>
<td>Via the <code>setRuddyLevel</code> API in `TXBeautyManager`</td>
<td>Value range: 0-9. `0` means the filter is disabled. The greater the value, the more obvious the effect.</td>
</tr></table>

[](id:step9)
### 9. Set color filters   

- Call [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusher__android.html#a3fdfeb3204581c27bbf1c8b5598714fb) in `V2TXLivePusher` to get a [TXBeautyManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXBeautyManager__android.html) instance to set color filters.
- Call the `setFilter` API in `TXBeautyManager` to set color filters. Color filters are a technology that adjusts the color tone of sections of an image. For example, it may lighten the yellow sections of an image to achieve the effect of skin brightening, or add warm tones to a video to give it a refreshing and soft boost.   
- Call the `setFilterStrength` API in `TXBeautyManager` to set the strength of a color filter. The higher the strength, the more obvious the effect. 

Based on our experience of operating Mobile QQ and Now Live, it’s not enough to use only the `setBeautyStyle` API in `TXBeautyManager` to set the beauty filter style. The `setBeautyStyle` API must be used together with `setFilter` to produce richer effects. Given this, our designers have developed 17 built-in color filters for you to choose from. 

```java 
// Select the desired color filter file. The filter file can be obtained from the resource file of the Mini Live App (a .png file starting with tuibeauty_filter_).
Bitmap filterBmp = decodeResource(getResources(), R.drawable.tuibeauty_filter_biaozhun);
mLivePusher.getBeautyManager().setFilter(filterBmp);
mLivePusher.getBeautyManager().setFilterStrength(0.5f);
```

[](id:step10)
### 10. Manage devices

`V2TXLivePusher` provides a series of APIs for the control of devices. You can call `getDeviceManager` to get a `TXDeviceManager` instance for device management. For detailed instructions, please see [TXDeviceManager API](https://liteav.sdk.qcloud.com/doc/api/en/group__TXDeviceManager__android.html).


[](id:step11)
### 11. Set the video mirroring effect for audience    

Call [setEncoderMirror](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusher__android.html#ae025945b6f2633d8e3b879a6fe24dd99) in `V2TXLivePusher` to set the camera mirror mode, which affects the way video images are presented to audience. By default, the local video watched by the host is flipped when the front camera is used, which creates the same effect as a mirror does. The video watched by audience is the same as that watched by the host, as shown below.
![](https://main.qcloudimg.com/raw/520d16280962523809e5695d2483d9ef.png)   

[](id:step12)
### 12. Publish streams in landscape mode    

In most cases, hosts stream while holding their phones vertically, and audience watch videos in portrait resolutions (e.g., 540 × 960). However, there are also cases where hosts hold phones horizontally, and ideally, audience should watch videos in landscape resolutions (960 × 540).
    
By default, `V2TXLivePusher` outputs videos in portrait resolutions. You can publish landscape-mode videos to audience by modifying a parameter of the `setVideoQuality` API.

```java
V2TXLiveDef.V2TXLiveVideoEncoderParam param = new V2TXLiveDef.V2TXLiveVideoEncoderParam(V2TXLiveDef.V2TXLiveVideoResolution.V2TXLiveVideoResolution960x540);
param.videoResolutionMode = isLandscape ? V2TXLiveVideoResolutionModeLandscape : V2TXLiveVideoResolutionModePortrait;
mLivePusher.setVideoQuality(param);
```

[](id:step13)
### 13. Set audio effects

Call `getAudioEffectManager` in `V2TXLivePusher` to get a `TXAudioEffectManager` instance, which can be used to mix background music and set in-ear monitoring, reverb, and other audio effects. Background music mixing means mixing into the published stream the music played by the host’s phone so that audience can also hear the music.

- Call the `enableVoiceEarMonitor` API in [TXAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/en/group__TXAudioEffectManager__android.html) to enable in-ear monitoring, which allows hosts to hear their vocals in earphones when they sing.
- Call the `setVoiceReverbType` API in `TXAudioEffectManager` to add reverb effects such as karaoke, hall, husky, and metal. The effects are applied to the videos watched by audience.
- Call the `setVoiceChangerType` API in `TXAudioEffectManager` to add voice changing effects such as little girl and middle-aged man to enrich host-audience interaction. The effects are applied to the videos watched by audience.

![](https://main.qcloudimg.com/raw/f8282bd6e1ba20e1e902bad52fa3131f.png)
>? For detailed instructions, please see [TXAudioEffectManager API](https://liteav.sdk.qcloud.com/doc/api/en/group__TXDeviceManager__android.html).

[](id:step14)
### 14. Set watermarks  

Call [setWatermark](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusher__android.html#a4f56a5a937d87e5b1ae6f77c5bab2335) in `V2TXLivePusher` to add a watermark to videos output by the SDK. The position of the watermark is determined by the `(x, y, scale)` parameter passed in.

- The watermark image must be in PNG rather than JPG format. The former carries opacity information, which allows the SDK to better address the image aliasing issue (changing the extension of a JPG image to PNG won’t work).
- The `(x, y, scale)` parameter specifies the normalized coordinates of the watermark relative to the resolution of the published video. For example, if the resolution of the published video is 540 x 960, and `(x, y, scale)` is set to `（0.1, 0.1, 0.1）`, the actual pixel coordinates of the watermark will be (540 x 0.1, 960 x 0.1). The width of the watermark image will be the video width x 0.1, and the height will be scaled automatically.

```java 
// Set a video watermark
mLivePusher.setWatermark(BitmapFactory.decodeResource(getResources(),R.drawable.watermark), 0.03f, 0.015f, 1f);
```

[](id:step15)
### 15. Inform hosts of poor network conditions 
Hosts should be informed when their network conditions are bad and be prompted to check their network.    

![](https://main.qcloudimg.com/raw/faaef46a80988270d3ddc96ec4e578b9.png)

You can capture the **V2TXLIVE_WARNING_NETWORK_BUSY** event using [onWarning](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusherObserver__android.html#abd54414cbd5d52c096f9cc090cfe1fec) in `V2TXLivePusherObserver`. The event indicates poor network conditions for hosts, which result in stuttering for audience. When this event occurs, you can send a UI message about poor network conditions to hosts.

```java
@Override
public void onWarning(int code, String msg, Bundle extraInfo) {
    if (code == V2TXLiveCode.V2TXLIVE_WARNING_NETWORK_BUSY) {
        showNetBusyTips(); // Show network tips
    }
}
```

[](id:step16)
### 16. Send SEI messages 
Call the [sendSeiMessage](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusher__android.html#a5ba3762815f11bf5005f151e06ae0b38) API in `V2TXLivePusher` to send SEI messages. SEI refers to the supplementary enhancement information of encoded video. It is not used most of the time, but you can insert custom information into SEI messages. The information will be forwarded to audience by live streaming CDNs. The applications for SEI messages include:
- Live quiz: The publisher can use SEI messages to send questions to the audience. SEI can ensure synchronization among audio, video, and the questions.
- Live showroom: The publisher can use SEI messages to display lyrics to the audience in real time. The effects are not affected by reduction in video encoding quality.
- Online education: The publisher can use SEI messages to display pointers and sketches on slides to the audience in real time.

Custom data is inserted directly into video data and therefore cannot be too large in size (preferably several bytes). It’s common to insert information such as custom timestamps.
```java
//Sample code for Android
int payloadType = 5;
String msg = "test";
mTXLivePusher.sendSeiMessage(payloadType, msg.getBytes("UTF-8"));
```
Common open-source players or web players are incapable of parsing SEI messages. You must use `V2TXLivePlayer`, the built-in player of LiteAVSDK.
1. Configuration:
```java
int payloadType = 5;
mTXLivePlayer.enableReceiveSeiMessage(true, payloadType)
```
2. If the video streams played by `V2TXLivePlayer` contain SEI messages, you will receive the messages via the `onReceiveSeiMessage` callback in `V2TXLivePlayerObserver`.

## Event Handling

### Listening for events
The SDK listens for publishing events and errors via the [V2TXLivePusherObserver](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLivePusherObserver__android.html) delegate. See [V2TXLiveCode](https://liteav.sdk.qcloud.com/doc/api/en/group__V2TXLiveCode__android.html) for a detailed list of events and error codes.

### Errors
An error indicates that the SDK encountered a serious problem that made it impossible for stream publishing to continue.

| Event ID | Code | Description |
| :------------------------------------ | :---- | :------------------------------- |
|V2TXLIVE_ERROR_FAILED                  | -1 | A common error not yet classified |
|V2TXLIVE_ERROR_INVALID_PARAMETER       | -2 | An invalid parameter was passed in during API calling. |
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
