## Demonstration
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo app we provide to try out TRTC's interactive live streaming features, including co-anchoring, anchor competition, low-latency watch, and on-screen comments.



To quickly enable the interactive live video streaming feature, you can modify the demo app we provide and adapt it to your needs. You can also use the `TRTCLiveRoom` component and customize your own UI.

[](id:DemoUI)
## Using the Demo App's UI

[](id:ui.step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestLiveRoom` and click **Create**.
3. Click **Next** to skip this step.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.


[](id:ui.step2)
### Step 2. Download the app source code
Clone or download the [TUILiveRoom](https://github.com/tencentyun/TUILiveRoom) source code.


[](id:ui.step3)
### Step 3. Configure app project files
1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`.
3. Set parameters in `GenerateTestUserSig.java` as follows:
<ul style="margin:0"><li/>SDKAPPID: a placeholder by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: a placeholder by default. Set it to the actual key.</ul>

![](https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png)

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the demo app**.
> The correct `UserSig` distribution method is to integrate the computing code of `UserSig` into your server and provide an app-oriented API. When `UserSig` is needed, your app can send a request to the business server to obtain the dynamic `UserSig`. For more information, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the demo app
Open the source code project `TUILiveRoom` with Android Studio (version 3.5 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the demo app's source code
The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code. The table below lists the files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|:-------:|:--------|
| anchor | Implementation code for anchor-end views |
| audience | Implementation code for audience-end views |
| common | Implementation code for common UI components |
| widget | Common controls |



## Tryout
>! You need at least two devices to try out the demo app.

### User A
1. Enter a username (**which must be unique**) and log in.
2. Tap **Create Room**.
3. Enter a room name and tap **Start**.

### User B
1. Enter a username (**which must be unique**).
2. Enter the ID of the room created by user A, and tap **Join**.<br>

>! You can find the room ID at the top of user A's room view.



## Listening for Room Status and Getting Room List for Co-Anchoring
You can use `LiveRoomManager` to listen for room status.
<dx-codeblock>
::: java java
LiveRoomManager.getInstance().addCallback(new LiveRoomManager.RoomCallback() {
    /**
     * A room was created
     * @param roomId
     * @param callback  The result of internal processing
     */
    @Override
    public void onRoomCreate(int roomId, final LiveRoomManager.ActionCallback callback) {
        // doSomething
    }

    /**
     * A room was terminated
     * @param roomId
     * @param callback  The result of internal processing
     */
    @Override
    public void onRoomDestroy(int roomId, final LiveRoomManager.ActionCallback callback) {
        // doSomething
    }
    
    /**
     * The room list was obtained
     * @param callback
     */
    @Override
    public void onGetRoomIdList(final LiveRoomManager.GetCallback callback) {
        // The room list was obtained, which is used for co-anchoring and must be maintained by yourself
        if(callback != null) {
            if(success) {
                // Callback successful, and the room list was returned
                callback.onSuccess(roomList);
            } else {
                // Failed to get the room list
                callback.onError(code, message);
            }
        }
    }
});
:::
</dx-codeblock>
Getting the room list may involve async operations. Using callbacks to get the list provides greater convenience and flexibility.


[](id:model)
## Customizing Your Own UI

The `Source` folder in the [source code](https://github.com/tencentyun/TUILiveRoom/tree/master/Android/Source/src/main/java/com/tencent/liteav/liveroom) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCLiveRoom`. You can find the component's APIs in `TRTCLiveRoom.java` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/710358e4e170d44304cdb9bc991ad209.jpg)

[](id:model.step1)
### Step 1. Integrate the SDK
The `TRTCLiveRoom` component depends on the TRTC SDK and IM SDK. Follow the steps below to integrate them into your project.

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
Configure permission requests for your app in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and above, the camera and read storage permissions must be requested at runtime.)
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
-keep class com.tencent.** { *; }
:::
</dx-codeblock>

[](id:model.step3)
### Step 3. Import the `TRTCLiveRoom` component
Copy all the files in the directory below to your project:
<dx-codeblock>
::: java java
src/main/java/com/tencent/liteav/liveroom/model
:::
</dx-codeblock>

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` API to create an instance of the `TRTCLiveRoom` component.
2. Create a `TRTCLiveRoomConfig` object, and set its `useCDNFirst` and `CDNPlayDomain` attributes.
 - `useCDNFirst`: specifies the way audience watch live streams. `true` means that audience watch live streams over CDNs, which is cost-efficient but has high latency. `false` means that audience watch live streams in the low latency mode, the cost of which is between that of CDN live streaming and co-anchoring, but the latency is within 1 second.
 - `CDNPlayDomain`: specifies the domain name for CDN live streaming, which takes effect only if `useCDNFirst` is set to `true`. You can set it in CSS console > **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**.
3. Call the `login` function to log in to the component, and set the key parameters as described below.
 <table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>SDKAPPID</td>
<td>You can view the `SDKAppID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr>
<tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_).</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. To obtain one, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr>
<tr>
<td>config</td>
<td>Global configuration information. Please initialize it during login as it cannot be modified after login.<ul style="margin:0;">
<li>`useCDNFirst`: specifies the way audience watch live streams. `true` means that audience watch live streams over CDNs, which is cost-efficient but has high latency. `false` means that audience watch live streams in the low latency mode, the cost of which is between that of CDN live streaming and co-anchoring, but the latency is within 1 second.</li>
<li>`CDNPlayDomain`: specifies the domain name for CDN live streaming, which takes effect only if `useCDNFirst` is set to `true`. You can set it in CSS console > **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>**.</li>
</ul></td>
</tr>
<tr>
<td>callback</td>
<td>Login callback. The code is 0 if login is successful.</td>
</tr>
</table>
<dx-codeblock>
::: java java
TRTCLiveRoom mLiveRoom = TRTCLiveRoom.sharedInstance(this);
// useCDNFirst: `true` means that audience watch live streams over CDNs, and `false` means that audience watch live streams in the low latency mode.
// yourCDNPlayDomain: the playback domain name for CDN live streaming
TRTCLiveRoomDef.TRTCLiveRoomConfig config = 
    new TRTCLiveRoomDef.TRTCLiveRoomConfig(useCDNFirst, yourCDNPlayDomain);
mLiveRoom.login(SDKAPPID, userId, userSig, config, 
    new TRTCLiveRoomCallback.ActionCallback() {
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
### Step 5. Create a room and become a speaker
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Before streaming, you can call `startCameraPreview` to enable camera preview, add beauty filter buttons to the UI, and set beauty filters through `getBeautyManager`.
>?Only the Enterprise Edition SDK supports advanced beauty filter features such as face changing and stickers.
3. After setting beauty filters, call `createRoom` to create a live streaming room.
4. Call `startPublish` to start streaming. To enable CDN live streaming, specify `useCDNFirst` and `CDNPlayDomain` in the `TRTCLiveRoomConfig` parameter, which is passed in during login, and specify `streamID` for playback when calling `startPublish`.

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

<dx-codeblock>
::: java java
// 1. Set the nickname and profile photo
mLiveRoom.setSelfProfile("A", "your_face_url", null);

// 2. Enable camera preview and set beauty filters before streaming
TXCloudVideoView view = new TXCloudVideoView(context);
parentView.add(view);
mLiveRoom.startCameraPreview(true, view, null);
mLiveRoom.getBeautyManager().setBeautyStyle(1);
mLiveRoom.getBeautyManager().setBeautyLevel(6);

// 3. Create a room
TRTCLiveRoomDef.TRTCCreateRoomParam param = new TRTCLiveRoomDef.TRTCCreateRoomParam();
param.roomName = "Test room";
mLiveRoom.createRoom(123456789, param, new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4. Start streaming and publish the streams to CDNs
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});
:::
</dx-codeblock>

[](id:model.step6)
### Step 6. Enter a room as a listener
1. After performing [step 4](#model.step4) to log in, you can call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest room list from the backend.
>?The room list in the demo app is for demonstration only. The business logic of live streaming room lists varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfos` to get short descriptions of the rooms, which are provided by anchors when they call `createRoom` to create the rooms.
>!If your room list already displays enough information, you can skip the step of calling `getRoomInfos`.
4. Select a room, call `enterRoom`, with the room ID passed in to enter the room.
5. Call `startPlay`, with the anchor's `userId` passed in to start playback.
 - If the room list displays the `userId` of the anchor, you can call `startPlay`, passing in the anchor's `userId` to start playback.
 - If you do not know the anchor's `userId`, you can find it in the `onAnchorEnter` event callback, which you will receive after entering the room. You can then call `startPlay` to start playback. 

![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

<dx-codeblock>
::: java java
// 1. Get the room list from the backend. Suppose it is `roomList`
List<Integer> roomList = GetRoomList();

// 2. Call `getRoomInfos` to get the details of the room
mLiveRoom.getRoomInfos(roomList, new TRTCLiveRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCLiveRoomDef.TRTCLiveRoomInfo> list) {
        if (code == 0) {
            // After getting the room information, you can display on the anchor list page the anchor's nickname, profile photo, and other information
        }
    }
})

// 3. Select a `roomid` and enter the room
mLiveRoom.enterRoom(roomid, null);

// 4. After receiving the notification about the anchor's entry, start playback
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {  
        // 5. Play the anchor's video
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
:::
</dx-codeblock>

[](id:model.step7)
### Step 7. Co-anchor
1. Audience calls `requestJoinAnchor` to send a co-anchoring request to the anchor.
2. The anchor receives a notification (`TRTCLiveRoomDelegate#onRequestJoinAnchor`) about the co-anchoring request.
3. The anchor calls `responseJoinAnchor` to accept or decline the co-anchoring request.
4. The audience receives the `TRTCLiveRoomDelegate#responseCallback` event notification, which carries the anchor's response.
5. If the anchor accepts the co-anchoring request, the audience can call `startCameraPreview` to turn the local camera on and then `startPublish` to push streams.
6. The anchor receives a notification (`TRTCLiveRoomDelegate#onAnchorEnter`) that a new stream is available, which carries the audience's `userId`.
7. The anchor calls `startPlay` to play the audience's video.

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)

<dx-codeblock>
::: java java
// 1. The audience sends a co-anchoring request
mLiveRoom.requestJoinAnchor(mSelfUserId + "requested to co-anchor", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4. The request is accepted by the anchor
            TXCloudVideoView view = new TXCloudVideoView(context);
            parentView.add(view);
            // 5. The audience turns on the camera and starts pushing streams
            mLiveRoom.startCameraPreview(true, view, null);
            mLiveRoom.startPublish(mSelfUserId + "_stream", null);
        }
    }
});

