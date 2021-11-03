## Overview

Screen recording is a new feature in iOS 10. In addition to using ReplayKit to record video from the screen, which is possible in iOS 9, with iOS 10, users can also stream live video from the screen. For details, see [Go Live with ReplayKit](https://developer.apple.com/videos/play/wwdc2016/601/). In iOS 11, Apple made ReplayKit more usable and more universally applicable and launched [ReplayKit2](https://developer.apple.com/videos/play/wwdc2017/606/), going from supporting ReplayKit alone to allowing the recording of the entire screen. Therefore, we recommend using ReplayKit2 in iOS 11 to enable the screen sharing feature. Screen sharing relies on extensions, which operate as independent processes. However, to ensure system smoothness, iOS allocates limited resources to extensions and may kill extensions with high memory usage. Given this, Tencent Cloud has further reduced the memory usage of LiteAVSDK while retaining its high streaming quality and low latency to ensure the stability of extensions.

>!This document describes how to use ReplayKit2 in iOS 11 to publish streams from the screen. The parts about the use of the SDK also apply to other custom stream publishing scenarios. For details, please see the sample code in the `TXReplayKit_Screen` file of the [demo](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC/Basic/LivePushScreen).

## Tryout

To try out the screen sharing feature, [click here](https://itunes.apple.com/cn/app/%E8%A7%86%E9%A2%91%E4%BA%91%E5%B7%A5%E5%85%B7%E5%8C%85/id1152295397?mt=8) or scan the QR code below to download Video Cloud Toolkit.
![](https://main.qcloudimg.com/raw/386c06636b522fbd0f85714acf73209b.png)

>! You can publish streams from the screen only in iOS 11 or above.

## Sample Code
Regarding frequently asked questions among developers, Tencent Cloud offers an easy-to-understand API example project, which you can use to quickly learn how to use different APIs.

| Platform |                         GitHub Address                          |
| :------: | :----------------------------------------------------------: |
| iOS| [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/iOS/MLVB-API-Example-OC) |
| Android  | [GitHub](https://github.com/tencentyun/MLVBSDK/tree/master/Android/MLVB-API-Example) |

#### Directions
1. Open Control Center, touch and hold the record button, and select **Video Cloud Toolkit**.
2. Open **Video Cloud Toolkit**, tap **Screen Sharing**, enter a publishing URL or tap **New** to get a publishing URL, and tap **Start**.



If the configuration is successful, you will receive a banner notification about the starting of stream publishing, and can watch the stream on another device. To stop publishing, tap the red bar at the top.

## Environment Requirements

### Xcode

Xcode 9 or above is required, and your iPhone must be updated to iOS 11 or above. Screen recording is not supported on emulators.

### Create a broadcast upload extension
Open your project with Xcode and select **New** > **Target…** > **Broadcast Upload Extension**, as shown below.
![](https://main.qcloudimg.com/raw/c4c0b0ee049c733640f813a318a25adb.png)
Enter a product name and click **Finish**. A new directory with the product name entered will appear in your project. Under the directory, there is an automatically generated `SampleHandler` class, which is responsible for screen recording operations.

### Import LiteAVSDK
Import `TXLiteAVSDK.framework` into the broadcast upload extension the same way you import a framework into the host app. The libraries the SDK depends on are also the same. For details, see [SDK Integration > iOS](https://intl.cloud.tencent.com/document/product/1071/38155).


## Integration
[](id:step1)
### Step 1. Create a stream publishing object

Add the following code to `SampleHandler.m`:
<dx-codeblock>
::: objective objective
#import "SampleHandler.h"
#import "V2TXLivePusher.h"

static V2TXLivePusher *s_txLivePublisher;
static NSString *s_rtmpUrl;
:::
</dx-codeblock>
<dx-codeblock>
::: objective objective
 - (void)initPublisher {
         if (s_txLivePublisher) {
             [s_txLivePublisher stopPush];
    }
    s_txLivePublisher = [[V2TXLivePusher alloc] initWithLiveMode:V2TXLiveMode_RTMP];
    [s_txLivePublisher setObserver:self];
    [s_txLivePublisher startPush:s_rtmpUrl];
}
:::
</dx-codeblock>

- `s_txLivePublisher` is the object used for stream publishing. As more than one `sampleHandler` instance may be returned via the screen recording callback, the variable is declared as static to ensure that the same publisher is used during screen sharing.
- The best place to create a `s_txLivePublisher` object is in the `-[SampleHandler broadcastStartedWithSetupInfo:]` method. This callback is returned after the broadcast upload extension starts, after which you can initialize the publisher to start publishing streams. However, with ReplayKit2, when the broadcast upload extension starts, the `setupInfo` returned is `nil`, making it impossible to obtain the URL for publishing and other information. Therefore, it is necessary to send a notification to the host app when the callback is returned, set the publishing URL and specify information including orientation and resolution in the host app, and then pass the information to the extension to start publishing streams.
- For details about communication between the extension and host app, please see [Communication and Data Transfer Between Extensions and Host Apps](#accessory).

[](id:step2)
### Step 2. Enable landscape-mode streaming and set the resolution

Call [setVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLivePusher__ios.html#a0b08436c1e14a8d7d9875fae59ac6d84) to set the resolution (you can select from a number of resolutions) and orientation for stream publishing. Below is an example:

```objective-c
  static BOOL s_landScape; // `YES`: landscape; `NO`: portrait
  [s_txLivePublisher setVideoQuality:V2TXLiveVideoResolution960x540 
                      resolutionMode:s_landScape ? V2TXLiveVideoResolutionModeLandscape : V2TXLiveVideoResolutionModePortrait];
  [s_txLivePublisher startPush:s_rtmpUrl];
```

[](id:step3)
### Step 3. Publish video
ReplayKit transfers video to`-[SampleHandler processSampleBuffer:withType]` though callbacks.

```objectivec
- (void)processSampleBuffer:(CMSampleBufferRef)sampleBuffer withType:(RPSampleBufferType)sampleBufferType {
    switch (sampleBufferType) {
        case RPSampleBufferTypeVideo:
            // Handle video sample buffer
        {
                if (!CMSampleBufferIsValid(sampleBuffer))
                    return;
            // Reserve a video frame and send it when calling `startPush` to avoid cases where stream publishing fails due to the lack of video data when publishing starts or after landscape/portrait mode switch
                if (s_lastSampleBuffer) {
                    CFRelease(s_lastSampleBuffer);
                    s_lastSampleBuffer = NULL;
                }
                s_lastSampleBuffer = sampleBuffer;
                CFRetain(s_lastSampleBuffer);
                V2TXLiveVideoFrame *videoFrame = [V2TXLiveVideoFrame new];
                videoFrame.bufferType = V2TXLiveBufferTypePixelBuffer;
                videoFrame.pixelFormat = V2TXLivePixelFormatNV12;
                videoFrame.pixelBuffer = CMSampleBufferGetImageBuffer(sampleBuffer);
                videoFrame.rotation = V2TXLiveRotation0;
                [s_txLivePublisher sendCustomVideoFrame:videoFrame];
        }
}
```
Call `-[V2TXLivePusher sendCustomVideoFrame:]` to send `sampleBuffer`.

The intervals at which the system sends `sampleBuffer` are not fixed. If the screen is static, the intervals can be quite long. Given this, the SDK has an internal frame feeding mechanism.
>! As the intervals of frame capturing may be long when the screen changes little, we recommend that you reserve a video frame to avoid cases where no video data can be sent when publishing starts or after landscape/portrait mode switch.

[](id:step4)
### Step 4. Set watermarks
Tencent Video Cloud supports two watermark setting methods. One is adding watermarks in the publishing SDK before videos are encoded. The other is watermarking videos while they are being decoded in the cloud.

We recommend the former, as there are three major drawbacks to watermarking in the cloud:
 - Watermarking in the cloud drives up your expenses as it increases the load on CVMs and is a paid service.
 - It does not adapt well to situations such as resolution change during the stream publishing process, which may cause problems like blurry screen.
 - Watermarking in the cloud will result in an extra latency of 3s or longer. This is caused by transcoding.

The watermark image must be in PNG format. PNG images carry opacity information, which allows the SDK to better address the image aliasing issue. Please note that PNG images require processing by professional designers. You are not advised to change the extension of a JPG image to PNG in Windows and use it as a watermark directly.

```objectivec
// Set a video watermark
[s_txLivePublisher setWatermark:image x:0 y:0 scale:1];
```

[](id:step5)
### Step 5. Stop publishing
ReplayKit calls `-[SampleHandler broadcastFinished]` to stop stream publishing. Below is an example:

```objectivec
- (void)broadcastFinished {
    // User has requested to finish the broadcast.
    if (s_txLivePublisher) {
        [s_txLivePublisher stopPush];
        s_txLivePublisher = nil;
    }
}
```
As there can be only one `V2TXLivePusher` object running at a time, make sure that you release all the resources when stopping publishing.


## Event Handling
### 1. Listening for events
The SDK listens for publishing events and errors via the [V2TXLivePusherObserver](http://doc.qcloudtrtc.com/group__V2TXLivePusherObserver__android.html) delegate. See [V2TXLiveCode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__V2TXLiveCode__android.html) for a detailed list of events and error codes.

### 2. Errors
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

### 3. Warnings
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


[](id:accessory)
### Appendix: Communication and Data Transfer Between Extensions and Host Apps
ReplayKit2 invokes only the broadcast upload extension during screen sharing. The extension does not support UI operations and cannot implement complicated business logic. Therefore, the host app is often responsible for implementing business logic such as authentication, while the extension focuses on recording the screen and publishing the audio and video data captured. This makes it necessary to communicate and transfer data between the extension and host app.

#### 1. Sending local notifications
Users should be informed of the status of the extension. For example, in cases where the host app is not started, you can send a local notification asking users to interact with the host app. Below is an example of sending a notification to users when the broadcast upload extension is started.
<dx-codeblock>
::: code 
- (void)broadcastStartedWithSetupInfo:(NSDictionary<NSString *,NSObject *> *)setupInfo {
    [self sendLocalNotificationToHostAppWithTitle:@"Tencent Cloud Screen Sharing" msg:@"Screen recording has started. Return to Cloud Video Toolkit > MLVB > Screen Sharing to set the publishing URL, orientation, and resolution." userInfo:@{kReplayKit2UploadingKey: kReplayKit2Uploading}];
}

- (void)sendLocalNotificationToHostAppWithTitle:(NSString*)title msg:(NSString*)msg userInfo:(NSDictionary*)userInfo
{
    UNUserNotificationCenter* center = [UNUserNotificationCenter currentNotificationCenter];
  
    UNMutableNotificationContent* content = [[UNMutableNotificationContent alloc] init];
    content.title = [NSString localizedUserNotificationStringForKey:title arguments:nil];
    content.body = [NSString localizedUserNotificationStringForKey:msg  arguments:nil];
    content.sound = [UNNotificationSound defaultSound];
    content.userInfo = userInfo;
  
    // Schedule a local notification to be sent at the specified time
    UNTimeIntervalNotificationTrigger* trigger = [UNTimeIntervalNotificationTrigger
                                                  triggerWithTimeInterval:0.1f repeats:NO];
  
    UNNotificationRequest* request = [UNNotificationRequest requestWithIdentifier:@"ReplayKit2Demo"
                                                                          content:content trigger:trigger];
  
    // Add operation after the notification is sent
    [center addNotificationRequest:request withCompletionHandler:^(NSError * _Nullable error) {
        
    }];
}
:::
</dx-codeblock>

You can use this notification to ask the user to return to the host app to configure publishing information and start stream publishing.

#### 2. Sending notifications between processes via CFNotificationCenter
The extension and host app may also need to interact with each other in real time, which cannot be achieved through local notifications because with local notifications, code is triggered only after users tap the banner. Neither can it be implemented via NSNotificationCenter because NSNotificationCenter does not allow communication between processes. To send notifications between processes, you will need CFNotificationCenter, but instead of using the `userInfo` field for data transfer, you must configure an app group and use `NSUserDefault` for data transfer. For example, after getting the publishing URL, the host app can notify the broadcast upload extension via CFNotificationCenter that stream publishing can start. You may also use the clipboard, but delayed rendering is needed as the clipboard sometimes fails to transfer data between processes in real time.
<dx-codeblock>
::: code 
CFNotificationCenterPostNotification(CFNotificationCenterGetDarwinNotifyCenter(),
                                    kDarvinNotificationNamePushStart,
                                    NULL,
                                    nil,
                                    YES);
:::
</dx-codeblock>
The extension can start publishing streams after receiving this notification. As the notification is at the CF layer, to facilitate operations, it needs to be sent to the Cocoa layer via NSNotificationCenter.
<dx-codeblock>
::: code 
    CFNotificationCenterAddObserver(CFNotificationCenterGetDarwinNotifyCenter(),
                                    (__bridge const void *)(self),
                                    onDarwinReplayKit2PushStart,
                                    kDarvinNotificationNamePushStart,
                                    NULL,
                                    CFNotificationSuspensionBehaviorDeliverImmediately);
                                                                        
    [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(handleReplayKit2PushStartNotification:) name:@"Cocoa_ReplayKit2_Push_Start" object:nil];


static void onDarwinReplayKit2PushStart(CFNotificationCenterRef center,
                                        void *observer, CFStringRef name,
                                        const void *object, CFDictionaryRef
                                        userInfo)
{
// Send to the Cocoa layer
    [[NSNotificationCenter defaultCenter] postNotificationName:@"Cocoa_ReplayKit2_Push_Start" object:nil];
}

- (void)handleReplayKit2PushStartNotification:(NSNotification*)noti
{
// Get the data to be transferred by the host app via NSUserDefault or the clipboard
//    NSUserDefaults *defaults = [[NSUserDefaults alloc] initWithSuiteName:kReplayKit2AppGroupId];
  
    UIPasteboard* pb = [UIPasteboard generalPasteboard];
    NSDictionary* defaults = [self jsonData2Dictionary:pb.string];
  
    s_rtmpUrl = [defaults objectForKey:kReplayKit2PushUrlKey];
    s_resolution = [defaults objectForKey:kReplayKit2ResolutionKey];
    if (s_resolution.length < 1) {
        s_resolution = kResolutionHD;
    }
    NSString* rotate = [defaults objectForKey:kReplayKit2RotateKey];
    if ([rotate isEqualToString:kReplayKit2Portrait]) {
        s_landScape = NO;
    }
    else {
        s_landScape = YES;
    }
    [self start];
}
:::
</dx-codeblock>

## FAQs
ReplayKit2 is a new framework introduced by Apple in iOS 11, for which relatively few official documents have been released. The framework is still being improved, and problems have been found. See below for some common questions you may have when using ReplayKit2.

1. **When does screen recording stop automatically?**
Screen recording stops automatically when the screen locks or there is an incoming call. At such times, the `broadcastFinished` function in `SampleHandler` will be invoked, and you can send a notification to users about the interruption.

2. **Why does screen recording stop sometimes during screen sharing?**
The problem usually occurs after landscape/portrait mode switch if the resolution for stream publishing is set high. The broadcast upload extension is allocated a memory of only 50 MB and will be killed if its memory usage exceeds the limit. Given this, we recommend that you set the resolution to 720p or lower.

3. **Why are images streamed from the screen of iPhone X distorted?**
iPhone X has a notch at the top of the screen, so video captured from the screen is not in the aspect ratio of 16:9. If you set the output resolution for stream publishing to 16:9, for example, to HD (960 × 540), the images published will be slightly distorted because their original aspect ratio is not 16:9. We recommend that you set the resolution according to your screen size. Besides, if you play video streamed from the screen of iPhone X in aspect fit mode, the video may have black bars, and if you play it in aspect fill mode, the video may be cropped.
