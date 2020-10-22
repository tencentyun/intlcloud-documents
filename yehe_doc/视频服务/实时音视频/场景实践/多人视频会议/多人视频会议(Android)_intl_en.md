## Effect Demo
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo to try out the video conferencing capabilities of TRTC, such as screen sharing, beauty filters, and low-latency conferencing.

To quickly implement the video conferencing feature, you can directly modify the demo provided by TRTC for adaptation or use the provided `TRTCMeeting` component and implement custom UI.

<span id="DemoUI"> </span>
## Reusing Demo UI
<span id="ui.step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter the application name such as `TestMeetingRoom`, and click **Create Application**.

>?This feature uses two basic PaaS services, namely, [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When TRTC is activated, IM will be activated automatically.IM is a value-added service at the prices as detailed in [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

<span id="ui.step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Android)** to enter GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_Android_latest.zip)**), and download the relevant SDK and supporting demo source code.
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

<span id="ui.step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#ui.step2).
2. Find and open the `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` file.
3. Set the relevant parameters in the `GenerateTestUserSig.java` file:
  <ul><li>SDKAPPID: it is 0 by default. Please replace it with your real `SDKAppID`.</li>
  <li>SECRETKEY: it is an empty string by default. Please replace it with your real key information.</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage the application.

>!The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Server-Side UserSig Generation](https://intl.cloud.tencent.com/document/product/647/35166).

<span id="ui.step4"></span>
### Step 4. Run the demo
Use Android Studio (v3.5 or above) to open the `TRTCScenesDemo` project and click **Run** to start debugging the demo.

<span id="ui.step5"></span>
### Step 5. Modify the demo source code
The `trtcmeetingdemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code. The following table lists the files or folders and the corresponding UIs for easy adjustment:

| File or Folder | Feature Description |
|:-------:|:--------|
| remote | Remote user list UI |
| widget | Common UI component |
| CreateMeetingActivity.java | UI for meeting creation |
| MeetingMainActivity.java | Main UI of video conferencing |
| MeetingVideoView.java | `TXCloudVideoView` with TRTC encapsulated, which is used to display local and remote user video data |
| MemberEntity.java | User data at the UI layer |
| MemberListAdapter.java | Adapter of the main UI of video conferencing |

<span id="model"> </span>
## Implementing Custom UI

The `trtcmeetingdemo` folder in the [source code](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo/trtcmeetingdemo/src/main/java/com/tencent/liteav/meeting) contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCMeeting`. You can find the API functions provided by this component in the `TRTCMeeting.java` file and use the corresponding API to implement your own custom UI.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

<span id="model.step1"> </span>
### Step 1. Integrate SDKs
The video conferencing component `TRTCMeeting` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project in the following steps:

**Method 1. Implement dependency through Maven repository**
1. Add the TRTC SDK and IM SDK dependencies to `dependencies`.
```
dependencies {
       compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       compile 'com.tencent.imsdk:imsdk:latest.release'
}
```
>?You can get the latest version numbers of the two SDKs on the [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK) homepages on GitHub.
>
2. In `defaultConfig`, specify the CPU architecture to be used by the application.
```
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
```
3. Click **Sync Now** to automatically download the SDK and integrate it into the project.

**Method 2. Implement dependency through local AAR files**
If the access to the Maven repository is slow in your development environment, you can download the ZIP packages and manually integrate the SDKs into your project as instructed in the integration document.
<table>
<tr>
<th>SDK</th>
<th>Download Page</th>
<th>Integration Guide</th>
</tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">Integration document</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">Integration document</a></td>
</tr>
</table>

<span id="model.step2"> </span>
### Step 2. Configure permissions and obfuscation rules
Configure application permissions in `AndroidManifest.xml`. The SDK requires the following permissions (on Android 6.0 and above, the camera and storage read permissions need to be requested dynamically):
```
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
<uses-feature android:name="android.hardware.camera"/>
<uses-feature android:name="android.hardware.camera.autofocus" />
```

In the `proguard-rules.pro` file, add the classes related to the SDK to the "do not obfuscate" list:
```
-keep class com.tencent.** { *; }
```

<span id="model.step3"> </span>
### Step 3. Import the TRTCMeeting component
Copy all files in the following directory to your project:
```
src/main/java/com/tencent/liteav/meeting/model
```

<span id="model.step4"> </span>
### Step 4. Create and log in to the component
1. Call the `sharedInstance` API to create an instance object of the `TRTCMeeting` component.
2. Call the `setDelegate` function to register the event notification of the component.
3. Call the `login` function to log in to the component. Enter key parameters as shown below:
 <table>
<tr>
<th>Parameter Name</th>
<th>Description</th>
</tr>
<tr>
<td>sdkAppId</td>
<td>You can view the `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC Console</a>.</td>
</tr>
<tr>
<td>userId</td>
<td>ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (_).</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">How to Calculate UserSig</a>.</td>
</tr>
<tr>
<td>callback</td>
<td>Login callback. The `code` will be 0 if login is successful.</td>
</tr>
</table>
<pre>
TRTCMeeting trtcMeeting = TRTCMeeting.sharedInstance(this);
trtcMeeting.login(SDKAPPID, userId, userSig, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // Logged in successfully
        }
    }
});
</pre>

<span id="model.step5"> </span>
### Step 5. Create a meeting
1. The chairperson can call `setSelfProfile` to set the nickname and profile photo after logging in by performing [step 4](#model.step4).
2. The chairperson can call `setDelegate` to make an event call of `createMeeting` to create a meeting room.
3. The chairperson can call `startCameraPreview` to capture video image or call `startMicrophone` to capture sound.
4. If the chairperson requires beauty filters, the beauty filter adjusting buttons can be configured on the UI for setting beauty filters through `getBeautyManager`.
>?Face changing and sticker pendant features are not supported for SDKs in editions other than the Enterprise Edition.
>
![](https://main.qcloudimg.com/raw/416a1afd87b196a6ef791bf63eeaa5e0.png)

```java
// 1. The chairperson sets the nickname and profile photo
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2. The chairperson creates a room
trtcMeeting.createMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. Enable camera and audio capture
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startCameraPreview(true, txCloudVideoView);
            trtcMeeting.startMicrophone();
            // 4. Set the beauty filter
            trtcMeeting.getBeautyManager().setBeautyStyle(1);
            trtcMeeting.getBeautyManager().setBeautyLevel(6);
        }
    }
});
```

<span id="model.step6"> </span>
### Step 6. The participant joins the meeting
1. The participant can call `setSelfProfile` to set the nickname and profile photo after logging in by performing [step 4](#model.step4).
2. The participant can call `enterMeeting` and pass in the meeting room number to enter the meeting room.
3. The participant can call `startCameraPreview` to capture video image and call `startMicrophone` to capture sound.
4. If another participant enables the camera, the participant will receive the `onUserVideoAvailable` event. At this time, the participant can call `startRemoteView` and pass in the `userId` to start playback.

![](https://main.qcloudimg.com/raw/f33213dea7a32ca9904c066952fcc535.png)

```java
// 1. The participant sets the nickname and profile photo
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2. The participant calls `enterMeeting` to enter the meeting room
trtcMeeting.enterMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. The participant successfully enters the room and can enable local camera and mic and the beauty filter feature
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startCameraPreview(true, txCloudVideoView);
            trtcMeeting.startMicrophone();
            trtcMeeting.getBeautyManager().setBeautyStyle(1);
            trtcMeeting.getBeautyManager().setBeautyLevel(6);
        }
    }
});

