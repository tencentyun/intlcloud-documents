You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo app we provide to try out TRTC’s group audio/video room features, including screen sharing, beauty filters, and low-latency conferencing.

[](id:DemoUI)
## Using the App’s UI
[](id:ui.step1)
### Step 1. Create an application

1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestMeetingRoom` and click **Create**.
3. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. For IM billing details, see [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

[](id:ui.step2)
### Step 2. Download the application source code

Clone or download the [TRTCFlutterScenesDemo](https://github.com/tencentyun/TRTCFlutterScenesDemo) source code.

[](id:ui.step3)
### Step 3. Configure the application file

1. In the **Modify Configuration** step, select your platform.
2. Find and open `/lib/debug/GenerateTestUserSig.dart`.
3. Set parameters in `GenerateTestUserSig.dart` as follows.
<ul style="margin:0">
    <li>SDKAPPID: It is `PLACEHOLDER` by default. You need to replace it with the real `SDKAppID`.</li>
    <li>SECRETKEY: It is `PLACEHOLDER` by default. You need to replace it with the real key information.</li>
</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4: Compile and Run the Demo

>! An Android project must be run on a real device rather than a simulator.

1. Run `flutter pub get`.
2. Compile, run, and test the project.
<dx-tabs>
::: iOS\s
1. Open `\ios project` in the source code directory with Xcode (11.0 or above).
2. Compile and run the demo project.
:::
::: Android\s
1. Run `flutter run`.
2. Open the demo project with Android Studio (3.5 or above), and click **Run**.
:::

</dx-tabs>

[](id:ui.step5)
### Step 5. Modify the demo source code

The `TRTCMeetingDemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code. The table below lists the files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|-------|--------|
| TRTCMeetingIndex.dart | The view for meeting creation or join |
| TRTCMeetingRoom.dart | The main view for video conferencing |
| TRTCMeetingMemberList.dart | The view for participant list |
| TRTCMeetingSetting.dart | The view for video conferencing parameter settings |

[](id:model)
## Customizing UI

