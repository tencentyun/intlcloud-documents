## Component Overview
`TUIKaraoke` is an open-source audio/video UI component. After integrating it into your project, you can make your application support the online karaoke scenario and try out the TRTC capabilities such as karaoke, seat management, gift giving/receiving, and text chat simply by writing a few lines of code. It also supports the iOS platform. Its basic features are as shown below:

<table>
     <tr>
         <th width=20%  style="text-align:center">Chat</th>
         <th width=20%  style="text-align:center">Sound Effect Management</th>
     </tr>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/819e86970cecabcb10143a49a4759b32.png" width="400"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/3616f2a5193c26bad447744ed7bf417d.png" width="400"></td>
</tr>
</table>



## Component Integration
### Step 1. Download and import the `TUIKaraoke` component

Go to [GitHub](https://github.com/tencentyun/TUIKaraoke), clone or download the code, copy the `Source` and `Debug` directories in the `Android` directory to your project, and complete the following import operations:
- Complete import in `setting.gradle` as shown below:
```
include ':Source'
include ':Debug'
```
- Add dependencies on `TUIKaraoke` to the `build.gradle` file in `app`:
```
api project(':Source')
```
- Add dependencies on `TRTC SDK` and `IM SDK` to the `build.gradle` file in the root directory:
```
ext {
    liteavSdk = "com.tencent.liteav:LiteAVSDK_TRTCl:latest.release"
    imSdk = "com.tencent.imsdk:imsdk-plus:latest.release"
}
```

### Step 2. Configure permission requests and obfuscation rules

Configure permission requests for your app in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and later, the mic access and storage read permission must be requested at runtime):

```
<uses-permission android:name="android.permission.SYSTEM_ALERT_WINDOW" />        // Use case: This permission is required for the floating window
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.RECORD_AUDIO" />
<uses-permission android:name="android.permission.MODIFY_AUDIO_SETTINGS" />
<uses-permission android:name="android.permission.BLUETOOTH" />                  // Use case: This permission is required when a Bluetooth headset is used
```

In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.
```
-keep class com.tencent.** { *;}
```

### Step 3. Initialize and log in to the component 
For more information on relevant APIs, see [TUIKaraoke](https://intl.cloud.tencent.com/document/product/647/41943).

```java
  // 1. Initialize
  TRTCKaraokeRoom mTRTCKaraokeRoom = TRTCKaraokeRoom.sharedInstance(this);
  mTRTCKaraokeRoom.setDelegate(this);
  // 2. Log in
  mTRTCKaraokeRoom.login(SDKAppID, UserID, UserSig, new TRTCKaraokeRoomCallback.ActionCallback() {
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
- **userId**: Current user ID, which is a string and can contain up to 32 bytes of letters and digits (special symbols are not supported). You can customize it based on your actual account system.
- **userSig**: Security protection signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to directly generate a debugging `userSig` online or calculate it on your own by referring to the [TUIKaraoke demo project](https://github.com/tencentyun/TUICalling/blob/main/Android/App/src/main/java/com/tencent/liteav/demo/LoginActivity.java#L74). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

### Step 4. Implement the online karaoke scenario
1. **The anchor creates a room through [TUIKaraoke.createRoom](https://intl.cloud.tencent.com/document/product/647/41943)**.
```java
int roomId = "Room ID";
TRTCKaraokeRoomDef.RoomParam roomParam = new TRTCKaraokeRoomDef.RoomParam();
roomParam.roomName = "Room name";
roomParam.needRequest = false; // Whether your consent is required for listeners to speak
roomParam.seatCount = 8;       // Number of seats in the room. Set it to `8`
roomParam.coverUrl = "URL of room cover image";
mTRTCKaraokeRoom.createRoom(roomId, roomParam, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
      if (code == 0) {
        // Room created successfully
      }
    }
});
```
2. **A listener enters the room through [TUIKaraoke.enterRoom](https://intl.cloud.tencent.com/document/product/647/41943)**.
```java
mTRTCKaraokeRoom.enterRoom(roomId, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
        // Entered room successfully
        }
    }
});
```
3. ***A listener mics on through [TUIKaraoke.enterSeat](https://intl.cloud.tencent.com/document/product/647/41943)**.
```java
// 1. A listener calls an API to mic on
int seatIndex = 1;
mTRTCKaraokeRoom.enterSeat(seatIndex, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
        // Mic turned on successfully
        }
    }
});
// 2. The listener receives the `onSeatListChange` callback and refreshes the seat list
@Override
public void onSeatListChange(final List<TRTCKaraokeRoomDef.SeatInfo> seatInfoList) {
}
```

>? You can implement other seat management operations as instructed in [TRTCKaraoke (Android)](https://intl.cloud.tencent.com/document/product/647/41943) or by referring to the [TUIKaraoke demo project](https://github.com/tencentyun/TUIKaraoke/).

4. **Play back songs and try out the karaoke scenario**
You can get the music ID and URL to play back a song based on your business. For more information, see [Music Playback APIs](https://intl.cloud.tencent.com/document/product/647/41943#.E9.9F.B3.E4.B9.90.E6.92.AD.E6.94.BE.E6.8E.A5.E5.8F.A32).
```java
// Play back the music
mTRTCKaraokeRoom.startPlayMusic(musicID,url);
// Stop the music
mTRTCKaraokeRoom.stopPlayMusic();
```

After completing the previous steps, you can implement the basic karaoke features. If your business needs more features such as text chat and gift giving, you can integrate the following capabilities:

### Step 5. Add the text chat feature (optional)
If you want the text chat feature between anchors and listeners, implement message sending/receiving as follows:
For more information on relevant APIs, see [sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/41943#sendroomtextmsg).
```java
// Sender: Sends text messages
mTRTCKaraokeRoom.sendRoomTextMsg("Hello Word!", new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // Sent successfully
        }
    }
});
// Receiver: Listens for text messages
mTRTCKaraokeRoom.setDelegate(new TRTCKaraokeRoomDelegate() {
  @Override
  public void onRecvRoomTextMsg(String message, TRTCKaraokeRoomDef.UserInfo userInfo) {
      Log.d(TAG, "Received a message from" + userInfo.userName + ": " + message);
  }
});
```

### Step 6. Add the gift giving feature (optional)
If you want the gift giving and receiving features, implement gift giving, receiving, and displaying as follows:
```java
// Sender: Customize `CMD_GIFT` to distinguish between gift messages
mTRTCKaraokeRoom.sendRoomCustomMsg("CMD_GIFT",date, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // Sent successfully
        }
    }
});

// Receiver: Listens for gift messages
mTRTCKaraokeRoom.setDelegate(new TRTCKaraokeRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCKaraokeRoomDef.UserInfo userInfo) {
        if ("CMD_GIFT".equals(cmd)) {
            // Received a gift message
            Log.d(TAG, "Received a gift from" + userInfo.userName + ": " + message);
        }
    }
});
```

## FAQs
### Does the `TUIKaraoke` component support sound effect features such as voice change, tone change, and reverb?
Yes. For more information, see the [TUIKaraoke demo project](https://github.com/tencentyun/TUIKaraoke/blob/main/Android/Source/src/main/java/com/tencent/liteav/tuikaraoke/ui/audio/AudioEffectPanel.java).

>? If you have any requirements or feedback, contact colleenyu@tencent.com.
