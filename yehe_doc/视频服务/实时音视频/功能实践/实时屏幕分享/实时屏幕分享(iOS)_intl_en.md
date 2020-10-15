TRTC supports two different screen sharing schemes on iOS:
- **In-application sharing**
It refers to sharing the image of the current application, which is supported on iOS 13 and above. As the screen content outside the current application cannot be shared, it is suitable for scenarios with high requirements for privacy protection.

- **Cross-application sharing**
Based on Apple's ReplayKit scheme, this feature can share the screen content of the entire system. However, the current application needs to provide an additional `Extension` component; therefore, the connection process is more complicated than that of in-application sharing.

>! It should be noted that the mobile edition of TRTC SDK does not support "substream sharing" like the desktop edition, as both iOS and Android limit the camera permission for applications on the background, which makes substream sharing meaningless.

## Supported Platforms

| iOS | Android | macOS | Windows | Electron | WeChat Mini Program | Chrome Browser|
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |   ×   |  &#10003;  |

## In-application Sharing

You can implement the in-application sharing scheme simply by calling the [startScreenCaptureInApp](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5dbd40c4ad65152e85591c8535b4ee90) API provided by the TRTC SDK and passing in the encoding parameter `TRTCVideoEncParam`. If the parameter is set to `nil`, the SDK will use the values set before the screen sharing.

We recommend the following encoding parameters for screen sharing on iOS:

| Parameter Item | Parameter Name | Common Recommended Value | Recommended Value for Text-based Teaching | 
|---------|---------|---------|-----|
| Resolution | videoResolution | 1280x720 | 1920x1080 | 
| Frame rate | videoFps | 10 FPS | 8 FPS |
| Highest bitrate | videoBitrate| 1,600 Kbps | 2,000 Kbps |
| Resolution adaption | enableAdjustRes | No | No |

- As the content in screen sharing generally does not change drastically, it is not economical to set a high FPS, and 10 FPS is recommended.
- If the screen sharing content contains many words, you can increase the resolution and bitrate accordingly.
- The highest bitrate (`videoBitrate`) refers to the highest output bitrate when the image content changes dramatically. If the screen content does not change a lot, the actual encoding bitrate will be lower.


## Cross-application Sharing

### Sample code
The sample code for cross-application sharing is placed in the **Screen** directory at [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCSimpleDemo/), which contains the following files:

```
├─ TRTCSimpleDemo              // Lite TRTC demo
|  ├─ Screen                   // Cross-application screen sharing demo
|  |  ├─ RTC                   // Demo of TRTC running in call mode. In this mode, there is no concept of role
|  |  |  ├─ TXReplayKit_Screen // Code of screen sharing process `Broadcast Upload Extension`. For more information, please see step 2.
|  |  |  |  ├─ SampleHandler.swift // Code for receiving screen sharing data from system
|  |  |  |  ├─ Info.plist                          
|  |  |  |  ├─ TXReplayKit_Screen.entitlements // Code for setting `AppGroup` information for communication between processes
|  |  |  
|  |  ├─ ScreenEntranceViewController.swift    // Feature entry UI
|  |  ├─ ScreenViewController.swift            // Screen sharing status UI
|  |  ├─ TRTCBroadcastExtensionLauncher.swift  // Auxiliary code for waking up system screen sharing
```

You can run the demos as instructed in [README](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTCSimpleDemo/README.md).


### Connection directions

For cross-application screen sharing on iOS, you need to add the `Extension` screen sharing process to work with the primary application process for push. The `Extension` screen sharing process is created by the system when screen sharing needs to be started and is used to receive the captured screen image; therefore, you need to perform the following steps:

1. Create an application group (`App Group`) and configure it in Xcode (optionally). This step is used to enable communication between the `Extension` screen sharing process and the primary application process.
2. Create a target of `Broadcast Upload Extension` in your project and integrate the `TXLiteAVSDK_ReplayKitExt.framework` tailored for the extension module in the SDK package into the target.
3. Connect to the receipt logic of the primary application so as to make it wait to receive the screen sharing data from `Broadcast Upload Extension`.
4. Use a helper class (`RPSystemBroadcastPickerView`) implemented in advance in the demo to implement the feature of waking up screen sharing by simply clicking a button like in VooV Meeting for iOS.

>! If you skip step 1, that is, if you do not configure an `App Group` (by passing in `nil` to the API), screen sharing can still run, but the stability will be compromised. Therefore, although there are many steps, please configure a correct `App Group` to ensure screen sharing stability.