// 2. The anchor receives the co-anchoring request
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestJoinAnchor(final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, 
        String reason, final int timeout) {
        // 3. The anchor accepts the co-anchoring request
        mLiveRoom.responseJoinAnchor(userInfo.userId, true, "agreed to co-anchor");
    }

    @Override
    public void onAnchorEnter(final String userId) {
        // 6. The anchor receives a notification that the co-anchoring audience has turned on the mic
        TXCloudVideoView view = new TXCloudVideoView(context);
        parentView.add(view);
        // 7. The anchor plays the audience's video
        mLiveRoom.startPlay(userId, view, null);
    }
});
:::
</dx-codeblock>

[](id:model.step8)
### Step 8. Compete across rooms
1. Anchor A calls `requestRoomPK` to send a competition request to anchor B.
2. Anchor B receives the `TRTCLiveRoomDelegate onRequestRoomPK` notification.
3. Anchor B calls `responseRoomPK` to accept or decline the competition request.
4. Anchor B accepts the request and, after receiving the `TRTCLiveRoomDelegate onAnchorEnter` notification, calls `startPlay` to play anchor A's video.
5. Anchor A receives the `responseCallback` notification, which specifies whether the competition request is accepted.
6. The request is accepted, and after receiving the `TRTCLiveRoomDelegate onAnchorEnter` notification, anchor A calls `startPlay` to play anchor B's video.

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

