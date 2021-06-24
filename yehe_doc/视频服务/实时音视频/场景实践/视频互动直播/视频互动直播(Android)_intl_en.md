## Demonstration
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC’s interactive live streaming features, including co-anchoring, anchor competition, low-latency watch, and on-screen comments.


To quickly enable the interactive live video streaming feature, you can modify the demo we provide and adapt it to your needs. You can also use the `TRTCLiveRoom` component and customize your own UI.

[](id:DemoUI)
## Using the Demo UI

[](id:ui.step1)
### Step 1. Create an application.
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g. `TestLiveRoom`, and click **Create**.

>!The interactive live streaming feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047).
When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.


[](id:ui.step2)
### Step 2. Download the SDK and demo source code.
1. Download the SDK and demo source code for your platform.
2. Click **Next**.

[](id:ui.step3)
### Step 3. Configure demo project files.
1. In the **Modify Configuration** step, select the platform in line with the source package downloaded.
2. Find and open the `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` file.
3. Set parameters in `GenerateTestUserSig.java` as follows.
<ul style="margin:0"><li/>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the demo.
Open the `TRTCScenesDemo` project with Android Studio (version 3.5 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the demo source code.
The `trtcliveroomdemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code. The table below lists the files (folders) and UI views they represent. You can refer to it when making UI changes.

| File or Folder | Use |
|:-------:|:--------|
| anchor | Implementation code for anchor-end views |
| audience | Implementation code for viewer-end views |
| common | Implementation code for common UI components |
| liveroomlist | Implementation code for the room list view |
| widget | Common controls |

[](id:model)
## Implementing A Custom UI

The `trtcliveroomdemo` folder in the [source code] contains two subfolders: `ui` and `model`. In the `model` subfolder is the reusable open-source component `TRTCLiveRoom`. You can find the component’s APIs in `TRTCLiveRoom.java` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/710358e4e170d44304cdb9bc991ad209.jpg)

[](id:model.step1)
### Step 1. Integrate the SDKs.
The `TRTCLiveRoom` component depends on the TRTC SDK and IM SDK. Follow the steps below to integrate them into your project.

**Method 1: adding dependencies via Maven**
1. Add the TRTC SDK and IM SDK dependencies to `dependencies`.
```
dependencies {
       complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       complie 'com.tencent.imsdk:imsdk:latest.release'
}
```
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).
>
2. In `defaultConfig`, specify the CPU architecture to be used by the app.
```
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
```
3. Click **Sync Now** to have the SDKs downloaded and integrated into your project automatically.

**Method 2: adding dependencies through local AAR files**
If your access to the Maven repository is slow, you can download the ZIP packages of the SDKs and manually and integrate them into your project as instructed in the documents below.
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
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">Integration Document</a></td>
</tr>
</table>

[](id:model.step2)
### Step 2. Configure permission requests and obfuscation rules.
Configure permission requests for your app in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and above, the camera and read storage permissions must be requested at runtime.)
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

In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.
```
-keep class com.tencent.** { *; }
```

[](id:model.step3)
### Step 3. Import the `TRTCLiveRoom` component.
Copy all the files in the following directory to your project:
```
src/main/java/com/tencent/liteav/liveroom/model
```

<span id="model.step4"></span>
### Step 4. Create a component instance and log in.
1. Call the `sharedInstance` API to create an instance of the `TRTCLiveRoom` component.
2. Create a `TRTCLiveRoomConfig` object, and set its `useCDNFirst` and `CDNPlayDomain` attributes.
 - `useCDNFirst`: specifies the way viewers watch live streams. `true` means that viewers watch live streams over CDNs, which is cost-efficient but has high latency. `false` means that viewers watch live streams under the low latency mode, the cost of which is between that of CDN live streaming and co-anchoring, but the latency is lower than 1 second.
 - `CDNPlayDomain`: specifies the domain name for CDN live streaming, which takes effect only if `useCDNFirst` is set to `true`. You can set it in CSS console > **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**.
3. Call the `login` function to log in to the component, and set the key parameters as described below.
 <table>
<tr>
<th>Parameter</th>
<th>Note</th>
</tr>
<tr>
<td>SDKAPPID</td>
<td>You can view the `SDKAPPID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr>
<tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_).</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. To obtain one, see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr>
<tr>
<td>config</td>
<td>Global configuration information. Please initialize it during login as it cannot be modified after login.<ul style="margin:0;">
<li>`useCDNFirst`: specifies the way viewers watch live streams. `true` means that viewers watch live streams over CDNs, which is cost-efficient but has high latency. `false` means that viewers watch live streams under the low latency mode, the cost of which is between that of CDN live streaming and co-anchoring, but the latency is lower than 1 second.</li>
<li>`CDNPlayDomain`: specifies the domain name for CDN live streaming, which takes effect only if `useCDNFirst` is set to `true`. You can set it in CSS console > **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>**.</li>
</ul></td>
</tr>
<tr>
<td>callback</td>
<td>Login callback. The code is 0 if login is successful.</td>
</tr>
</table>