// 4. The participant receives the notification that another member enables the camera and starts playback
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onUserVideoAvailable(String userId, boolean available) {
        if (available) {
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startRemoteView(userId, txCloudVideoView);
        } else {
            trtcMeeting.stopRemoteView(userId, null);
        }
    }
});
```

<span id="model.step7"> </span>
### Step 7. Share the screen

1. The screen sharing feature needs to apply for the floating window permission from the system, so you need to implement specific logic in the UI.
2. Call `startScreenCapture`, pass in the encoding parameters and the floating window in the screen sharing process to implement the screen sharing feature. For more information, please see [TRTC SDK](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58).
3. Other participants in the meeting will receive the `onUserVideoAvailable` event notification.
>!Screen sharing and camera capture are mutually exclusive. If you need to enable screen sharing, please call `stopCameraPreview` to disable camera capture first.

```java
// 1. Add the activity and permission of the SDK's screen sharing feature in the `AndroidManifest.xml` file
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<application>
    <activity
        android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity"
        android:theme="@android:style/Theme.Translucent" />
</application>
// 2. Apply for the floating window permission in your UI
if (Build.VERSION.SDK_INT >= 23) {
    if (!Settings.canDrawOverlays(getApplicationContext())) {
        Intent intent = new Intent(Settings.ACTION_MANAGE_OVERLAY_PERMISSION, Uri.parse("package:" + getPackageName()));
        startActivityForResult(intent, 100);
    } else {
        startScreenCapture();
    }
} else {
    startScreenCapture();
}

// 3. System callback result
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    if (requestCode == 100) {
        if (Build.VERSION.SDK_INT >= 23) {
            if (Settings.canDrawOverlays(this)) {
                // Authorized user successfully
                startScreenCapture();
            } else {
            }
        }
    }
}
// 4. Enable screen sharing
private void startScreenCapture() {
        TRTCCloudDef.TRTCVideoEncParam encParams = new TRTCCloudDef.TRTCVideoEncParam();
        encParams.videoResolution = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_1280_720;
        encParams.videoResolutionMode = TRTCCloudDef.TRTC_VIDEO_RESOLUTION_MODE_PORTRAIT;
        encParams.videoFps = 10;
        encParams.enableAdjustRes = false;
        encParams.videoBitrate = 1200;

        TRTCCloudDef.TRTCScreenShareParams params = new TRTCCloudDef.TRTCScreenShareParams();
        mTRTCMeeting.stopCameraPreview();
        mTRTCMeeting.startScreenCapture(encParams, params);
}
```

<span id="model.step8"> </span>
### Step 8. Implement text chat and messaging mute
- `sendRoomTextMsg` can be used to send general text messages, and all anchors and viewers in the room can receive the `onRecvRoomTextMsg` callback.
 The backend of IM has default sensitive word filtering rules, and text messages that are considered to contain any sensitive words will not be forwarded by the cloud.
```java
// Sender: sends text messages
trtcMeeting.sendRoomTextMsg("Hello Word!", null);
// Receiver: listens on text messages
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomTextMsg(
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        Log.d(TAG, "A message from" + userInfo.userName + "is received:" + message);
    }
});
```
- `sendRoomCustomMsg` can be used to send custom (signaling) messages, and all chairpersons and participants in the room can receive the `onRecvRoomCustomMsg` callback.
Custom messages are often used to transfer custom signals, such as meeting controls like mute.
```java
// Sender: mute notifications can be identified by custom `CMD`
// eg:"CMD_MUTE_AUDIO" indicates a mute notification
trtcMeeting.sendRoomCustomMsg("CMD_MUTE_AUDIO", "1", null);
// Receiver: listens on custom messages
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, 
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        if ("CMD_MUTE_AUDIO".equals(cmd)) {
            // Receive the mute notification
            Log.d(TAG, "A mute notification from" + userInfo.userName + "is received:" + message);
            trtcMeeting.muteLocalAudio("1".equals(message));
        }
    }
});
```
