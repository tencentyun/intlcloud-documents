## Demo UI
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo app we provide to try out TRTC’s video conferencing features, including screen sharing, beauty filters, and low-latency conferencing.


To quickly enable the video conferencing feature, you can modify the demo app we provide and adapt it to your needs. You can also use the `TRTCMeeting` component and customize your own UI.

[](id:DemoUI)

## Using the App’s UI
[](id:ui.step1)
### Step 1. Create an application
1. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g., `TestMeetingRoom`, and click **Create**.
3. Click **Next** to skip this step.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!  This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.

[](id:ui.step2)
### Step 2. Download the application source code
Clone or download the [TUIMeeting](https://github.com/tencentyun/TUIMeeting) source code.

[](id:ui.step3)
### Step 3. Configure the application file
1. In the **Modify Configuration** step, select your platform.
2. Find and open `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`.
3. Set parameters in `GenerateTestUserSig.java`:
<ul style="margin:0"><li/>SDKAPPID: a placeholder by default. Set it to the actual `SDKAppID`.
<li>SECRETKEY: a placeholder by default. Set it to the actual key.</ul>
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.


>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the application
Open the source code project `TUIMeeting` with Android Studio (version 3.5 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the app’s source code
The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code. The table below lists the files (folders) and UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|:-------:|:--------|
| remote | The remote user list view |
| widget | Common UI component |
| CreateMeetingActivity.java | The meeting creation view |
| MeetingMainActivity.java | The main view for video conferencing |
| MeetingVideoView.java | Include `TXCloudVideoView`, which displays the video data of the local user and remote users |
| MemberEntity.java | User data at the UI layer |
| MemberListAdapter.java | Adapter for the main video conferencing view |



## Tryout

> ! You need at least two devices to try out the application.

### User A
1. Enter a username (**which must be unique**) and log in.
2. Enter the conference ID and tap **Join**.
3. Enter a room topic and tap **Chat**.

### User B
1. Enter a username (**which must be unique**) and log in.
2. Enter the meeting ID created by user A and click **Join Meeting**. <br>

[](id:model)
## Customizing UI

The `Source` folder in the [source code](https://github.com/tencentyun/TUIMeeting/tree/master/Android/Source/src/main/java/com/tencent/liteav/meeting) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCMeeting`. You can find the component's APIs in `TRTCMeeting.java` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:model.step1)
### Step 1. Integrate the SDKs
The video conferencing component `TRTCMeeting` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project.

**Method 1: adding dependencies via Maven**
1. Add the TRTC SDK and IM SDK dependencies to `dependencies`.
<dx-codeblock>
::: java java
dependencies {
       compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       compile 'com.tencent.imsdk:imsdk:latest.release'
}
:::
</dx-codeblock>
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).
2. In `defaultConfig`, specify the CPU architecture to be used by your application.
<dx-codeblock>
::: java java
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
:::
</dx-codeblock>
3. Click **Sync Now** to automatically download the SDKs and integrate them into your project.

**Method 2: adding dependencies through local AAR files**
If your access to the Maven repository is slow, you can download the ZIP files of the SDKs and manually integrate them into your project as instructed in the documents below.
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

[](id:model.step2)
### Step 2. Configure permission requests and obfuscation rules
Configure permission requests for your application in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and above, the camera and read storage permissions must be requested at runtime.)
<dx-codeblock>
::: java java
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
:::
</dx-codeblock>

In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.
<dx-codeblock>
::: java java
-keep class com.tencent.** { *;}
:::
</dx-codeblock>

[](id:model.step3)
### Step 3. Import the `TRTCMeeting` component.
Copy all the files in the directory below to your project:
<dx-codeblock>
::: java java
src/main/java/com/tencent/liteav/meeting/model
:::
</dx-codeblock>

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` API to create an instance of the `TRTCMeeting` component.
2. Call the `setDelegate` API to register event callbacks of the component.
3. Call the `login` API to log in to the component, and set the key parameters as described below.
<table>
<tr><th>Parameter</th><th>Description</th></tr><tr>
<td>SDKAppID</td>
<td>You can view `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend you set it based on your business account system.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. To obtain one, see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr><tr>
<td>callback</td>
<td>Login callback. The code is `0` if login is successful.</td>
</tr>
</table>
<dx-codeblock>
::: java java
TRTCMeeting trtcMeeting = TRTCMeeting.sharedInstance(this);
trtcMeeting.login(SDKAPPID, userId, userSig, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // Logged in
        }
    }
});
:::
</dx-codeblock>

[](id:model.step5)
### Step 5. Create a conference as an anchor
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your username and profile photo as an anchor.
2. Call `setDelegate` and then `createMeeting` to create a conference room.
3. Call `startCameraPreview` to capture video and `startMicrophone` to capture audio.
4. To use beauty filters, you can add beauty filter buttons to the UI and set beauty filters through `getBeautyManager`.
>?Only the Enterprise Edition SDK supports face changing and stickers.

