## Component Overview

`TUIVoiceRoom` is an open-source audio/video UI component. After integrating it into your project, you can make your application support the group audio chat scenario simply by writing a few lines of code. It also supports the [iOS](https://intl.cloud.tencent.com/document/product/647/37287) platform. Its basic features are as shown below:

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a30e897eabbc6f9104bd41db246f33b1.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/857d3b1651cdf1126f1653e1541b3bba.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/6ddb805c442974d202ef610db643fa39.png" width="250"></td>
</tr>
</tbody></table>


## Component Integration

### Step 1. Download and import the `TUIVoiceRoom` component
Go to [GitHub](https://github.com/tencentyun/TUIVoiceRoom), clone or download the code, copy the `Android/Source` directory to your project, and complete the following import operations:
- Complete import in `setting.gradle` as shown below:
```
include ':Source'
```
- Add dependencies on `Source` to the `build.gradle` file in `app`:
```
api project(':Source')
```
- Add dependencies on `TRTC SDK` and `IM SDK` to the `build.gradle` file in the root directory:
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### Step 2. Configure permission requests and obfuscation rules
Configure permission requests for your app in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and later, the mic access must be requested at runtime):

```
<uses-permission android:name="android.permission.INTERNET" />              
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
```

In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.

```
-keep class com.tencent.** { *;}
```

### Step 3. Initialize and log in to the component
```java
    // 1. Initialize
    TRTCVoiceRoom mTRTCVoiceRoom = TRTCVoiceRoom.sharedInstance(this);
    mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    );
		  // 2. Log in
    mTRTCVoiceRoom.login(SDKAppID, userId, userSig, new TRTCVoiceRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            // Logged in
            }
        }
    });
```

**Parameter description:**
- **SDKAppID**: **TRTC application ID**. If you haven't activated the TRTC service, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, and click **Application Info**. The `SDKAppID` is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: **TRTC application key**, which corresponds to `SDKAppID`. On the [Application Management](https://console.cloud.tencent.com/trtc/app) page in the TRTC console, the `SecretKey` is as shown below:
- **userId**: ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend that you keep it consistent with your user account system.
- **userSig**: Security protection signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to directly generate a debugging `userSig` online or calculate it on your own by referring to the [demo project](https://github.com/tencentyun/TUIVoiceRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Implement the audio chat room
1. **The room owner creates an audio chat room through [TRTCVoiceRoom#createRoom](https://intl.cloud.tencent.com/document/product/647/37339)**.
```java
// 1. The room owner calls an API to create a room
int roomId = 12345; // Room ID
final TRTCVoiceRoomDef.RoomParam roomParam = new TRTCVoiceRoomDef.RoomParam();
roomParam.roomName = "Room name";
roomParam.needRequest = false; // Whether your consent is required for listeners to speak
roomParam.seatCount = 7; // Number of room seats. In this example, the number is 7. 6 seats are available after you take one.
roomParam.coverUrl = "URL of room cover image";
mTRTCVoiceRoom.createRoom(roomId, roomParam, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
				// Room created successfully
        }
    }
});
```
2. **A listener enters the audio chat room through [TRTCVoiceRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/37339)**.
```java
// 1. A listener calls an API to enter the room
mTRTCVoiceRoom.enterRoom(roomId, new TRTCVoiceRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
            // Entered room successfully
            }
        }
});
```
3. ***A listener mics on through [TRTCVoiceRoom#enterSeat](https://intl.cloud.tencent.com/document/product/647/37339)**.
```java
// 1. A listener calls an API to mic on
int seatIndex = 2; // Seat index
mTRTCVoiceRoom.enterSeat(seatIndex, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
        // Operation succeeded
        }
    }
});

// 2. The `onSeatListChange` callback is received, and the seat list is refreshed
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}
```
4. **The room owner makes a listener speaker through [TRTCVoiceRoom#pickSeat](https://intl.cloud.tencent.com/document/product/647/37339)**.
```java
// 1. The room owner invites a listener to speak
int seatIndex = 2; // Seat index
String userId = "123"; // ID of the user to speak
mTRTCVoiceRoom.pickSeat(1, userId, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
				// Operation succeeded
        }
    }
});

// 2. The `onSeatListChange` callback is received, and the seat list is refreshed
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}
```
5. **A listener requests to speak through [TRTCVoiceRoom#sendInvitation](https://intl.cloud.tencent.com/document/product/647/37339)**.
```java
// Listener
// 1. A listener calls an API to request to speak
String seatIndex = "1"; // Seat index
String userId = "123"; // User ID
String inviteId = mTRTCVoiceRoom.sendInvitation("takeSeat", userId, seatIndex, null);

// 2. Place the user in the seat after the invitation is accepted
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.enterSeat(index, null);
    }
}

// Room owner
// 1. The room owner receives the request
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("takeSeat")) {
        // 2. The room owner accepts the request.
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
```
6. **The room owner invites a listener to speak through [TRTCVoiceRoom#sendInvitation](https://intl.cloud.tencent.com/document/product/647/37339)**.
```java
// Room owner
// 1. The room owner calls an API to invite a listener to speak
String seatIndex = "1"; // Seat index
String userId = "123"; // User ID
String inviteId = mTRTCVoiceRoom.sendInvitation("pickSeat", userId, seatIndex, null);

// 2. Place the user in the seat after the invitation is accepted
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.pickSeat(index, null);
    }
}

// Listener
// 1. The listener receives the invitation
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("pickSeat")) {
        // 2. The listener accepts the invitation
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
```
7. **Implement text chat through [TRTCVoiceRoom#sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/37339)**.
```java
// Sender: Sends text messages
mTRTCVoiceRoom.sendRoomTextMsg("Hello World!", null);
// Receiver: Listens for text messages
mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
  @Override
  public void onRecvRoomTextMsg(String message, TRTCVoiceRoomDef.UserInfo userInfo) {
      Log.d(TAG, "Received a message from" + userInfo.userName + ": " + message);
  }
});
```
8. **Implement on-screen commenting through [TRTCVoiceRoom#sendRoomCustomMsg](https://intl.cloud.tencent.com/document/product/647/37339)**.
```java
// A sender can customize CMD to distinguish on-screen comments and likes.
// For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes.
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// Receiver: Listens for custom messages
mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCVoiceRoomDef.UserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // An on-screen comment is received
            Log.d(TAG, "Received an on-screen comment from" + userInfo.userName + ": " + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // A like is received
            Log.d(TAG, userInfo.userName + "liked you.");
        }
    }
});
```

## FAQs
If you have any requirements or feedback, contact colleenyu@tencent.com.