```
TRTCLiveRoom mLiveRoom = TRTCLiveRoom.sharedInstance(this);
// useCDNFirst: `true` means that viewers watch live streams over CDNs, and `false` means that viewers watch live streams under the low latency mode.
// yourCDNPlayDomain: the playback domain name for CDN live streaming
TRTCLiveRoomDef.TRTCLiveRoomConfig config = 
    new TRTCLiveRoomDef.TRTCLiveRoomConfig(useCDNFirst, yourCDNPlayDomain);
mLiveRoom.login(SDKAPPID, userId, userSig, config, 
    new TRTCLiveRoomCallback.ActionCallback() {
            @Override
            public void onCallback(int code, String msg) {
                if (code == 0) {
                    //Login successful
                }
            }
});
```

[](id:model.step5)
### Step 5. Start streaming as an anchor.
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo as an anchor.
2. Before streaming, you can call `startCameraPreview` to enable camera preview, add beauty filter buttons to the UI, and set beauty filters through `getBeautyManager`.
 >?Only the Enterprise Edition SDK supports face changing and stickers.
 >
3. After setting beauty filters, call `createRoom` to create a live streaming room.
4. Call `startPublish` to start streaming. To enable CDN live streaming, specify `useCDNFirst` and `CDNPlayDomain` in the `TRTCLiveRoomConfig` parameter passed in during login and specify the `streamID` for playback when calling `startPublish`.

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

```
// 1. The anchor sets his or her nickname and profile photo.
mLiveRoom.setSelfProfile("A", "your_face_url", null);

// 2. The anchor enables camera preview and sets beauty filters before streaming.
TXCloudVideoView view = new TXCloudVideoView(context);
parentView.add(view);
mLiveRoom.startCameraPreview(true, view, null);
mLiveRoom.getBeautyManager().setBeautyStyle(1);
mLiveRoom.getBeautyManager().setBeautyLevel(6);

// 3. The anchor creates a room.
TRTCLiveRoomDef.TRTCCreateRoomParam param = new TRTCLiveRoomDef.TRTCCreateRoomParam();
param.roomName = "Test room";
mLiveRoom.createRoom(123456789, param, new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4. The anchor starts streaming and publishes the streams to CDNs.
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});
```

[](id:model.step6)
### Step 6. Play as a viewer.
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo as a viewer.
2. Gets the latest room list from the backend.
 >?The room list in the demo is for demonstration only. The business logic of live streaming room lists vary significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
 >
3. Call `getRoomInfos` to get short descriptions of the rooms, which are provided by anchors when they call `createRoom` to create the rooms.
 >!If your room list already displays enough information, you can skip the step of calling `getRoomInfos`.
4. Select a room, call `enterRoom`, and pass in the room ID to enter the room.
5. Call `startPlay` and pass in the `userId` of the anchor to start playback.
 - If the room list displays the `userId` of the anchor, you can call `startPlay` and pass in the anchor’s `userId` to start playback.
 - If you do not know the anchor's `userId`, you can find it in the `onAnchorEnter` event callback, which you will receive after entering the room. You can then call `startPlay` to start playback. 

![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

```
// 1. Get the room list from the backend. Suppose it is `roomList`.
List<Integer> roomList = GetRoomList();

// 2. Call `getRoomInfos` to get the details of the room
mLiveRoom.getRoomInfos(roomList, new TRTCLiveRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCLiveRoomDef.TRTCLiveRoomInfo> list) {
        if (code == 0) {
            // After getting the room information, you can display on the anchor list page the anchor's nickname, profile photo, and other information.
        }
    }
})

// 3. Select a `roomid` and enter the room.
mLiveRoom.enterRoom(roomid, null);

// 4. After receiving the notification about the anchor’s entry, start playback.
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {  
        // 5. Play the anchor's video image.
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

[](id:model.step7)
### Step 7. Co-anchor as a viewer.
1. A viewer calls `requestJoinAnchor` to send a co-anchoring request to the anchor.
2. The anchor receives a notification (`TRTCLiveRoomDelegate#onRequestJoinAnchor`) that a viewer requested to co-anchor.
3. The anchor calls `responseJoinAnchor` to accept or decline the co-anchoring request.
4. The viewer receives the `TRTCLiveRoomDelegate#responseCallback` event notification, which carries the anchor’s response.
5. If the anchor accepts the co-anchoring request, the viewer can call `startCameraPreview` to turn on the local camera and then `startPublish` to push streams.
6. The anchor receives a notification (`TRTCLiveRoomDelegate#onAnchorEnter`) that a new stream from a viewer is available. The notification specifies the viewer’s `userId`.
7. The anchor calls `startPlay` to play the viewer's video image.

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)

