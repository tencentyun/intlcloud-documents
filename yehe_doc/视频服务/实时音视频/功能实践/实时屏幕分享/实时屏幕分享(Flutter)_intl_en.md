## Android
The TRTC SDK supports screen sharing on Android. This means you can share your screen with other users in the same room. Pay attention to the following points regarding this feature:

- Unlike the desktop edition, for Android, SDK versions earlier than v8.6 do not support substream screen sharing. Therefore, video capturing by the camera must be stopped first before screen sharing can start. Substream screen sharing is supported on v8.6 and later versions, so there is no need to stop video capturing by the camera.
- Screen sharing consumes CPU. On Android, a background app consuming CPU continuously is very likely to be killed by the system. The solution to this problem is creating a floating window after screen sharing starts. As Android does not kill apps with foreground views, your app can share the screen continuously without being killed by the system.


### Starting screen sharing
To start screen sharing on Android, simply call [startScreenCapture()](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html) in `TRTCCloud`. However, to ensure the stability and video quality of screen sharing, you need to do the following.

#### Adding an activity
Copy the activity below and paste it in the manifest file. You can skip this if the activity is already included in your project code.
```xml
<activity 
    android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity" 
    android:theme="@android:style/Theme.Translucent"/>
```

#### Setting video encoding parameters
By setting the first parameter `encParams` in [startScreenCapture()](https://pub.dev/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html), you can specify the encoding quality of screen sharing. If `encParams` is set to `null`, the SDK will use the encoding parameters set previously. We recommend the following settings:

| Item | Parameter | Recommended Value for Regular Scenarios | Recommended Value for Text-based Teaching |
|---------|---------|---------|-----|
| Resolution | videoResolution | 1280 × 720 | 1920 × 1080 |
| Frame rate | videoFps | 10 fps | 8 fps |
| Highest bitrate | videoBitrate| 1600 Kbps | 2000 Kbps |
| Resolution adaption | enableAdjustRes | NO | NO |
>?
>- As screen content generally does not change drastically, it is not economical to use a high frame rate. We recommend setting it to 10 fps.
>- If the screen you share contains a large amount of text, you can increase the resolution and bitrate accordingly.
>- The highest bitrate (`videoBitrate`) refers to the highest output bitrate when a shared screen changes dramatically. If the shared content does not change a lot, the actual encoding bitrate will be lower.

#### Displaying a floating window
Since Android 7.0, apps running in the background tend to be killed by the system if they consume CPU. To prevent your app from being killed when it is sharing the screen in the background, you need to create a floating window when screen sharing starts, which also serves the purpose of reminding the user to avoid displaying personal information as his or her screen is being shared.

##### Method: displaying a common floating window
The code in [tool.dart](https://github.com/c1avie/trtc_demo/blob/master/lib/page/trtcmeetingdemo/tool.dart) offers an example of how to create a mini floating window similar to the one in VooV Meeting:
```
// Create a floating window when screen sharing starts to prevent the app from being killed when running in the background
  static void showOverlayWindow() {
    SystemWindowHeader header = SystemWindowHeader(
      title: SystemWindowText(
          text: "Screen being shared", fontSize: 14, textColor: Colors.black45),
      decoration: SystemWindowDecoration(startColor: Colors.grey[100]),
    );
    SystemAlertWindow.showSystemWindow(
      width: 18,
      height: 95,
      header: header,
      margin: SystemWindowMargin(top: 200),
      gravity: SystemWindowGravity.TOP,
    );
  }
```

## iOS
- **[In-app sharing](#Internal)**
With in-app sharing, sharing is limited to the views of the current app. This feature is supported on iOS 13 and above. As content outside the current app cannot be shared, this feature is suitable for scenarios with high requirements on privacy protection.
- **[Cross-app sharing](#Cross)**
Based on Apple's ReplayKit scheme, cross-app sharing allows the sharing of content across the system, but the steps required to implement this feature are more complicated than those for in-app sharing as an additional extension is needed.

[](id:Internal)
### Scheme 1: in-app sharing on iOS

You can implement in-app sharing simply by calling the [startScreenCapture](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html) API of the TRTC SDK, passing in the encoding parameter `TRTCVideoEncParam`, and setting the `appGroup` parameter to `''`. If `TRTCVideoEncParam` is set to `null`, the SDK will use the encoding parameters set previously.

We recommend the following encoding settings for screen sharing on iOS:

| Item | Parameter | Recommended Value for Regular Scenarios | Recommended Value for Text-based Teaching |
|---------|---------|---------|-----|
| Resolution | videoResolution | 1280 × 720 | 1920 × 1080 |
| Frame rate | videoFps | 10 fps | 8 fps |
| Highest bitrate | videoBitrate| 1600 Kbps | 2000 Kbps |
| Resolution adaption | enableAdjustRes | NO | NO |

>?
>- As screen content generally does not change drastically, it is not economical to use a high frame rate. We recommend setting it to 10 fps.
>- If the screen you share contains a large amount of text, you can increase the resolution and bitrate accordingly.
>- The highest bitrate (`videoBitrate`) refers to the highest output bitrate when a shared screen changes dramatically. If the shared content does not change a lot, the actual encoding bitrate will be lower.

[](id:Cross)
### Scheme 2: cross-app sharing on iOS

#### Sample code
You can find the sample code for cross-app sharing in the **ios** directory of the [TRTC demo](https://github.com/c1avie/trtc_demo). The directory contains the following files:

```
├── Broadcast.Upload        // Code for the screen recording process Broadcast Upload Extension. For details, see step 2 below.
│   ├── Broadcast.Upload.entitlements       // Code for configuring an App Group to enable communication between processes
│   ├── Broadcast.UploadDebug.entitlements  // Code for configuring an App Group to enable communication between processes (debug environment)
│   ├── Info.plist
│   └── SampleHandler.swift     // Code for receiving screen recording data from the system
├── Resource                    // Resource file
├── Runner                      // A simple TRTC demo
├── TXLiteAVSDK_ReplayKitExt.framework      //TXLiteAVSDK_ReplayKitExt SDK
```

You can run the demo as instructed in [README](https://github.com/c1avie/trtc_demo/blob/master/README.md).


#### Directions
To enable cross-app screen sharing on iOS, you need to add the screen recording process Broadcast Upload Extension, which works with the host app to push streams. A Broadcast Upload Extension is created by the system when a screen needs to be shared and is responsible for receiving the screen images captured by the system. For this, you need to do the following:
1. Create an App Group and configure it in Xcode (optional) to enable communication between the Broadcast Upload Extension and host app.
2. Create a target of Broadcast Upload Extension in your project and integrate into it `TXLiteAVSDK_ReplayKitExt.framework` from the SDK package, which is tailored for the extension module.
3. Make the host app wait to receive screen recording data from the Broadcast Upload Extension.
4. Edit the `pubspec.yaml` file and import the `replay_kit_launcher` plugin to make it possible to start screen sharing by tapping a button (optional), as in TRTC Demo Screen.
```
# Import the TRTC SDK and `replay_kit_launcher`
dependencies:
  tencent_trtc_cloud: ^0.2.1
  replay_kit_launcher: ^0.2.0+1
```

>! If you skip [step 1](#Step1), that is, if you do not configure an App Group (by passing `null` in the API), you can still enable the screen sharing feature, but its stability will be compromised. Therefore, to ensure the stability of screen sharing, we suggest that you configure an App Group as described in this document.

[](id:createGroup)[](id:Step1)
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
6. In the new target, Xcode will create a `SampleHandler.swift` file. Replace the file content with the following code. You need to **change `APPGROUP` in the code to the App Group Identifier created earlier**.
<dx-codeblock>
::: iOS swift

import ReplayKit
import TXLiteAVSDK_ReplayKitExt


let APPGROUP = "group.com.tencent.comm.trtc.demo"

class SampleHandler: RPBroadcastSampleHandler, TXReplayKitExtDelegate {

    let recordScreenKey = Notification.Name.init("TRTCRecordScreenKey")
    
    override func broadcastStarted(withSetupInfo setupInfo: [String : NSObject]?) {
        // User has requested to start the broadcast. Setup info from the UI extension can be supplied but optional.
        TXReplayKitExt.sharedInstance().setup(withAppGroup: APPGROUP, delegate: self)
    }
    
    override func broadcastPaused() {
        // User has requested to pause the broadcast. Samples will stop being delivered.
    }
    
    override func broadcastResumed() {
        // User has requested to resume the broadcast. Samples delivery will resume.
    }
    
    override func broadcastFinished() {
        // User has requested to finish the broadcast.
        TXReplayKitExt.sharedInstance() .finishBroadcast()
    }
    
    func broadcastFinished(_ broadcast: TXReplayKitExt, reason: TXReplayKitExtReason) {
        var tip = ""
        switch reason {
        case TXReplayKitExtReason.requestedByMain:
            tip = "Screen sharing ended"
            break
        case TXReplayKitExtReason.disconnected:
            tip = "App was disconnected"
            break
        case TXReplayKitExtReason.versionMismatch:
            tip = "Integration error (SDK version mismatch)"
            break
        default:
            break
        }
        
        let error = NSError(domain: NSStringFromClass(self.classForCoder), code: 0, userInfo: [NSLocalizedFailureReasonErrorKey:tip])
        finishBroadcastWithError(error)
    }
    
    override func processSampleBuffer(_ sampleBuffer: CMSampleBuffer, with sampleBufferType: RPSampleBufferType) {
        switch sampleBufferType {
        case RPSampleBufferType.video:
            // Handle video sample buffer
            TXReplayKitExt.sharedInstance() .sendVideoSampleBuffer(sampleBuffer)
            break
        case RPSampleBufferType.audioApp:
            // Handle audio sample buffer for app audio
            break
        case RPSampleBufferType.audioMic:
            // Handle audio sample buffer for mic audio
            break
        @unknown default:
            // Handle other sample buffer types
            fatalError("Unknown type of sample buffer")
        }
    }
}
:::
</dx-codeblock>

[](id:receive)
#### Step 3. Make the host app wait to receive data
Before screen sharing starts, the host app must be on standby to receive screen recording data from the Broadcast Upload Extension. To achieve this, follow these steps:
1. Make sure that camera capturing is disabled in `TRTCCloud`; if not, call [stopLocalPreview](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/stopLocalPreview.html) to disable it.
2. Call [startScreenCapture](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startScreenCapture.html), passing in the `AppGroup` set in [step 1](#createGroup) to put the SDK on standby.
3. The SDK will then wait for a user to trigger screen sharing. If a "triggering button" is not added as described in [step 4](#launch), users need to press and hold the screen recording button in the iOS Control Center to start screen sharing.

4. You can call [stopScreenCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa8ea0235691fc9cde0a64833249230bb) to stop screen sharing at any time.
<dx-codeblock>
::: dart 
// Start screen sharing. You need to replace `APPGROUP` with the App Group created in the steps above. 
trtcCloud.startScreenCapture(
    TRTCVideoEncParam(
        videoFps: 10,
        videoResolution: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_1280_720,
        videoBitrate: 1600,
        videoResolutionMode: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT,
    ),
    iosAppGroup,
);

// Stop screen sharing
await trtcCloud.stopScreenCapture();


// Event notification for the start of screen sharing, which can be received through `TRTCCloudListener`
onRtcListener(type, param){
    if (type == TRTCCloudListener.onScreenCaptureStarted) {
      // Screen sharing starts.
    }
}
:::
</dx-codeblock>

[](id:launch)
#### Step 4. Add a screen sharing triggering button (optional)
In [step 3](#receive), users need to start screen sharing manually by pressing and holding the screen recording button in the Control Center. To make it possible to start screen sharing by tapping a button in your app as in TRTC Demo Screen, follow these steps:


1. Add the `replay_kit_launcher` plugin to your project.
2. Add a button to your UI and call `ReplayKitLauncher.launchReplayKitBroadcast(iosExtensionName);` in the response function of the button to activate the screen sharing feature.
```
// Customize a response for button tapping.
onShareClick() async {
   if (Platform.isAndroid) {
      if (await SystemAlertWindow.requestPermissions) {
        MeetingTool.showOverlayWindow();
      }
    } else {
      // The screen sharing feature can only be tested on a real device.
      ReplayKitLauncher.launchReplayKitBroadcast(iosExtensionName);
    }
}
```

## Watching Shared Screen
- **Watch screens shared by Android/iOS users**
  When an Android/iOS user starts screen sharing, the screen is shared via the primary stream, and other users in the room will be notified through [onUserVideoAvailable](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud_listener/TRTCCloudListener-class.html) in `TRTCCloudListener`.
  Users who want to watch the shared screen can call the [startRemoteView](https://pub.flutter-io.cn/documentation/tencent_trtc_cloud/latest/trtc_cloud/TRTCCloud/startRemoteView.html) API to start rendering the primary stream of the remote user.

## FAQs
 **Can there be multiple channels of screen sharing streams in a room at the same time?**
Currently, each TRTC room can have only one channel of screen sharing stream.
