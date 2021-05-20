TRTC supports two screen sharing schemes on iOS:
- **In-app sharing**
With in-app sharing, sharing is limited to the screens of the current app. It is supported on iOS 13 and above. As screens outside the current app cannot be shared, the scheme is suitable for scenarios with high requirements for privacy protection.
- **Cross-app sharing**
Based on Apple's ReplayKit scheme, cross-app sharing allows the sharing of screens across the system, but the steps to required to implement the scheme are more complicated than those for in-app sharing because the app must provide an additional extension.

>! Please note that the mobile editions of the TRTC SDK do not support "substream sharing" as the desktop editions do, for both iOS and Android ban the use of the camera by apps running in the background. It’s therefore of little point for the mobile editions to support the feature.

## Supported Platforms

| iOS | Android | macOS | Windows |Electron| Chrome |
|:-------:|:-------:|:-------:|:-------:|:-------:|:-------:|
|  &#10003; |  &#10003; |  &#10003;  |&#10003;  |   &#10003;  |  &#10003;  |

## In-app Sharing

You can implement the in-app sharing scheme simply by calling the [`startScreenCaptureInApp`](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a5dbd40c4ad65152e85591c8535b4ee90) API provided by the TRTC SDK and passing in the encoding parameter `TRTCVideoEncParam`. If the parameter is set to `nil`, the SDK will use the encoding parameters set before screen sharing.

We recommend the following encoding parameter settings for screen sharing on iOS:

| Item | Parameter Name | Recommended Value for Regular Scenarios | Recommended Value for Text-based Teaching |
|---------|---------|---------|-----|
| Resolution | videoResolution | 1280 × 720 | 1920 × 1080 |
| Frame rate | videoFps | 10 FPS | 8 FPS |
| Highest bitrate | videoBitrate| 1,600 Kbps | 2,000 Kbps |
| Resolution adaption | enableAdjustRes | No | No |

- As shared screens generally do not change drastically, it is not economical to use a high FPS. We recommend setting it to 10 FPS.
- If the screen you share contains a large amount of text, you can increase the resolution and bitrate accordingly.
- The highest bitrate (`videoBitrate`) refers to the highest output bitrate when a shared screen changes dramatically. If the shared content does not change a lot, the actual encoding bitrate will be lower.


## Cross-app Sharing

### Sample code
You can find the sample code for cross-app sharing in the **Screen** directory of [GitHub] which contains the following files:

```
├─ TRTCSimpleDemo              // A simple TRTC demo
|  ├─ Screen                   // Cross-app screen sharing demo
|  |  ├─ RTC                   // Demo for running TRTC in the call modes, to which the concept of roles does not apply
|  |  |  ├─ TXReplayKit_Screen // Code for the screen recording process Broadcast Upload Extension. For details, see step 2.
|  |  |  |  ├─ SampleHandler.swift // For receiving screen recording data from the system
|  |  |  |  ├─ Info.plist                          
|  |  |  |  ├─ TXReplayKit_Screen.entitlements // For setting an AppGroup to enable communication between processes
|  |  |  
|  |  ├─ ScreenEntranceViewController.swift    // Feature entry UI
|  |  ├─ ScreenViewController.swift            // Screen recording status UI
|  |  ├─ TRTCBroadcastExtensionLauncher.swift  // Auxiliary code for starting screen recording
```

You can run the demo as instructed in [README](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTC-API-Example-OC).


### Directions

To enable cross-app screen sharing on iOS, you need to add the screen recording process Broadcast Upload Extension, which works with the host app to push streams. A Broadcast Upload Extension is created by the system when screen sharing is needed and is responsible for receiving the screen images captured by the system. For this, you need to do the following:

1. Create an application group (App Group) and configure it in Xcode (optional) to enable communication between the Broadcast Upload Extension and host app.
2. Create a target of Broadcast Upload Extension in your project and integrate into it `TXLiteAVSDK_ReplayKitExt.framework` from the SDK package, which is tailored for the extension module.
3. Make the host app stand by to receive screen recording data from the Broadcast Upload Extension.
4. Use a helper class (`RPSystemBroadcastPickerView`) already implemented in the demo to make it possible to start screen sharing by clicking a button (optional), as in the iOS edition of VooV Meeting.

>! If you skip step 1, that is, if you do not configure an App Group (by passing in `nil` to the API), you can still enable screen sharing, but its stability will be compromised. Therefore, the steps may be complicated, but to ensure the stability of screen sharing, we suggest that you configure an App Group as described in this document.