<dx-codeblock>
::: java java
// Anchor A:
// Create room 12345
mLiveRoom.createRoom(12345, param, null);

mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {
        // 6. Receive a notification about anchor B's entry
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});

// 1. Send a competition request to anchor B
mLiveRoom.requestRoomPK(54321, "B", 
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {  
        // 5. Receive a callback of whether the request is accepted by anchor B
        if (code == 0) {
            // Accepted
        } else {
            // Declined
        }
    }
});

// Anchor B:
// Create room 54321
mLiveRoom.createRoom(54321, param, null);

// 2. Receive anchor A's request
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestRoomPK(
       final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, final int timeout) {
        // 3. Accept anchor A's request
        mLiveRoom.responseRoomPK(userInfo.userId, true, "");
    }
    @Override
    public void onAnchorEnter(final String userId) {
        // 4. Receive a notification about anchor A's entry and play anchor A's video
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
:::
</dx-codeblock>

[](id:model.step9)
### Step 9. Enable text chat and on-screen comments
- Call `sendRoomTextMsg` to send common text messages. All users in the room will receive an `onRecvRoomTextMsg` callback.
 IM has its default content moderation rules. Text messages that contain restricted terms will not be forwarded by the cloud.
  <dx-codeblock>
  ::: java java
  // Sender: send text messages
  mLiveRoom.sendRoomTextMsg("Hello Word!", null);
  // Recipient: listen for text messages
  mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomTextMsg(String roomId, 
        String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        Log.d(TAG, "Received a message from" + userInfo.userName + ": " + message);
    }
  });
  :::
  </dx-codeblock>
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All users in the room will receive an `onRecvRoomCustomMsg` callback.
Custom messages are often used to transfer custom signals, e.g., to give and broadcast likes.
<dx-codeblock>
::: java java// Sender: customize commands to distinguish on-screen comments and likes
// For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes
mLiveRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mLiveRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// Recipient: listen for custom messages
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String roomId, String cmd, 
        String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // Received an on-screen comment
            Log.d(TAG, "Received an on-screen comment from" + userInfo.userName + ": " + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // Received a like
            Log.d(TAG, userInfo.userName + "liked you.");
        }
    }
});
:::
</dx-codeblock>