```
// 1. The viewer sends a co-anchoring request.
mLiveRoom.requestJoinAnchor(mSelfUserId + "requested to co-anchor", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4. The anchor accepts the viewer's request.
            TXCloudVideoView view = new TXCloudVideoView(context);
            parentView.add(view);
            // 5. The viewer turns on the camera and starts pushing streams.
            mLiveRoom.startCameraPreview(true, view, null);
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});

// 2. The anchor receives the co-anchoring request.
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestJoinAnchor(final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, 
        String reason, final int timeout) {
        // 3. The anchor accepts the co-anchoring request.
        mLiveRoom.responseJoinAnchor(userInfo.userId, true, "agreed to co-anchor");
    }

    @Override
    public void onAnchorEnter(final String userId) {
        // 6. The anchor receives a notification that the co-anchoring viewer has turned on the mic.
        TXCloudVideoView view = new TXCloudVideoView(context);
        parentView.add(view);
        // 7. The anchor plays the viewer's video image.
        mLiveRoom.startPlay(userId, view, null);
    }
});
```

[](id:model.step8)
### Step 8. Anchors compete with each other.
1. Anchor A calls `requestRoomPK` to send a competition request to anchor B.
2. Anchor B receives the `TRTCLiveRoomDelegate onRequestRoomPK` notification.
3. Anchor B calls `responseRoomPK` to accept or decline the competition request.
4. Anchor B accepts the request, waits for the `TRTCLiveRoomDelegate onAnchorEnter` notification, and calls `startPlay` to play anchor A's video image.
5. Anchor A receives the `responseCallback` notification, which specifies whether the competition request is accepted.
6. The request is accepted. Anchor A waits for the `TRTCLiveRoomDelegate onAnchorEnter` notification and calls `startPlay` to play anchor B's video image.

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

```
// Anchor A:
// Anchor A creates room 12345.
mLiveRoom.createRoom(12345, param, null);

mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {
        // 6. Anchor A receives a notification of anchor B’s entry.
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});

// 1. Anchor A sends a competition request to anchor B.
mLiveRoom.requestRoomPK(54321, "B", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {  
        // 5. Anchor A receives a callback of whether anchor B accepts the request.
        if (code == 0) {
            // Accepted
        } else {
            // Declined
        }
    }
});

// Anchor B:
// Anchor B creates room 54321.
mLiveRoom.createRoom(54321, param, null);

// 2. Anchor B receives anchor A’s request.
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestRoomPK(
       final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, final int timeout) {
        // 3. Anchor B accepts anchor A's request.
        mLiveRoom.responseRoomPK(userInfo.userId, true, "");
    }
    @Override
    public void onAnchorEnter(final String userId) {
        // 4. Anchor B receives a notification of anchor A’s entry and plays anchor A's video image.
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

[](id:model.step9)
### Step 9. Enable text chat and on-screen comments.
- Call `sendRoomTextMsg` to send text messages. All anchors and viewers in the room will receive the `onRecvRoomTextMsg` callback.
 IM has its default content moderation rules. Text messages that contain blocked terms will not be forwarded by the cloud.
```
// Sender: send text messages
mLiveRoom.sendRoomTextMsg("Hello Word!", null);
// Recipient: listen for text messages
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomTextMsg(String roomId, 
        String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        Log.d(TAG, "Received a message from" + userInfo.userName + ":" + message);
    }
});
```
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All anchors and viewers in the room will receive the `onRecvRoomCustomMsg` callback.
Custom messages are often used to transfer custom signals, e.g., sending and broadcasting likes.
```
// E.g., use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes.
mLiveRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mLiveRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// Recipient: listen for custom messages
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String roomId, String cmd, 
        String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // An on-screen comment is received.
            Log.d(TAG, "Received an on-screen comment from" + userInfo.userName + ":" + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // A like is received.
            Log.d(TAG, userInfo.userName + "liked you.");
        }
    }
});
```