<span id="createGroup"> </span>
#### Step 1. Create an App Group.
Log in to [**https://developer.apple.com/**](https://develop.apple.com) and do the following (**please download the corresponding provisioning profile again afterwards**.)

1. Click **Certificates, IDs & Profiles**.
2. Click "+" on the right.
3. Select **App Groups** and click **Continue**.
4. In the form that pops up, fill in the **Description** and **Identifier** boxes. For "Identifier", you need to pass in the `AppGroup` parameter in the API. After this, click **Continue**.
 ![](https://main.qcloudimg.com/raw/43dd60f5053b21c167ee3a8dbe7d16f9/Create_AppGroup.jpg)
5. Return to the "Identifiers" page, select **App IDs**, and click your `App ID` (you need to configure the host app and the AppID of the extension in the same way).
6. Select **App Groups** and click **Edit**.
7. In the form that pops up, select the App Group you created, click **Continue** to return to the edit page, and click **Save** to save the settings.
 ![](https://main.qcloudimg.com/raw/962c1b705433aa62c9617f90d28238c5/Apply_AppGroup.jpg)
8. Download the provisioning profile again and import it to Xcode.

<span id="createExtension"> </span>
#### Step 2. Create a Broadcast Upload Extension.
1. In the Xcode menu, click **File** > **New** > **Target...** > **Broadcast Upload Extension**.
2. In the dialog box that pops up, enter the information required. You **don't need to** check **Include UI Extension**. Click **Finish** to complete the creation.
3. Drag `TXLiteAVSDK_ReplayKitExt.framework` in the SDK package into the project and select the target created.
4. Click **+ Capability**, and double-click **App Groups**, as shown below:
 ![AddCapability](https://main.qcloudimg.com/raw/a2b38f1581a495f2a966f6eaf464e057.png)
 A file named `target name.entitlements` will appear in the file list as shown below. Select it, click "+", and enter the `App Group` created earlier.
 ![AddGroup](https://main.qcloudimg.com/raw/b4904a8b425cf55e58497b35c0700966.png)
5. Select the target of the host app **and configure it in the same way as described above.**
6. In the new target, Xcode will automatically create a `SampleHandler.m` file. Replace the file content with the following code. You need to **change `APPGROUP` in the code to the App Group Identifier created earlier**.

```objc
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
            tip = @"App disconnected";
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
#### Step 3. Make the host app stand by to receive data.
Before screen sharing starts, the host app must be put on standby to receive screen recording data from the Broadcast Upload Extension. To do this, follow these steps:
1. Make sure that camera capture is disabled in `TRTCCloud`; if not, call [`stopLocalPreview`](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a01ee967e3180a5e2fc0e37e9e99e85b3) to disable it.
2. Call the [`startScreenCaptureByReplaykit:appGroup:`](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a92330045ce479f3b5e5c6b366731c7ff) method and pass in the `AppGroup` set in [step 1](#createGroup) to put the SDK on standby.
3. The SDK will then wait for a user to trigger screen sharing. If a "triggering button" is not added as described in [step 4](#launch), users need to press and hold the screen recording button in the iOS Control Center to start screen sharing.
4. You can call the [`stopScreenCapture`](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) API to stop screen sharing at any time.

```
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

// Stop screen sharing.
- (void)stopScreenCapture {
    [[TRTCCloud sharedInstance] stopScreenCapture];
}

// Event notification for screen sharing start, which can be received through `TRTCCloudDelegate`
- (void)onScreenCaptureStarted
    [self showTip:@"Screen sharing started"];
}
```

<span id="launch"> </span>
#### Step 4. Add a screen sharing triggering button (optional)
In [step 3](#receive), users need to start screen sharing manually by pressing and holding the screen recording button in the Control Center. To make it possible to start screen sharing by clicking a button in your app as in VooV Meeting, follow these steps:

1. Find the `TRTCBroadcastExtensionLauncher` class in the [demo] and add it to your project.
2. Add a button to your UI and call the `launch` function of `TRTCBroadcastExtensionLauncher` in the response function of the button to trigger screen sharing.
```
// Customize a response for button clicking
- (IBAction)onScreenButtonTapped:(id)sender {
    [TRTCBroadcastExtensionLauncher launch
}
```

>!
>- Apple added `RPSystemBroadcastPickerView` to iOS 12.0, which can show a picker view in apps for users to select whether to start screen sharing. Currently, `RPSystemBroadcastPickerView` does not support custom UI. Nor does Apple provide an official triggering method.
>- `TRTCBroadcastExtensionLauncher` works by going through the subviews of `RPSystemBroadcastPickerView`, finding the UI button, and triggering its click event.
>- **Please note that this scheme is not recommended by Apple and may become invalid in its next update. We have therefore made [step 4](#launch) optional. You need to bear the risks arising from implementing the scheme yourself.**

## Viewing Shared Screens
- **Viewing screens shared by macOS/Windows users**
  When a macOS/Windows user in a room starts screen sharing, the screen will be shared through a substream, and other users in the room will be notified through [`onUserSubStreamAvailable`](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__csharp.html#a15be39bb902bf917321b26701e961286) in `TRTCCloudDelegate`.
  Users who want to view the shared screen can start rendering the substream image of the remote user through the [`startRemoteSubStreamView`](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#ae029514645970e7d32470cf1c7aca716) API.

- **Viewing screens shared by Android/iOS users**
  When an Android/iOS user starts screen sharing, the screen will be shared through the primary stream, and other users in the room will be notified through [`onUserVideoAvailable`](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a533d6ea3982a922dd6c0f3d05af4ce80) in `TRTCCloudDelegate`.
  Users who want to view the shared screen can start rendering the primary stream of the remote user through the [`startRemoteView`](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#af85283710ba6071e9fd77cc485baed49) API.