The `TRTCMeetingDemo` folder in the [source code](https://github.com/tencentyun/TRTCFlutterScenesDemo) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCMeeting`. You can find the component's APIs in `TRTCMeeting.dart` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:model.step1)
### Step 1. Integrate the SDK

The interactive live streaming component `RTCMeeting` depends on the [TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud) and [IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin). You can configure `pubspec.yaml` to download their updates automatically.

Add the following dependencies to `pubspec.yaml` of your project.
```
dependencies:
  tencent_trtc_cloud: latest version number
  tencent_im_sdk_plugin: latest version number
```

[](id:model.step2)
### Step 2. Configure permission requests and obfuscation rules

<dx-tabs>
::: iOS\s
Add request for mic permission in `Info.plist`:
```
<key>NSMicrophoneUsageDescription</key>
<string>Audio calls are possible only with mic access.</string>
```
:::
::: Android\s
1. Open `/android/app/src/main/AndroidManifest.xml`.
2. Add `xmlns:tools="http://schemas.android.com/tools"` to `manifest`.
3. Add `tools:replace="android:label"` to `application`.
>? Without the above steps, the [Android Manifest merge failed](https://intl.cloud.tencent.com/document/product/647/39242) error will occur and the compilation will fail.

![Illustration](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
:::
</dx-tabs>

[](id:model.step3)
### Step 3. Import the `TRTCMeeting` component.

Copy all the files in the directory below to your project:
```
lib/TRTCMeetingDemo/model/
```

[](id:model.step4)
### Step 4. Create an instance and log in

1. Call the `sharedInstance` API to create an instance of the `TRTCMeeting` component.
2. Call the `registerListener` function to register event callbacks of the component.
3. Call the `login` API to log in to the component, and set the key parameters as described below.
<table>
    <tr>
        <th>Parameter</th>
        <th>Description</th>
    </tr>
    <tr>
        <td>SDKAppID</td>
        <td>You can view `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
    </tr>
    <tr>
        <td>userId</td>
        <td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend you set it based on your business account system.</td>
    </tr>
    <tr>
        <td>userSig</td>
        <td>Tencent Cloud's proprietary security signature. To obtain one, see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
    </tr>
</table>

<dx-codeblock>
::: dart dart
TRTCMeeting trtcMeeting = TRTCMeeting.sharedInstance();
trtcMeeting.registerListener(onListener);
ActionCallback res = await trtcMeeting.login(
    GenerateTestUserSig.sdkAppId,
    userId,
    GenerateTestUserSig.genTestSig(userId),
);
if (res.code == 0) {
    // Login succeeded
}
:::
</dx-codeblock>

[](id:model.step5)
### Step 5. Create a meeting as an anchor

1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your username and profile photo as an anchor.
2. Call `createMeeting` to create a meeting room.
3. Call `startCameraPreview` to capture video and `artMicrophone` to capture audio.
4. To use beauty filters, you can add beauty filter buttons to the UI and set beauty filters through `getBeautyManager`.
>?Only the Enterprise Edition SDK supports face changing and stickers.

![](https://main.qcloudimg.com/raw/7d55d4983e6fe8da04e63babe5ab3822.png)

<dx-codeblock>
::: dart dart
// 1. The anchor sets his or her nickname and profile photo.
trtcMeeting.setSelfProfile('my_name', 'my_avatar');

// 2. The anchor creates a meeting.
ActionCallback res = await trtcMeeting.createMeeting(roomId);
if (res.code == 0) {
    // Created the meeting successfully
    // 3. The anchor turns the camera on and enables audio capturing.
    trtcMeeting.startCameraPreview(true, TRTCCloudVideoViewId);
    trtcMeeting.startMicrophone();
    // 4. Set the beauty filter.
    trtcMeeting.getBeautyManager().setBeautyStyle(TRTCCloudDef.TRTC_BEAUTY_STYLE_PITU);
    trtcMeeting.getBeautyManager().setBeautyLevel(6);
}
:::
</dx-codeblock>

[](id:model.step6)
### Step 6. Join a meeting as a participant

1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your username and profile photo as a participant.
2. Call `enterMeeting`, passing in the meeting room ID to enter the room.
3. Call `startCameraPreview` to capture video and `startMicrophone` to capture audio.
4. If another participant turns the camera on, you will receive the `onUserVideoAvailable` notification, and can call `startRemoteView` and pass in the `userId` to play the participant’s video.

![](https://main.qcloudimg.com/raw/ce4bc9c134a94709c3f8e1768c65be88.png)

<dx-codeblock>
::: dart dart
// 1. Set your username and profile photo as a participant
trtcMeeting.setSelfProfile('my_name', 'my_avatar');

// 2. The participant calls `enterMeeting` to enter the meeting room.
ActionCallback res = await trtcMeeting.enterMeeting(roomId);
if (res.code == 0) {
    // Joined the meeting successfully.
    // 3. The anchor turns the camera on and enables audio capturing.
    trtcMeeting.startCameraPreview(true, TRTCCloudVideoViewId);
    trtcMeeting.startMicrophone();
    // 4. Set the beauty filter.
    trtcMeeting.getBeautyManager().setBeautyStyle(TRTCCloudDef.TRTC_BEAUTY_STYLE_PITU);
    trtcMeeting.getBeautyManager().setBeautyLevel(6);
}

// 5. The participant receives the notification that another member enables the camera and starts playback
trtcMeeting.registerListener(onListener);
onListener(TRTCMeetingDelegate type, param) {
    switch (type) {
        case TRTCMeetingDelegate.onUserVideoAvailable:
            if (param['available']) {
                trtcMeeting.startCameraPreview(
                    param['userId'],
                    TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG,
                    TRTCCloudVideoViewId
                );
            } else {
                trtcMeeting.stopRemoteView(
                    param['userId'],
                    TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG
                );
            }
            break;
    }
}
:::
</dx-codeblock>

[](id:model.step7)
### Step 7. Share the screen

1. The screen sharing feature requires the floating window permission, so you need to include the permission requesting logic in your UI.
2. Call `startScreenCapture`, passing in encoding parameters and the floating window during screen recording to start screen sharing. For more information, see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58).
3. Other participants in the meeting will receive the `onUserVideoAvailable` event notification.

>!Screen sharing and camera capturing are mutually exclusive. Before enabling screen sharing, you need to call `stopCameraPreview` to disable camera capturing. For more information, see [TRTC SDK](https://intl.cloud.tencent.com/document/product/647/39859).

<dx-codeblock>
::: dart dart
await trtcMeeting.stopCameraPreview();
trtcMeeting.startScreenCapture(
    videoFps: 10,
    videoBitrate: 1600,
    videoResolution: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_1280_720,
    videoResolutionMode: TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT,
    appGroup: iosAppGroup,
);
:::
</dx-codeblock>

[](id:model.step8)
### Step 8. Implement text chat and muting notifications

- Call `sendRoomTextMsg` to send text messages. All participants in the meeting will receive the `onRecvRoomTextMsg` callback. IM has its default content moderation rules. Text messages that contain restricted terms will not be forwarded by the cloud.
<dx-codeblock>
::: dart dart
// Sender: send text messages
trtcMeeting.sendRoomTextMsg('Hello Word!');
// Recipient: listen for text messages
trtcMeeting.registerListener(onListener);
onListener(TRTCMeetingDelegate type, param) {
    switch (type) {
        case TRTCMeetingDelegate.onRecvRoomTextMsg:
            print('Received a message from' + param['userName'] + ':' + param['message']);
            break;
    }
}
:::
</dx-codeblock>

- Call `sendRoomCustomMsg` to send custom (signaling) messages, and all participants in the meeting will receive the `onRecvRoomCustomMsg` callback. Custom messages are often used to transfer custom signals, such as muting notifications and notifications about other meeting controls.
<dx-codeblock>
::: dart dart
// Sender: customize CMD to distinguish a muting notification
// E.g., use "CMD_MUTE_AUDIO" to indicate muting notifications
trtcMeeting.sendRoomCustomMsg('CMD_MUTE_AUDIO', '1');
// Recipient: listen for custom messages
trtcMeeting.registerListener(onListener);
onListener(TRTCMeetingDelegate type, param) {
    switch (type) {
        case TRTCMeetingDelegate.onRecvRoomCustomMsg:
            if (param['command'] == 'CMD_MUTE_AUDIO') {
                // Receive a muting notification.
                print('Received a muting notification from' + param['userName'] + ':' + param['message']);
                trtcMeeting.muteLocalAudio(message == '1');
            }
            break;
    }
}
:::
</dx-codeblock>
