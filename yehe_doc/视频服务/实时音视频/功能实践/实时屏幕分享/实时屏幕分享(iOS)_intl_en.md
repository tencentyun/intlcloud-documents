TRTC supports two screen sharing schemes on iOS:
- **In-app sharing**
With in-app sharing, sharing is limited to the views of the current app. This feature is supported on iOS 13 and above. As content outside the current app cannot be shared, this feature is suitable for scenarios with high requirements on privacy protection.
- **Cross-app sharing**
Based on Apple's ReplayKit scheme, cross-app sharing allows the sharing of content across the system, but the steps required to implement this feature are more complicated than those for in-app sharing as an additional extension is needed.



## Supported Platforms

| iOS | Android | macOS | Windows | Electron| Chrome |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |   &#10003;  |

## In-app Sharing

You can implement in-app sharing simply by calling the [startScreenCaptureInApp](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a16d30ca3f89863da2581ff3872bf31f0) API of the TRTC SDK, passing in the encoding parameter `TRTCVideoEncParam`. If `TRTCVideoEncParam` is set to `nil`, the SDK will use the encoding parameters set previously.

We recommend the following encoding settings for screen sharing on iOS:

| Item | Parameter | Recommended Value for Regular Scenarios | Recommended Value for Text-based Teaching |
|---------|---------|---------|-----|
| Resolution | videoResolution | 1280 × 720 | 1920 × 1080 |
| Frame rate | videoFps | 10 fps | 8 fps |
| Highest bitrate | videoBitrate| 1600 Kbps | 2000 Kbps |
| Resolution adaption | enableAdjustRes | NO | NO |

- As screen content generally does not change drastically, it is not economical to use a high frame rate. We recommend setting it to 10 fps.
- If the screen you share contains a large amount of text, you can increase the resolution and bitrate accordingly.
- The highest bitrate (`videoBitrate`) refers to the highest output bitrate when a shared screen changes dramatically. If the shared content does not change a lot, the actual encoding bitrate will be lower.


## Cross-app Sharing

### Sample code
You can find the sample code for cross-app sharing in the **ScreenShare** directory of [this GitHub page](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC), which contains the following files:

```
├─ TRTC-API-Example-OC              // TRTC API examples 
|  ├─ Basic                   // Demonstrates the cross-app screen sharing feature
|  |  ├─ ScreenShare                   // Demonstrates the cross-app screen sharing feature
|  |  |  ├── ScreenAnchorViewController.h
|  |  |  ├── ScreenAnchorViewController.m       // Screen recording view for anchor
|  |  |  ├── ScreenAnchorViewController.xib
|  |  |  ├── ScreenAudienceViewController.h
|  |  |  ├── ScreenAudienceViewController.m     // Screen recording watching view for audience
|  |  |  ├── ScreenAudienceViewController.xib
|  |  |  ├── ScreenEntranceViewController.h
|  |  ├─ ScreenEntranceViewController.swift    // Screen sharing starting view
|  |  |  ├── ScreenEntranceViewController.xib
|  |  |  ├── TRTCBroadcastExtensionLauncher.h
|  |  |  ├── TRTCBroadcastExtensionLauncher.m   // Supplementary code for starting screen recording
|  |  |  ├── TXReplayKit_Screen   // Code for the screen recording process Broadcast Upload Extension. For details, see step 2.
|  |  |  │   ├── Info.plist
|  |  |  │   ├── SampleHandler.h
|  |  |  │   └── SampleHandler.m                // Code for receiving screen recording data from the system
```

You can run the demo as instructed in [README](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTC-API-Example-OC/README.md).


### Directions

To enable cross-app screen sharing on iOS, you need to add the screen recording process Broadcast Upload Extension, which works with the host app to push streams. A Broadcast Upload Extension is created by the system when screen sharing is needed and is responsible for receiving the screen images captured by the system. For this, you need to do the following:

1. Create an App Group and configure it in Xcode (optional) to enable communication between the Broadcast Upload Extension and host app.
2. Create a target of Broadcast Upload Extension in your project and integrate into it `TXLiteAVSDK_ReplayKitExt.framework` from the SDK package, which is tailored for the extension module.
3. Make the host app wait to receive screen recording data from the Broadcast Upload Extension.
4. Use a helper class (`RPSystemBroadcastPickerView`) already implemented in the demo to make it possible to start screen sharing by tapping a button (optional), as in VooV Meeting for iOS.