<span id="createGroup"> </span>
#### Step 1. Create an App Group
Log in to [develop.apple.com](https://develop.apple.com) with your account and perform the following operations (**please download the corresponding provisioning profile again after completing the steps**):

1. Click **Certificates, IDs & Profiles**.
2. Click "+" on the right.
3. Select **App Groups** and click **Continue**.
4. Enter the "Description" and "Identifier" in the pop-up form. You need to pass in the corresponding `AppGroup` parameter in the API to "Identifier". After completing these settings, click **Continue**.
 ![](https://main.qcloudimg.com/raw/43dd60f5053b21c167ee3a8dbe7d16f9/Create_AppGroup.jpg)
5. Return to the "Identifier" page, select **App IDs** on the top-left sidebar and click your `App ID` (you need to configure the `AppID` fields for both the primary application and `Extension` in the similar way).
6. Select **App Groups** and click **Edit**.
7. In the pop-up form, select the `App Group` that you created earlier, click **Continue** to return to the editing page, and click **Save** to save the settings.
 ![](https://main.qcloudimg.com/raw/962c1b705433aa62c9617f90d28238c5/Apply_AppGroup.jpg)
8. Download the provisioning profile again and configure it into Xcode.

<span id="createExtension"> </span>
#### Step 2. Create the Broadcast Upload Extension
1. In Xcode menu, click **File** > **New** > **Target...** > **Broadcast Upload Extension**.
2. In the pop-up dialog box, enter the relevant information. You **don't need to** check **Include UI Extension**. Click **Finish** to complete the creation.
3. Drag `TXLiteAVSDK_ReplayKitExt.framework` in the downloaded SDK package into the project and check the newly created target.
4. Select the new target, click **+ Capability**, and double-click **App Groups** as shown below:
 ![AddCapability](https://main.qcloudimg.com/raw/a2b38f1581a495f2a966f6eaf464e057.png)
 After these steps are completed, a file named `target name.entitlements` will be generated in the file list as shown below. Select it and click "+" to enter the just created `App Group`.
 ![AddGroup](https://main.qcloudimg.com/raw/b4904a8b425cf55e58497b35c0700966.png)
5. Select the target of the primary application **and configure it in the same way as above.**
6. In the new target, Xcode will automatically create a `SampleHandler.m` file. Replace the file content with the following code and **replace the `APPGROUP` in the code with the just created `App Group Identifier`**.

```objc
#import "SampleHandler.h"
@import TXLiteAVSDK_ReplayKitExt;

#define APPGROUP @"group.com.tencent.liteav.RPLiveStreamShare"

@interface SampleHandler() <TXReplayKitExtDelegate>
@end

@implementation SampleHandler
// Note: replace the `APPGROUP` with the just created `App Group Identifier`.
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
- (void)boradcastFinished:(TXReplayKitExt *)broadcast reason:(TXReplayKitExtReason)reason
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
            tip = @"Integration error (the SDK version number does not match)";
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
```

<span id="receive"> </span>
#### Step 3. Connect to the receipt logic of the primary application
Connect to the receipt logic of the primary application in the following steps, so that the primary application can stay in `waiting` status before screen sharing starts in order to receive the screen sharing data from the `Broadcast Upload Extension` process at any time.
1. Make sure that camera capture has been disabled in `TRTCCloud`; and if not, call [stopLocalPreview](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3) to disable it.
2. Call the [startScreenCaptureByReplaykit:appGroup:](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a92330045ce479f3b5e5c6b366731c7ff) method and pass in the `AppGroup` set in [step 1](#createGroup) to make the SDK enter the `waiting` status.
3. Wait for the user to trigger screen sharing. If the "triggering button" in [step 4](#launch) is not implemented, the user needs to trigger screen sharing by pressing and holding the screen recording button in Control Center of iOS:
4. You can call the [stopScreenCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) API to stop screen sharing at any time.
 
```
// Start screen sharing. You need to replace the `APPGROUP` with the just created `App Group Identifier`.
- (void)startScreenCapture {
    TRTCVideoEncParam *videoEncConfig = [[TRTCVideoEncParam alloc] init];
    videoEncConfig.videoResolution = TRTCVideoResolution_1280_720;
    videoEncConfig.videoFps = 10;
    videoEncConfig.videoBitrate = 2000;
		// You need to replace the `APPGROUP` with the just created `App Group Identifier`:
    [[TRTCCloud sharedInstance] startScreenCaptureByReplaykit:videoEncConfig
                                                     appGroup:APPGROUP];
}

// Stop screen sharing
- (void)stopScreenCapture {
    [[TRTCCloud sharedInstance] stopScreenCapture];
}

// Event notification for screen sharing start, which can be received through `TRTCCloudDelegate`
- (void)onScreenCaptureStarted {
    [self showTip:@"Screen sharing started"];
}
```

<span id="launch"> </span>
#### Step 4. Add a screen sharing triggering button (optional)
Till [step 3](#receive), the user needs to start screen sharing manually by pressing and holding the screen recording button in Control Center. You can implement the feature of triggering screen sharing simply by clicking a button like in VooV Meeting in the following steps:

1. Find the `TRTCBroadcastExtensionLauncher` class in the [demo](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCSimpleDemo/Screen) and add it to your project.
2. Place a button on your UI and call the `launch` function of `TRTCBroadcastExtensionLauncher` in the response function of the button to wake up screen sharing.

```
// Custom button response method
- (IBAction)onScreenButtonTapped:(id)sender {
    [TRTCBroadcastExtensionLauncher launch];
}
```

>!Apple added `RPSystemBroadcastPickerView` to iOS 12.0, which can pop up a launcher in applications for user to confirm whether to start screen sharing. Currently, `RPSystemBroadcastPickerView` does not support custom UI or provide an official wakeup method.
>`TRTCBroadcastExtensionLauncher` works by traversing subviews of `RPSystemBroadcastPickerView` to find the `UIButton` and trigger its click event.
> **However, this scheme is not officially recommended by Apple and may become invalid in the next system update. Therefore, [step 4](#launch) is only an alternative scheme, and all risks arising from using it shall be borne by you.**

## Viewing Shared Screen
- **View macOS/Windows screen sharing**
  When a macOS/Windows user in a room starts screen sharing, the screen will be shared through a substream, and other users in the room will get a notification through the [onUserSubStreamAvailable](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) event in `TRTCCloudDelegate`.
  Users who want to view the shared screen can start rendering the substream image of the remote user through the [startRemoteSubStreamView](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) API.

- **View Android/iOS screen sharing**
  When an Android/iOS user starts screen sharing, the screen will shared through the primary stream, and other users in the room will get a notification through the [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) event in `TRTCCloudDelegate`.
  Users who want to view the shared screen can start rendering the primary stream image of the remote user through the [startRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) API.








