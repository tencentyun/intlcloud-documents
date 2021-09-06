## Overview
Camera publishing refers to the process of collecting video and audio data from the mobile phone’s camera and mic, encoding the data, and publishing it to cloud-based live streaming platforms. Tencent Cloud’s LiteAVSDK provides the camera publishing capability via `V2TXLivePusher`. The figure below shows the UI for camera publishing operations in the simplified demo of LiteAVSDK.
![](https://main.qcloudimg.com/raw/39ee7f9e0e092d0adb9f1dff1077a482.png)

## Notes
**About running projects on x86 emulators:** the SDK uses a lot of audio and video APIs of the iOS system, most of which cannot be used on the x86 emulator built into macOS. Therefore, we recommend that you test your project on a real device.

## Sample Code
| Platform |                         GitHub Address                          |           Key Class            |
| :------: | :----------------------------------------------------------: | :-------------------------: |
|   iOS    | [GitHub](https://github.com/tencentyun/LiteAVProfessional_iOS/blob/master/Demo/TXLiteAVDemo/LivePusherDemo/CameraPushDemo/CameraPushViewController.m) | CameraPushViewController.m  |
| Android  | [GitHub](https://github.com/tencentyun/LiteAVProfessional_Android/blob/master/Demo/livepusherdemo/src/main/java/com/tencent/liteav/demo/livepusher/camerapush/ui/CameraPushMainActivity.java) | CameraPushMainActivity.java |

## Feature Integration
[](id:step1)
### 1. Download the SDK
[Download](https://intl.cloud.tencent.com/document/product/1071/38150) the SDK and follow the instructions in [SDK Integration](https://intl.cloud.tencent.com/document/product/1071/38155) to integrate the SDK into your application.

[](id:step2)
### 2. Configure a license for the SDK
Click [Get License](https://console.cloud.tencent.com/live/license) to obtain a trial license. You will get two strings: a license URL and a decryption key.
Before you use LiteAVSDK features in your application, complete the following configurations (preferably in `- [AppDelegate application:didFinishLaunchingWithOptions:]`):

```objc
@import TXLiteAVSDK_Professional;
@implementation AppDelegate
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    NSString * const licenceURL = @"<The license URL obtained>";
    NSString * const licenceKey = @"<The key obtained>";
        
    //TXLiveBase can be found in the "TXLiveBase.h" header file
    [TXLiveBase setLicenceURL:licenceURL key:licenceKey]; 
    NSLog(@"SDK Version = %@", [TXLiveBase getSDKVersionStr]);
}
@end
```

[](id:step3)
### 3. Initialize the `V2TXLivePusher` component
Create a `V2TXLivePusher` object and specify `V2TXLiveMode`.

```objectivec   
 V2TXLivePusher *pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTMP]; // Set the live streaming protocol to RTMP 
```

[](id:step4)
### 4. Enable camera preview
Call `setRenderView` in [V2TXLivePusher](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html) to configure a view object for displaying video images, and then call `startCamera` to enable camera preview for your mobile phone.

<dx-codeblock>
::: objectivec objectivec
 // Create a view object and insert it into the UI
 UIView *_localView = [[UIView alloc] initWithFrame:self.view.bounds];
 [self.view insertSubview:_localView atIndex:0];
 _localView.center = self.view.center;

 // Enable preview for the local camera
 [_pusher setRenderView:_localView];
 [_pusher startCamera:YES];
:::
</dx-codeblock>

> ! To add animated effects to the view, modify its `transform` attribute rather than `frame` attribute.
>```objectivec
  [UIView animateWithDuration:0.5 animations:^{
            _localView.transform = CGAffineTransformMakeScale(0.3, 0.3); // Shrink by 1/3
        }];
     ```
```

[](id:step5)
### 5. Start and stop publishing streams
After calling `startCamera` to enable camera preview, you can call the [startPush](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a33b38f236a439e7d848606acb68cc087) API in `V2TXLivePusher` to start stream publishing.
​```objectivec 
// Start publishing streams
NSString* rtmpUrl = @"rtmp://test.com/live/xxxxxx"; // Enter your RTMP URL for stream publishing
[_pusher startPush:rtmpUrl];
```

Call [stopPush](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a7332411d6264bc743b0b2bae0b8a73ae) in `V2TXLivePusher` to stop publishing streams.
```objectivec
// Stop publishing streams
[_pusher stopPush];
```
>! If you have enabled camera preview, please disable it when you stop publishing streams.  

-  **How can I obtain a valid publishing URL?**
To generate a publishing URL, activate CSS, and go to the **CSS console** > **CSS Toolkit** > [**Address Generator**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator). For more information, see [Push/Pull URL](https://intl.cloud.tencent.com/document/product/1071/39359).
![](https://main.qcloudimg.com/raw/0ec9d83f340454c287d96f83eec3a3e4.png)
- **Why is `V2TXLIVE_ERROR_INVALID_LICENSE` returned?**    
If the `startPush` API returns `V2TXLIVE_ERROR_INVALID_LICENSE`, it means your license verification failed. Please check your configuration against [Step 2. Configure a license for the SDK](#step2).

[](id:step6)
### 6. Publish audio-only streams
If your live streaming scenarios involve audio only, you can skip [Step 4](#step4), or call `stopCamera` before `startPush`.
```objectivec
V2TXLivePusher *_pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTMP]; 
NSString* rtmpUrl = @"rtmp://test.com/live/xxxxxx";    
[_pusher startMicrophone];
[_pusher startPush:rtmpUrl];
```
>? If you publish audio-only streams but no streams can be pulled from an RTMP, FLV, or HLS playback URL, there is a problem with your line configuration, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for help.

[](id:step7)
### 7. Set video quality
Call [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a0b08436c1e14a8d7d9875fae59ac6d84) in `V2TXLivePusher` to set the quality of videos watched by audience. The encoding parameters set determine the quality of videos presented to audience. The local video seen by the host is the original version that has not been encoded or compressed, and is therefore not affected by the settings. For details, please see [Set Video Quality](https://intl.cloud.tencent.com/zh/document/product/1071).

[](id:step8)
### 8. Set the beauty filter style and skin brightening and rosy skin filters
Call [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a4fb05ae6b5face276ace62558731280a) in `V2TXLivePusher` to get a `TXBeautyManager` instance to set beauty filters.

#### Beauty filter style
The SDK has three built-in beauty filter algorithms, each corresponding to a beauty filter style. Choose one that best fits your product positioning. For details, please see the [TXBeautyManager.h](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#gafbbe0e87ec0168eacfc10e57c43abad8) file.

| Beauty Filter Style | Description |
|---------|---------|
| TXBeautyStyleSmooth | The smooth style, which features more obvious skin smoothing effects and is suitable for live shows
| TXBeautyStyleNature | The natural style, which retains more facial details and is more natural
| TXBeautyStylePitu | The Pitu style, which uses the beauty filter algorithm developed by YouTu Lab. Its effect is between the smooth style and the natural style: it retains more skin details than the smooth style and delivers more obvious skin smoothing effects than the natural style.

You can call the [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#a8f2378a87c2e79fa3b978078e534ef4a) API in `TXBeautyManager` to set the beauty filter style.

<table>
<tr><th>Item</th><th width=51%>Configuration</th><th>Description</th></tr>
<tr>
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
![](https://main.qcloudimg.com/raw/55b969c713b9d96f496bcab3d72e3850.png)
- Call [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a4fb05ae6b5face276ace62558731280a) in `V2TXLivePusher` to get a `TXBeautyManager` instance to set color filters.
- Call the `setFilter` API in `TXBeautyManager` to set color filters. Color filters are a technology that adjusts the color tone of sections of an image. For example, it may lighten the yellow sections of an image to achieve the effect of skin brightening, or add warm tones to a video to give it a refreshing and soft boost.   
- Call the `setFilterStrength` API in `TXBeautyManager` to set the strength of a color filter. The higher the strength, the more obvious the effect. 

Based on our experience of operating Now Live, it's not enough to use the `setBeautyStyle` API in `TXBeautyManager` to set the beauty filter style alone. The `setBeautyStyle` API must be used together with `setFilter` in order to produce richer effects. Given this, we have provided 17 built-in color filters for you to use.
```objectivec
NSString * path = [[NSBundle mainBundle] pathForResource:@"FilterResource" ofType:@"bundle"];
path = [path stringByAppendingPathComponent:lookupFileName];

UIImage *image = [UIImage imageWithContentsOfFile:path];
[[_pusher getBeautyManager] setFilter:image];
[[_pusher getBeautyManager] setFilterStrength:0.5f];
```

[](id:step10)
### 10. Manage devices
`V2TXLivePusher` provides a series of APIs for the control of devices. You can call `getDeviceManager` to get a `TXDeviceManager` instance for device management. For detailed instructions, please see [TXDeviceManager API](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__ios.html#interfaceTXDeviceManager).
![](https://main.qcloudimg.com/raw/f071f9c5edf88e61b108a77946669d60.png)

[](id:step11)
### 11. Set the mirror effect for audience
Call [setRenderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#adf4cd57c705a1022d6730fd722f8dab5) in `V2TXLivePusher` to set the mirror mode of the camera, which affects the way video images are presented to audience. By default, the local image seen by the host is flipped when the front camera is used, which creates the same effect as a mirror does. If you call the API to enable the mirror mode for audience, the image seen by audience will be the same as that seen by the host.
![](https://main.qcloudimg.com/raw/48cb3e6a39e968f3707fc956c062632a.png)

[](id:step12)
### 12. Publish streams in landscape mode
In most cases, hosts stream while holding their phones vertically, and audience watch videos in portrait resolutions (e.g., 540 x 960). However, hosts also hold phones horizontally sometimes, and ideally, audience should be able to watch videos in landscape resolutions (960 x 540), as shown below: 
![](https://main.qcloudimg.com/raw/d42f32ad9deef5b3eba3ccb271fe05e8.png)

By default, `V2TXLivePusher` outputs videos in portrait resolutions. You can have it output landscape-mode videos to audience by modifying the parameters of [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a0b08436c1e14a8d7d9875fae59ac6d84).
```objectivec
[_pusher setVideoQuality:videoQuality
             resolutionMode:isLandscape ? V2TXLiveVideoResolutionModeLandscape : V2TXLiveVideoResolutionModePortrait];
```

[](id:step13)
### 13. Set audio effects
Call [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__ios.html) in `V2TXLivePusher` to get a `TXAudioEffectManager` instance, which can be used to mix background music and set in-ear monitoring, reverb, and other audio effects. Background music mixing means mixing into the published stream the music played by the host’s phone so that audience can also hear the music.
![](https://main.qcloudimg.com/raw/eeff5f60fa29d204e501ef2029b922ea.png)

- Call the `enableVoiceEarMonitor` API in `TXAudioEffectManager` to enable in-ear monitoring, which allows hosts to hear their vocals in earphones when they sing.
- Call the `setVoiceReverbType` API in `TXAudioEffectManager` to add reverb effects such as karaoke, hall, husky, and metal. The effects are applied to the videos watched by audience.
- Call the `setVoiceChangerType` API in `TXAudioEffectManager` to add voice changing effects such as little girl and middle-aged man to enrich host-audience interaction. The effects are applied to the videos watched by audience.
![](https://main.qcloudimg.com/raw/a90a110e2950568b9d7cd6bef8e0893b.png)

>? For detailed instructions, please see [TXAudioEffectManager API](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__ios.html).

[](id:step14)
### 14. Set watermarks

Call [setWatermark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#ad48aacbfad38b8f5389c159283fae859) in `V2TXLivePusher` to add a watermark to videos output by the SDK. The position of the watermark is determined by the `(x, y, scale)` parameter passed in.

- The watermark image must be in PNG rather than JPG format. The former carries opacity information, which allows the SDK to better address the image aliasing issue (changing the extension of a JPG image to PNG won’t work).
- The `(x, y, scale)` parameter specifies the normalized coordinates of the watermark relative to the resolution of the published video. For example, if the resolution of the published video is 540 x 960, and `(x, y, scale)` is set to `（0.1, 0.1, 0.1）`, the actual pixel coordinates of the watermark will be (540 x 0.1, 960 x 0.1). The width of the watermark will be the image width x 0.1, and the height will be scaled automatically.

```objectivec
// Set a video watermark
[_pusher setWatermark:[UIImage imageNamed:@"watermark"] x:0.03 y:0.015 scale:1];
```

[](id:step15)
### 15. Inform hosts of poor network conditions
Connecting phones to Wi-Fi does not necessarily guarantee network conditions. In case of poor Wi-Fi signal or limited bandwidth, the network speed of a Wi-Fi connected phone may be slower than that of a phone using 4G. Hosts should be informed when their network conditions are bad and be prompted to switch to a different network.    
![](https://main.qcloudimg.com/raw/66441cb1356f87caeffb4a3102b938ea.png)  

You can capture the **V2TXLIVE_WARNING_NETWORK_BUSY** event using [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLiveCode__ios.html#ga5506c2171438841ab3e99c80786c7ba0) in `V2TXLivePusherObserver`. The event indicates poor network conditions for hosts, which result in stuttering for audience. When the event occurs, you can send a UI message about poor network conditions to hosts, as shown above.


<dx-codeblock>
::: objectiveC objectiveC
- (void)onWarning:(V2TXLiveCode)code
          message:(NSString *)msg
        extraInfo:(NSDictionary *)extraInfo {
    dispatch_async(dispatch_get_main_queue(), ^{
        if (code == V2TXLIVE_WARNING_NETWORK_BUSY) {
            [_notification displayNotificationWithMessage:
                @"Your network conditions are poor. Please switch to a different network." forDuration:5];
        }
    });
}
:::
</dx-codeblock>


## Event Handling
### Listening for events
The SDK listens for publishing events and errors via the [V2TXLivePusherObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__ios.html) delegate. See [V2TXLiveCode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLiveCode__ios.html) for a detailed list of events and error codes.

### Error events 
The SDK detected some serious issues, which make it impossible for stream publishing to continue.

| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
|V2TXLIVE_ERROR_FAILED                  | -1 | A common error not yet classified |
|V2TXLIVE_ERROR_INVALID_PARAMETER       | -2 | An invalid parameter was passed in during API calling. |
|V2TXLIVE_ERROR_REFUSED                 | -3 | The API call was rejected.  |
|V2TXLIVE_ERROR_NOT_SUPPORTED           | -4 | The API cannot be called.  |
|V2TXLIVE_ERROR_INVALID_LICENSE         | -5 | Failed to call the API due to invalid license.  |
|V2TXLIVE_ERROR_REQUEST_TIMEOUT         | -6 | The server request timed out.  |
|V2TXLIVE_ERROR_SERVER_PROCESS_FAILED   | -7 | The server could not handle your request.  |

### Warning events 
The SDK detected some warning events. Warning events trigger tentative protection or recovery logic and can often be resolved.

| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
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