![](https://main.qcloudimg.com/raw/7d55d4983e6fe8da04e63babe5ab3822.png)


<dx-codeblock>
::: java java
// 1. The host sets his or her nickname and profile photo.
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2. The host creates a room.
trtcMeeting.createMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. The host turns on the camera and enables audio capturing.
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startCameraPreview(true, txCloudVideoView);
            trtcMeeting.startMicrophone();
            // 4. The host sets beauty filters.
            trtcMeeting.getBeautyManager().setBeautyStyle(1);
            trtcMeeting.getBeautyManager().setBeautyLevel(6);
        }
    }
});
:::
</dx-codeblock>

[](id:model.step6)
### Step 6. Join a conference as a participant
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your username and profile photo as a participant.
2. Call `enterMeeting`, passing in the conference room ID to enter the room.
3. Call `startCameraPreview` to capture video and `startMicrophone` to capture audio.
4. If another attendee turns the camera on, you will receive the `onUserVideoAvailable` notification, and can call `startRemoteView` and pass in the `userId` to play the attendee’s video.

![](https://main.qcloudimg.com/raw/ce4bc9c134a94709c3f8e1768c65be88.png)

<dx-codeblock>
::: java java
// 1. Set your username and profile photo as a participant
trtcMeeting.setSelfProfile("my_name", "my_avatar", null);

// 2. The attendee calls `enterMeeting` to enter the meeting room.
trtcMeeting.enterMeeting(roomId, new TRTCMeetingCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. After entering the room, the attendee turns on the mic and camera, or enables beauty filters as well.
            TXCloudVideoView txCloudVideoView = new TXCloudVideoView(TestMeetingActivity.this);
            parentView.add(view);
            trtcMeeting.startCameraPreview(true, txCloudVideoView);
            trtcMeeting.startMicrophone();
            trtcMeeting.getBeautyManager().setBeautyStyle(1);
            trtcMeeting.getBeautyManager().setBeautyLevel(6);
        }
    }
});

// 3. The attendee receives a notification that another attendee has turned on the camera and starts playing the attendee’s video.
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
:::
</dx-codeblock>

[](id:model.step7)
### Step 7. Share the screen

1. The screen sharing feature requires the floating window permission, so you need to include the permission requesting logic in your UI.
2. Call `startScreenCapture`, passing in encoding parameters and the floating window during screen recording to start screen sharing. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58).
3. Other participants in the meeting will receive the `onUserVideoAvailable` event notification.

>!Screen sharing and camera capturing are mutually exclusive. Before enabling screen sharing, you need to call `stopCameraPreview` to disable camera capturing.

<dx-codeblock>
::: java java
// 1. Add the SDK’s screen sharing activity and permission in `AndroidManifest.xml`.
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />
<application>
    <activity
        android:name="com.tencent.rtmp.video.TXScreenCapture$TXScreenCaptureAssistantActivity"
        android:theme="@android:style/Theme.Translucent" />
</application>
:::
</dx-codeblock>
<dx-codeblock>
::: java java
// 2. Request the floating window permission in your UI.
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
                // The user grant the permission.
                startScreenCapture();
            } else {
            }
        }
    }
}

// 4. Enable screen sharing.
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
:::
</dx-codeblock>

[](id:model.step8)
### Step 8. Implement text chat and muting notifications
- Call `sendRoomTextMsg` to send a common text message. All users in the room will receive an `onRecvRoomTextMsg` callback.
 IM has its default content moderation rules. Text messages that contain restricted terms will not be forwarded by the cloud.
 <dx-codeblock>
 ::: java java
 // Sender: send text messages
 trtcMeeting.sendRoomTextMsg("Hello Word!", null);
 // Recipient: listen for text messages
 trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomTextMsg(
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        Log.d(TAG, "Received a message from" + userInfo.userName + ": " + message);
    }
 });
 :::
 </dx-codeblock>
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All users in the room will receive the `onRecvRoomCustomMsg` callback.
Custom messages are often used to transfer custom signals, such as muting notifications and notifications about other meeting controls.
<dx-codeblock>
::: java java
// Sender: customize CMD to distinguish a muting notification
// E.g., use "CMD_MUTE_AUDIO" to indicate muting notifications
trtcMeeting.sendRoomCustomMsg("CMD_MUTE_AUDIO", "1", null);
// Recipient: listen for custom messages
trtcMeeting.setDelegate(new TRTCMeetingDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, 
		    String message, TRTCMeetingDef.UserInfo userInfo) {
        if ("CMD_MUTE_AUDIO".equals(cmd)) {
            // Receive a muting notification.
            Log.d(TAG, "Received a muting notification from" + userInfo.userName + ":" + message);
            trtcMeeting.muteLocalAudio("1".equals(message));
        }
    }
});
:::
</dx-codeblock>
