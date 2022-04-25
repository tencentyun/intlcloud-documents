## Component Overview

`TUILiveRoom` is an open-source video live streaming scenarios UI component. After integrating it into your project, you can make your application support the interactive video live streaming scenario simply by writing a few lines of code. It provides source code for Android and iOS platforms. Its basic features are as shown below:
<table>
<tr>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/34337da1f6427b9a834f6562eba5c663.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/52eb1656b5a892e6da65f49a1d503735.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/70c9e1e7290592f8c7892b236fb1061e.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/ed8c3666aa03951c6d0d9cfe2dccc495.jpg"/></td>
</tr>
</table>

[](id:model)

## Component Integration
[](id:model.step1)
### Step 1. Download and import the `TUILiveRoom` component
Go to [GitHub](https://github.com/tencentyun/TUILiveRoom), clone or download the code, copy the `Android/Beauty`, `Android/Debug`, and `Android/Source` directories to your project, and complete the following import operations:

- Complete import in `setting.gradle` as shown below:
```
include ':Beauty'
include ':Source'
include ':Debug'
```
- Add dependencies on `Source` to the `build.gradle` file in `app`:
```
api project(":Source")
```
- Add dependencies on `TRTC SDK` and `IM SDK` to the `build.gradle` file in the root directory:
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

[](id:model.step2)
### Step 2. Configure permission requests and obfuscation rules
1. Configure permission requests for your application in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and above, the camera and storage read permissions must be requested at runtime.)
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
2. In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.
<dx-codeblock>
::: java java
-keep class com.tencent.** { *;}
:::
</dx-codeblock>

[](id:model.step3)
### Step 3. Initialize and log in to the component
<dx-codeblock>
::: java java
TRTCLiveRoom mLiveRoom = TRTCLiveRoom.sharedInstance(this);
// useCDNFirst: `true` means that audience watch live streams over CDNs, and `false` means that audience watch live streams in the low latency mode.
// yourCDNPlayDomain: The playback domain name for CDN live streaming
TRTCLiveRoomDef.TRTCLiveRoomConfig config = 
    new TRTCLiveRoomDef.TRTCLiveRoomConfig(useCDNFirst, CDNPlayDomain);
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

**Parameter description:**
- **SDKAppID**: **TRTC application ID**. If you haven't activated the TRTC service, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, and click **Application Info**. The `SDKAppID` is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: **TRTC application key**, which corresponds to `SDKAppID`. On the [Application Management](https://console.cloud.tencent.com/trtc/app) page in the TRTC console, the `SecretKey` is as shown below:
- **userId**: ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend that you keep it consistent with your user account system.
- **userSig**: Security protection signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to directly generate a debugging `userSig` online, or you can calculate it on your own by referring to the [demo project](https://github.com/tencentyun/TUIRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).
- **config**: Global configuration information. Please initialize it during login as it cannot be modified after login.
- **useCDNFirst**: Specifies the way the audience watches live streams. `true` means that the audience watches live streams over CDNs, which is cost-efficient but has high latency. `false` means that the audience watches live streams in the low latency mode, the cost of which is between that of CDN live streaming and co-anchoring, but the latency is within one second.
- **CDNPlayDomain**: Specifies the domain name for CDN live streaming, which takes effect only if `useCDNFirst` is set to `true`. You can set it in **CSS console** > [Domain Management](https://console.cloud.tencent.com/live/domainmanage).
- **callback**: Callback for login. The return code is `0` if login is successful.



[](id:model.step4)
### Step 4. Implement an interactive video live room
1. **The anchor starts streaming through [TRTCLiveRoom#createRoom](https://intl.cloud.tencent.com/document/product/647/37333)**.
<dx-codeblock>
::: java java
// 1. Set your username and profile photo as an anchor
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
2. **Audience watches through [TRTCLiveRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/37333)**.
```java
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

// 4. After receiving the notification about the anchor’s entry, start playback
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {  
        // 5. Play the anchor's video
				// `mTXCloudVideoView` is the view for playback for audience
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
```

3. **Audience member and the anchor co-anchor together through [TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37333)**.
<dx-codeblock>
::: java java
// 1. The audience member sends a co-anchoring request
// `LINK_MIC_TIMEOUT` is the timeout period
mLiveRoom.requestJoinAnchor(mSelfUserId + "requested to co-anchor", LINK_MIC_TIMEOUT
    new TRTCLiveRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 4. The request is accepted by the anchor
            TXCloudVideoView view = new TXCloudVideoView(context);
            parentView.add(view);
            // 5. The audience member turns on the camera and starts pushing streams
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
        // 6. The anchor receives a notification that the co-anchoring audience member has turned on the mic
        TXCloudVideoView view = new TXCloudVideoView(context);
        parentView.add(view);
        // 7. The anchor plays the audience member’s video
        mLiveRoom.startPlay(userId, view, null);
    }
});
:::
</dx-codeblock>
4. **Anchors compete through [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37333)**.
<dx-codeblock>
::: java java
// Anchor A:
// Create room 12345
mLiveRoom.createRoom(12345, param, null);

mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onAnchorEnter(final String userId) {
        // 6. Receive a notification about anchor B’s entry
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

// 2. Receive anchor A’s request
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRequestRoomPK(
       final TRTCLiveRoomDef.TRTCLiveUserInfo userInfo, final int timeout) {
        // 3. Accept anchor A's request
        mLiveRoom.responseRoomPK(userInfo.userId, true, "");
    }
    @Override
    public void onAnchorEnter(final String userId) {
        // 4. Receive a notification about anchor A’s entry and play anchor A's video
        mLiveRoom.startPlay(userId, mTXCloudVideoView, null);
    }
});
:::
</dx-codeblock>
5. **Implement text chat through [TRTCLiveRoom#sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/37333)**.
<dx-codeblock>
::: java java
// Sender: Sends text messages
mLiveRoom.sendRoomTextMsg("Hello Word!", null);
// Receiver: Listens for text messages
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
	@Override
	public void onRecvRoomTextMsg(String roomId, 
			String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
			Log.d(TAG, "Received a message from" + userInfo.userName + ": " + message);
	}
});
:::
</dx-codeblock>
6. **Implement on-screen commenting through [TRTCLiveRoom#sendRoomCustomMsg](https://intl.cloud.tencent.com/document/product/647/37333)**.
<dx-codeblock>
::: java java
// A sender can customize CMD to distinguish on-screen comments and likes.
// For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes.
mLiveRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mLiveRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// Receiver: Listens for custom messages
mLiveRoom.setDelegate(new TRTCLiveRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String roomId, String cmd, 
        String message, TRTCLiveRoomDef.TRTCLiveUserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // An on-screen comment is received.
            Log.d(TAG, "Received an on-screen comment from" + userInfo.userName + ": " + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // A like is received.
            Log.d(TAG, userInfo.userName + "liked you.");
        }
    }
});
:::
</dx-codeblock>

## FAQs
If you have any requirements or feedback, contact colleenyu@tencent.com.