>! If you skip step 1, that is, if you do not configure an App Group (by passing in `nil` to the API), you can still enable screen sharing, but its stability will be compromised. Therefore, to ensure the stability of screen sharing, we suggest that you configure an App Group as described in this document.

[](id:createGroup)
#### Step 1. Create an App Group
Log in to [**https://developer.apple.com/**](https://develop.apple.com) and do the following. **You need to download the provisioning profile again afterwards**.

1. Click **Certificates, IDs & Profiles**.
2. Click "+" next to **Identifiers**.
3. Select **App Groups** and click **Continue**.
4. In the form that pops up, fill in the **Description** and **Identifier** boxes. For **Identifier**, type the `AppGroup` value passed in to the API. After this, click **Continue**.
 ![](https://main.qcloudimg.com/raw/43dd60f5053b21c167ee3a8dbe7d16f9/Create_AppGroup.jpg)
5. Select **Identifiers** on the top left sidebar, and click your App ID (you need to configure App ID for the host app and extension in the same way).
6. Select **App Groups** and click **Edit**.
7. In the form that pops up, select the App Group you created, click **Continue** to return to the edit page, and click **Save** to save the settings.
 ![](https://main.qcloudimg.com/raw/962c1b705433aa62c9617f90d28238c5/Apply_AppGroup.jpg)
8. Download the provisioning profile again and import it to Xcode.

[](id:createExtension)
#### Step 2. Create a Broadcast Upload Extension
1. In the Xcode menu, click **File** > **New** > **Target...**, and select **Broadcast Upload Extension**.
2. In the dialog box that pops up, enter the information required. You **don't need to** check **Include UI Extension**. Click **Finish** to complete the creation.
3. Drag `TXLiteAVSDK_ReplayKitExt.framework` in the SDK package into the project and select the target created.
4. Click **+ Capability**, and double-click **App Groups**, as shown below:
 ![AddCapability](https://main.qcloudimg.com/raw/a2b38f1581a495f2a966f6eaf464e057.png)
 A file named `target name.entitlements` will appear in the file list as shown below. Select it, click "+", and enter the `App Group` created earlier.
 ![AddGroup](https://main.qcloudimg.com/raw/b4904a8b425cf55e58497b35c0700966.png)
5. Select the target of the host app **and configure it in the same way as described above.**
6. In the new target, Xcode will automatically create a file named `SampleHandler.h`. Replace the file content with the following code. You need to **change `APPGROUP` in the code to the App Group Identifier created earlier**.
<dx-codeblock>
::: iOS object-c
#import "SampleHandler.h"
@import TXLiteAVSDK_ReplayKitExt;

#define APPGROUP @"group.com.tencent.liteav.RPLiveStreamShare"

@interface SampleHandler() <TXReplayKitExtDelegate>
@end

@implementation SampleHandler
// Note: replace `APPGROUP` with the App Group Identifier created earlier.
- (void)broadcastStartedWithSetupInfo:(NSDictionary<NSString *,NSObject *> *)setupInfo {
    [[TXReplayKitExt sharedInstance] setupWithAppGroup:APPGROUP delegate:self];
}

- (void)broadcastPaused {
    // User has requested to pause the broadcast. Samples will stop being delivered.
}

- (void)broadcastResumed {
    // User has requested to resume the broadcast. Samples delivery will resume.
}

- (void)broadcastFinished {
    [[TXReplayKitExt sharedInstance] finishBroadcast];
    // User has requested to finish the broadcast.
}

#pragma mark - TXReplayKitExtDelegate
- (void)broadcastFinished:(TXReplayKitExt *)broadcast reason:(TXReplayKitExtReason)reason
{
    NSString *tip = @"";
    switch (reason) {
        case TXReplayKitExtReasonRequestedByMain:
            tip = @"Screen sharing ended";
            break;
        case TXReplayKitExtReasonDisconnected:
            tip = @"Application disconnected";
            break;
        case TXReplayKitExtReasonVersionMismatch:
            tip = @"Integration error (SDK version mismatch)";
            break;
    }

    NSError *error = [NSError errorWithDomain:NSStringFromClass(self.class)
                                         code:0
                                     userInfo:@{
                                         NSLocalizedFailureReasonErrorKey:tip
                                     }];
    [self finishBroadcastWithError:error];
}

- (void)processSampleBuffer:(CMSampleBufferRef)sampleBuffer withType:(RPSampleBufferType)sampleBufferType {
    switch (sampleBufferType) {
        case RPSampleBufferTypeVideo:
            [[TXReplayKitExt sharedInstance] sendVideoSampleBuffer:sampleBuffer];
            break;
        case RPSampleBufferTypeAudioApp:
            // Handle audio sample buffer for app audio
            break;
        case RPSampleBufferTypeAudioMic:
            // Handle audio sample buffer for mic audio
            break;
            
        default:
            break;
    }
}
@end
:::
</dx-codeblock>

[](id:receive)
#### Step 3. Make the host app wait to receive data
Before screen sharing starts, the host app must be on standby to receive screen recording data from the Broadcast Upload Extension. To achieve this, follow these steps:
1. Make sure that camera capturing has been disabled in `TRTCCloud`; if not, call [stopLocalPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3) to disable it.
2. Call the [startScreenCaptureByReplaykit:appGroup:](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a78a8da8c2f235446d03cd2db26f97b60) API, passing in the `AppGroup` set in [step 1](#createGroup) to put the SDK on standby.
3. The SDK will then wait for a user to trigger screen sharing. If a "triggering button" is not added as described in [step 4](#launch), users need to press and hold the screen recording button in the iOS Control Center to start screen sharing.

4. You can call [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) to stop screen sharing at any time.
<dx-codeblock>
::: iOS object-c
// Start screen sharing. You need to replace `APPGROUP` with the App Group Identifier created earlier.
- (void)startScreenCapture {
    TRTCVideoEncParam *videoEncConfig = [[TRTCVideoEncParam alloc] init];
    videoEncConfig.videoResolution = TRTCVideoResolution_1280_720;
    videoEncConfig.videoFps = 10;
    videoEncConfig.videoBitrate = 2000;
    // You need to replace `APPGROUP` with the App Group Identifier created earlier.
    [[TRTCCloud sharedInstance] startScreenCaptureByReplaykit:videoEncConfig
                                                     appGroup:APPGROUP];
}

// Stop screen sharing
- (void)stopScreenCapture {
    [[TRTCCloud sharedInstance] stopScreenCapture];
}

// Event notification for the start of screen sharing, which can be received through `TRTCCloudDelegate`
- (void)onScreenCaptureStarted
    [self showTip:@"Screen sharing started"];
}
:::
</dx-codeblock>

[](id:launch)
#### Step 4. Add a screen sharing triggering button (optional)
In [step 3](#receive), users need to start screen sharing manually by pressing and holding the screen recording button in the Control Center. To make it possible to start screen sharing by tapping a button in your app as in VooV Meeting, follow these steps:


1. Find the `TRTCBroadcastExtensionLauncher` class in the [demo](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC/Basic/ScreenShare) and add it to your project.
2. Add a button to your UI and call the `launch` function of `TRTCBroadcastExtensionLauncher` in the response function of the button to trigger screen sharing.
<dx-codeblock>
::: iOS object-c
// Customize a response for button tapping
- (IBAction)onScreenButtonTapped:(id)sender {
    [TRTCBroadcastExtensionLauncher launch];
}
:::
</dx-codeblock>

>!
>- Apple added `RPSystemBroadcastPickerView` to iOS 12.0, which can show a picker view in apps for users to select whether to start screen sharing. Currently, `RPSystemBroadcastPickerView` does not support custom UI, and Apple does not provide an official triggering method.
>- `TRTCBroadcastExtensionLauncher` works by going through the subviews of `RPSystemBroadcastPickerView`, finding the UI button, and triggering its tapping event.
>- **Please note that this scheme is not recommended by Apple and may become invalid in its next update. We have therefore made [step 4](#launch) optional. You need to bear the risks of using the scheme yourself.**

## Watching Shared Screen
- **Watch screens shared by macOS/Windows users**
  When a macOS/Windows user in a room starts screen sharing, the screen will be shared through a substream, and other users in the room will be notified through [onUserSubStreamAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__csharp.html#a52ad5b09959df6e940aec7fb9615de9c) in `TRTCCloudDelegate`.
  Users who want to watch the shared screen can start rendering the substream image of the remote user by calling the [startRemoteSubStreamView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) API.

- **Watch screens shared by Android/iOS users**
  When an Android/iOS user starts screen sharing, the screen will be shared through the primary stream, and other users in the room will be notified through [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) in `TRTCCloudDelegate`.
  Users who want to watch the shared screen can start rendering the primary stream of the remote user by calling the [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) API.








