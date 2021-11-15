## Overview
Publishing from camera refers to the process of collecting video and audio data from the mobile phone’s camera and mic, encoding the data, and publishing it to cloud-based live streaming platforms. Tencent Cloud’s LiteAVSDK provides the camera publishing capability via `V2TXLivePusher`.


## Notes
**About running projects on x86 emulators:** The SDK uses a lot of audio and video APIs of the iOS system, most of which cannot be used on the x86 emulator built into macOS. Therefore, we recommend that you test your project on a real device.

## Sample Code
| Platform |                         GitHub Address                          |           Key Class            |
| :------: | :----------------------------------------------------------: | :-------------------------: |
|   iOS    | [GitHub](https://github.com/tencentyun/LiteAVProfessional_iOS/blob/master/Demo/TXLiteAVDemo/LivePusherDemo/CameraPushDemo/CameraPushViewController.m) | CameraPushViewController.m  |
| Android  | [GitHub](https://github.com/tencentyun/LiteAVProfessional_Android/blob/master/Demo/livepusherdemo/src/main/java/com/tencent/liteav/demo/livepusher/camerapush/ui/CameraPushMainActivity.java) | CameraPushMainActivity.java |
>?In addition to the above sample code, regarding frequently asked questions among developers, Tencent Cloud offers a straightforward API example project, which you can use to quickly learn how to use different APIs.
>- iOS: [MLVB-API-Example](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC)
>- Android: [MLVB-API-Example](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example)

## Integration
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

>! To add animated effects to the view, modify its `transform` attribute rather than `frame` attribute.
>```objectivec
  [UIView animateWithDuration:0.5 animations:^{
            _localView.transform = CGAffineTransformMakeScale(0.3, 0.3); // Shrink by 1/3
        }];
     ```


[](id:step5)
### 5. Start and stop publishing
After calling `startCamera` to enable camera preview, you can call the [startPush](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a33b38f236a439e7d848606acb68cc087) API in `V2TXLivePusher` to start publishing. You can use [TRTC’s URL](https://intl.cloud.tencent.com/document/product/1071/39359) or an [RTMP URL](https://intl.cloud.tencent.com/document/product/1071/39359) for publishing. The former uses UDP. It offers better streaming quality and supports co-anchoring.
```objectivec 
// Start publishing. You can use the `trtc://` or `rtmp://` protocol. The former supports co-anchoring.
NSString* url = @"trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=A&usersig=xxxxx";  //This URL supports co-anchoring.
NSString* url = @"rtmp://test.com/live/streamid?txSecret=xxxxx&txTime=xxxxxxxx";    //This URL does not support co-anchoring. The stream is published to a live streaming CDN.
[_pusher startPush:url];
```

Call [stopPush](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a7332411d6264bc743b0b2bae0b8a73ae) in `V2TXLivePusher` to stop publishing streams.
```objectivec
//Stop publishing
[_pusher stopPush];
```

>! If you have enabled camera preview, please disable it when you stop publishing streams. 

-  **How can I obtain a valid publishing URL?**
Activate CSS and, in the CSS console, go to [**CSS Toolkit** > **Address Generator**](https://console.cloud.tencent.com/live/addrgenerator/addrgenerator) to generate a publishing URL. For more information, see [Publishing/Playback URL](https://intl.cloud.tencent.com/document/product/1071/39359).

- **Why is `V2TXLIVE_ERROR_INVALID_LICENSE` returned?**    
If the `startPush` API returns `V2TXLIVE_ERROR_INVALID_LICENSE`, it means your license verification failed. Please check your configuration against [Step 2. Configure a license for the SDK](#step2).

[](id:step6)
### 6. Publish audio-only streams
If your live streaming scenarios involve audio only, you can skip [Step 4](#step4) or do not call `startCamera` before `startPush`.
```objectivec
V2TXLivePusher *_pusher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTMP]; 
// Start publishing. You can use the `trtc://` or `rtmp://` protocol. The former supports co-anchoring.
NSString* url = @"trtc://cloud.tencent.com/push/streamid?sdkappid=1400188888&userId=A&usersig=xxxxx";  //This URL supports co-anchoring.
NSString* url = @"rtmp://test.com/live/streamid?txSecret=xxxxx&txTime=xxxxxxxx";    //This URL does not support co-anchoring. The stream is published to a live streaming CDN.
[_pusher startPush:url];
[_pusher startMicrophone];
```
>? If you publish audio-only streams but no streams can be pulled from an RTMP, FLV, or HLS playback URL, there is a problem with your line configuration, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for help.

[](id:step7)
### 7. Set video quality
Call [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a0b08436c1e14a8d7d9875fae59ac6d84) in `V2TXLivePusher` to set the quality of videos watched by audience. The encoding parameters set determine the quality of videos presented to audience. The local video watched by the host is the original HD version that has not been encoded or compressed, and is therefore not affected by the settings. For details, please see [Setting Video Quality](https://intl.cloud.tencent.com/document/product/1071/41861).

[](id:step8)
### 8. Set the beauty filter style and skin brightening and rosy skin effects

Call [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a4fb05ae6b5face276ace62558731280a) in `V2TXLivePusher` to get a `TXBeautyManager` instance to set beauty filters.

#### Beauty filter style
The SDK has three built-in beauty filter algorithms, each corresponding to a beauty filter style. Choose one that best fits your product positioning. For details, please see the [TXBeautyManager.h](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#gafbbe0e87ec0168eacfc10e57c43abad8) file.

| Beauty Filter Style | Description |
|---------|---------|
| TXBeautyStyleSmooth | The smooth style, which features more obvious skin smoothing effects and is suitable for live showrooms  |
| TXBeautyStyleNature | The natural style, which retains more facial details and is more natural  |
| TXBeautyStylePitu | The Pitu style, which uses the beauty filter algorithm developed by YouTu Lab. Its effect is between the smooth style and the natural style, that is, it retains more skin details than the smooth style and delivers more obvious skin smoothing effects than the natural style.  |

You can call the [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXBeautyManager__ios.html#a8f2378a87c2e79fa3b978078e534ef4a) API in `TXBeautyManager` to set the beauty filter style.

<table>
<tr><th>Item</th><th width=51%>Configuration</th><th>Description</th></tr>
<tr>
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

- Call [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a4fb05ae6b5face276ace62558731280a) in `V2TXLivePusher` to get a `TXBeautyManager` instance to set color filters.
- Call the `setFilter` API in `TXBeautyManager` to set color filters. Color filters are a technology that adjusts the color tone of sections of an image. For example, it may lighten the yellow sections of an image to achieve the effect of skin brightening, or add warm tones to a video to give it a refreshing and soft boost.   
- Call the `setFilterStrength` API in `TXBeautyManager` to set the strength of a color filter. The higher the strength, the more obvious the effect. 

Based on our experience of operating Mobile QQ and Now Live, it’s not enough to use only the `setBeautyStyle` API in `TXBeautyManager` to set the beauty filter style. The `setBeautyStyle` API must be used together with `setFilter` to produce richer effects. Given this, our designers have developed 17 built-in color filters for you to choose from.
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


[](id:step11)
### 11. Set the video mirroring effect for audience
Call [setRenderMirror](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#adf4cd57c705a1022d6730fd722f8dab5) in `V2TXLivePusher` to set the camera mirror mode, which affects the way video images are presented to audience. By default, the local image seen by the host is flipped when the front camera is used.
![](https://main.qcloudimg.com/raw/520d16280962523809e5695d2483d9ef.png)

[](id:step12)
### 12. Publish streams in landscape mode
In most cases, hosts stream while holding their phones vertically, and audience watch videos in portrait resolutions (e.g., 540 × 960). However, there are also cases where hosts hold phones horizontally, and ideally, audience should watch videos in landscape resolutions (960 × 540).


By default, `V2TXLivePusher` outputs videos in portrait resolutions. You can publish landscape-mode videos to audience by modifying a parameter of the [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a0b08436c1e14a8d7d9875fae59ac6d84) API.
```objectivec
[_pusher setVideoQuality:videoQuality
             resolutionMode:isLandscape ? V2TXLiveVideoResolutionModeLandscape : V2TXLiveVideoResolutionModePortrait];
```

[](id:step13)
### 13. Set audio effects
Call [getAudioEffectManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__ios.html) in `V2TXLivePusher` to get a `TXAudioEffectManager` instance, which can be used to mix background music and set in-ear monitoring, reverb, and other audio effects. Background music mixing means mixing into the published stream the music played by the host’s phone so that audience can also hear the music.


- Call the `enableVoiceEarMonitor` API in `TXAudioEffectManager` to enable in-ear monitoring, which allows hosts to hear their vocals in earphones when they sing.
- Call the `setVoiceReverbType` API in `TXAudioEffectManager` to add reverb effects such as karaoke, hall, husky, and metal. The effects are applied to the videos watched by audience.
- Call the `setVoiceChangerType` API in `TXAudioEffectManager` to add voice changing effects such as little girl and middle-aged man to enrich host-audience interaction. The effects are applied to the videos watched by audience.
![](https://main.qcloudimg.com/raw/f8282bd6e1ba20e1e902bad52fa3131f.png)

>? For detailed instructions, please see [TXAudioEffectManager API](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXAudioEffectManager__ios.html).

[](id:step14)
### 14. Set watermarks

Call [setWatermark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#ad48aacbfad38b8f5389c159283fae859) in `V2TXLivePusher` to add a watermark to videos output by the SDK. The position of the watermark is determined by the `(x, y, scale)` parameter passed in.

- The watermark image must be in PNG rather than JPG format. The former carries opacity information, which allows the SDK to better address the image aliasing issue (changing the extension of a JPG image to PNG won’t work).
- The `(x, y, scale)` parameter specifies the normalized coordinates of the watermark relative to the resolution of the published video. For example, if the resolution of the published video is 540 x 960, and `(x, y, scale)` is set to `（0.1, 0.1, 0.1）`, the actual pixel coordinates of the watermark will be (540 x 0.1, 960 x 0.1). The width of the watermark will be the video width x 0.1, and the height will be scaled automatically.

```objectivec
// Set a video watermark
[_pusher setWatermark:[UIImage imageNamed:@"watermark"] x:0.03 y:0.015 scale:1];
```

[](id:step15)
### 15. Inform hosts of poor network conditions
Connecting phones to Wi-Fi does not necessarily guarantee network conditions. In case of poor Wi-Fi signal or limited bandwidth, the network speed of a Wi-Fi connected phone may be slower than that of a phone using 4G. Hosts should be informed when their network conditions are bad and be prompted to switch to a different network.    
![](https://main.qcloudimg.com/raw/faaef46a80988270d3ddc96ec4e578b9.png)  

You can capture the **V2TXLIVE_WARNING_NETWORK_BUSY** event using [onWarning](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLiveCode__ios.html#ga5506c2171438841ab3e99c80786c7ba0) in `V2TXLivePusherObserver`. The event indicates poor network conditions for hosts, which result in stuttering for audience. When this event occurs, you can send a UI message about poor network conditions to hosts, as shown above.
```
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
```

[](id:step16)
### 16. Send SEI messages
Call the [sendSeiMessage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a106dc65c2616b80e193aad95876f7fe6) API in `V2TXLivePusher` to send SEI messages. SEI refers to the supplementary enhancement information of encoded video. It is not used most of the time, but you can insert custom information into SEI messages. The information will be forwarded to audience by live streaming CDNs. The applications for SEI messages include:
- Live quiz: The publisher can use SEI messages to send questions to the audience. SEI can ensure synchronization among audio, video, and the questions.
- Live showroom: The publisher can use SEI messages to display lyrics to the audience in real time. The effects are not affected by reduction in video encoding quality.
- Online education: The publisher can use SEI messages to display pointers and sketches on slides to the audience in real time.

Custom data is inserted directly into video data and therefore cannot be too large in size (preferably several bytes). It’s common to insert information such as custom timestamps.
```objectiveC
int payloadType = 5;
NSString* msg = @"test";
[_pusher sendSeiMessage:payloadType data:[msg dataUsingEncoding:NSUTF8StringEncoding]];
```
Common open-source players or web players are incapable of parsing SEI messages. You must use `V2TXLivePlayer`, the built-in player of LiteAVSDK.
1. Configuration:
```objectiveC
int payloadType = 5;
[_player enableReceiveSeiMessage:YES payloadType:payloadType];
```
2. If the video streams played by `V2TXLivePlayer` contain SEI messages, you will receive the messages via the `onReceiveSeiMessage` callback in `V2TXLivePlayerObserver`.


## Event Handling
### Listening for events
The SDK listens for publishing events and errors via the [V2TXLivePusherObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusherObserver__ios.html) delegate. See [V2TXLiveCode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLiveCode__ios.html) for a detailed list of events and error codes.

### Errors 
An error indicates that the SDK encountered a serious problem that made it impossible for stream publishing to continue.

| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
|V2TXLIVE_ERROR_FAILED                  | -1 | A common error not yet classified |
|V2TXLIVE_ERROR_INVALID_PARAMETER       | -2 | An invalid parameter was passed in during API calling. |
|V2TXLIVE_ERROR_REFUSED                 | -3 | The API call was rejected.  |
|V2TXLIVE_ERROR_NOT_SUPPORTED           | -4 | The API cannot be called.  |
|V2TXLIVE_ERROR_INVALID_LICENSE         | -5 | Failed to call the API due to invalid license.  |
|V2TXLIVE_ERROR_REQUEST_TIMEOUT         | -6 | The server request timed out.  |
|V2TXLIVE_ERROR_SERVER_PROCESS_FAILED   | -7 | The server could not handle your request.  |

### Warnings 
A warning indicates that the SDK encountered a problem whose severity level is warning. Warning events trigger tentative protection or recovery logic and can often be resolved.

| Event ID | Code | Description |
| :-------------------  |:-------- |  :------------------------ |
|V2TXLIVE_WARNING_NETWORK_BUSY                  |  1101|  Bad network connection: data upload blocked due to limited upstream bandwidth. |
|V2TXLIVE_WARNING_VIDEO_BLOCK                   |  2105|  Latency during video playback.  |
|V2TXLIVE_WARNING_CAMERA_START_FAILED           | -1301|  Failed to turn the camera on.  |
|V2TXLIVE_WARNING_CAMERA_OCCUPIED               | -1316| The camera is occupied. Try a different camera. |
|V2TXLIVE_WARNING_CAMERA_NO_PERMISSION          | -1314| No access to the camera. This usually occurs on mobile devices and may be because the user denied the access. |
|V2TXLIVE_WARNING_MICROPHONE_START_FAILED       | -1302| Failed to turn the mic on. |
|V2TXLIVE_WARNING_MICROPHONE_OCCUPIED           | -1319| The mic is occupied. This occurs when, for example, the user is having a call on the mobile device. |
|V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION      | -1317| No access to the mic. This usually occurs on mobile devices and may be because the user denied the access. |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED  | -1309|  The system does not support screen sharing.  |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED   | -1308|  Failed to start screen recording. If this occurs on a mobile device, it may be because the user denied the access.  |
|V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED    | -7001|  Screen recording was stopped by the system.  |
