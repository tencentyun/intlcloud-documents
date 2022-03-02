## Demo UI
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo app we provide to try out TRTC’s group audio/video call features, including screen sharing, beauty filters, and low-latency video call.




## Solution Strengths
- `TUIRoom` integrates various capabilities such as ultra-low-latency audio/video call, screen sharing, and beauty filter, covering the common features of group audio/video room.
- It can be further developed as needed to quickly implement custom UI and layout, helping you quickly launch your business.
- It encapsulates the basic TRTC and IM SDKs to implement basic logic control and provides APIs for you to call features easily.

## Connection Guide
To quickly implement the group audio/video room feature, you can modify the demo app we provide and adapt it to your needs. You can also use the `Module` module in the app and customize your own UI.

[](id:step1_1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestTUIRoom` and click **Create**.
3. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>?The video conferencing feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/10479). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.

[](id:step1_2)
### Step 2. Download the application source code
Click [TUIRoom](https://github.com/tencentyun/TUIRoom) to clone or download the source code.

[](id:step1_3)
### Step 3. Configure application project files
1. In the **Modify Configuration** step, select your platform.
2. Find and open `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`.
3. Set parameters in `GenerateTestUserSig.java`:
<ul style="margin:0"><li/>SDKAPPID: a placeholder by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: a placeholder by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>? 
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:step1_4)
### Step 4. Run the application
Open the source code project `TUIRoom` with Android Studio (version 3.5 or above) and click **Run**.

[](id:step1_5)
### Step 5. Modify the project source code
The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code. The table below lists the files (folders) and UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|:-------:|:--------|
| remote | The remote user list view |
| widget | Common UI component |
| CreateRoomActivity.java | The audio/video room creation view |
| RoomMainActivity.java | The main view for audio/video room |
| RoomVideoView.java | Include `TXCloudVideoView`, which displays the video data of the local user and remote users |
| MemberEntity.java | User data at the UI layer |
| MemberListAdapter.java | Adapter for the main audio/video room view |

## Tryout
>! You need at least two devices to try out the application.
### Entry page
Select **Create Room** or **Enter Room**.


### Room creation page
When user A creates a room, the room ID will be automatically generated. User A can click **Create Room** to access the main UI.


### Room entry page
User B enters the ID of the room created by user A and click **Join** to access the main UI.


### Main UI (user A)
<img src="https://qcloudimg.tencent-cloud.cn/raw/eebab2b82db719000f0dc376070a25e7.png" width=300px>

### Mic-on list
It displays all users in the current room. If a user enables the camera and mic, you can watch the video image and hear the voice of the user.

### Top toolbar
It implements features such as mic switch, front/rear camera switch, room information display, and room exit.

### Bottom toolbar
It implements features such as local mic/camera control, beauty filter control, user list, and settings.

### Beauty filter
Beauty filters and special effects can be displayed on the screen during live streaming.

### Settings window
Audio and video parameters can be set, and **screen sharing** can be enabled.


### Exiting a room
- **Anchor**: dismisses the room, so all users need to exit the room.
- **Non-anchor**: leaves the room.

## Customizing UI

The `Source` folder in the [source code](https://github.com/tencentyun/TUIRoom) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TUIRoomCore`. You can find the component's APIs in `TUIRoomCore.java` and use them to customize your own UI.
![#600px](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:step2_1)
### Step 1. Integrate the SDK
The group audio/video room component `TUIRoomCore` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project:

- **Method 1: adding dependencies via Maven**
	1. Add the TRTC SDK and IM SDK dependencies to `dependencies`.
```java
dependencies {
	 compile "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
	 compile 'com.tencent.imsdk:imsdk:latest.release'
}
```
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).

	2. In `defaultConfig`, specify the CPU architecture to be used by your application.
```java
defaultConfig {
	ndk {
			abiFilters "armeabi-v7a"
	}
}
```
	3. Click **Sync Now** to automatically download the SDKs and integrate them into your project.
- **Method 2: adding dependencies through local AAR files**
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

[](id:step2_2)
### Step 2. Configure permission requests and obfuscation rules
1. Configure permission requests for your application in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and above, the camera and read storage permissions must be requested at runtime.)
```java
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
2. In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.
```java
-keep class com.tencent.** { *;}
```

[](id:step2_3)
### Step 3. Import the `TUIRoomCore` component
Copy all the files in the directory below to your project:
```java
src/main/java/com/tencent/liteav/tuiroom/model
```

[](id:step2_4)
### Step 4. Create an instance and log in
Call `TUILogin` in `TUICore` to log in as shown below:
```java
TUILogin.init(this, "sdkAppid", null, new V2TIMSDKListener() {

		@Override
		public void onKickedOffline() {

		}

		@Override
		public void onUserSigExpired() {

		}
	});
TUILogin.login("userId", "userSig", new V2TIMCallback() {
	@Override
	public void onError(int code, String msg) {

	}

	@Override
	public void onSuccess() {

	}
});
```

[](id:step2_5)
### Step 5. Set a nickname
After successful login, call `setSelfProfile` to set the user profile.

[](id:step2_6)

### Step 6. Create a room
1. A member calls the `createRoom` API to create a room. After successful room creation, the member enters the rooms (including chat room and TRTC room) as the anchor.
```java
TUIRoomCore tuiRoomCore = TUIRoomCore.getInstance(context);
tuiCore.setListener(listener);
tuiCore.createRoom("roomId", TUIRoomCoreDef.SpeechMode.FREE_SPEECH,
        new TUIRoomCoreCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            // Room created successfully
            } else {
		}
	}
});

```
2. Call the `startCameraPreview` API to start capturing and displaying the local video.
![](https://qcloudimg.tencent-cloud.cn/raw/8c3391905188089fecd17e23477d34ea.png)

[](id:step2_7)
### Step 7. Dismiss the room
- The anchor calls the `destoryRoom` API to dismiss the room and IM group chat and exit the TRTC room.
- Room members receive the `onDestroyRoom` callback message that notifies them of group dismissal and exit the TRTC room.

[](id:step2_8)
### Step 8. Enter a room
1. The room entry process is basically the same as the room creation process. The member needs to call the `enterRoom` API to enter the room.
2. Other members receive the `onRemoteUserEnter` callback that notifies them of room entry by the member.
```java
TUIRoomCore tuiRoomCore = TUIRoomCore.getInstance(context);
tuiCore.setListener(listener);
tuiCore.enterRoom("roomId", new TUIRoomCoreCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            // Entered the room successfully
            } else {
		}
	}
});
```
![](https://qcloudimg.tencent-cloud.cn/raw/ffbda4de381ea198bf808de7d823ab59.png)

[](id:step2_9)
### Step 9. Exit a room
1. The member calls the `leaveRoom` API to exit the IM and TRTC rooms.
2. Other members receive the `onRemoteUserLeave` callback that notifies them of the room exit by the member.

[](id:step2_10)
### Step 10. Enable screen sharing.

1. The screen sharing feature requires the floating window permission, so you need to include the permission requesting logic in your UI.
2. Call `startScreenCapture` of `TUIRoomCore` and pass in encoding parameters and the floating window during screen recording to start screen sharing. For more information, please see [TRTC SDK](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloud__android.html#aa6671fc587513dad7df580556e43be58).
3. Other members in the room will receive the `onRemoteUserScreenVideoAvailable` event notification.

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
        mTUIRoom.stopCameraPreview();
        mTUIRoom.startScreenCapture(encParams, params);
}
:::
</dx-codeblock>
