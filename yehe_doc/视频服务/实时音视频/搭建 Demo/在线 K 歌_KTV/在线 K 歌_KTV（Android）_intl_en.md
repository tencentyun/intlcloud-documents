## Demo UI
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC's karaoke features, including low-latency karaoke, seat management, gift sending and receiving, text chat, etc.
<table>
     <tr>
         <th>Room Owner</th>  
         <th>Listener</th>  
     </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/e52ccb64cd686f6af1c1f561d7969d36.jpg"/></td>
<td><img src="https://main.qcloudimg.com/raw/206ba3492f4a2f18f36b1d5cba4e5558.jpg"/></td>
</tr>
</table>


To quickly enable the karaoke feature, you can modify the demo app we provide and adapt it to your needs. You may also use the `TUIKaraoke` component and customize your own UI.

[](id:DemoUI)
## Using the App’s UI

[](id:ui.step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestKaraoke` and click **Create**.
3. Click **Next** to skip this step.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)
### Step 2. Download the application source code
Clone or download the [TUIKaraoke](https://github.com/tencentyun/TUIKaraoke/tree/main/Android/Source/src/main/java/com/tencent/liteav/tuikaraoke) source code.

[](id:ui.step3)
### Step 3. Configure application project files
1. In the **Modify Configuration** step, select your platform.
2. Find and open `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`.
3. Set parameters in `GenerateTestUserSig.java`:
<ul style="margin:0"><li/>SDKAPPID: a placeholder by default. Set it to the actual `SDKAppID`.
<li>SECRETKEY: a placeholder by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.


>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the application
Open the source code project `TUIKaraoke` with Android Studio (version 3.5 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the app’s source code
The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code. The table below lists the files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|-------|--------|
| base | Basic classes used by the UI |
| room | Main room views for room owner and listener |
| widget | Common controls |

## Tryout
>! You need at least two devices to try out the application.

### User A
1. Enter a username (**which must be unique**) and log in.
2. Tap **Create Room**.
2. Enter the room subject and tap **Join**.

### User B
1. Enter a username (**which must be unique**) and log in.
2. Enter the ID of the room created by user A, and tap **Enter Room**.<br>

>! You can find the room ID at the top of user A’s room view.
<img src="https://qcloudimg.tencent-cloud.cn/raw/746497909c6a802c55205cf13461b804.png" width="320"/>

[](id:model)

## Customizing UI

The `Source` folder in the [source code](https://github.com/tencentyun/TUIKaraoke/tree/main/Android/Source/src/main/java/com/tencent/liteav/tuikaraoke) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCKaraokeRoom`. You can find the component’s APIs in `TRTCKaraokeRoom.java` and use them to customize your own UI.
<img src="https://main.qcloudimg.com/raw/9c9b6537318b1fa8cd9c6e4e717c361a.png">

[](id:model.step1)
### Step 1. Integrate the SDKs
The `TRTCKaraokeRoom` component depends on the TRTC SDK and IM SDK. Follow the steps below to integrate them into your project.

**Method 1: adding dependencies via Maven**
1. Add the TRTC SDK and IM SDK dependencies to `dependencies`.
<dx-codeblock>
::: java java
dependencies {
       complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       complie 'com.tencent.imsdk:imsdk:latest.release'
       compile 'com.google.code.gson:gson:2.3.1'
}
:::
</dx-codeblock>

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
Configure permission requests for your app in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and above, the read storage permission must be requested at runtime.)
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
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
:::
</dx-codeblock>

In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.
<dx-codeblock>
::: java java
-keep class com.tencent.** { *;}
:::
</dx-codeblock>

[](id:model.step3)
### Step 3. Import the `TRTCKaraoke` component
Copy all the files in the directory below to your project:
<dx-codeblock>
::: java java
Source/src/main/java/com/tencent/liteav/tuikaraoke/model
:::
</dx-codeblock>

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` API to create an instance of the `TRTCKaraoke` component.
2. Call the `setDelegate` API to register event callbacks of the component.
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
<tr>
<td>callback</td>
<td>Login callback. The code is `0` if login is successful.</td>
</tr>
</table>
<dx-codeblock>
::: java java
TRTCKaraoke mTRTCKaraokeRoom = TRTCKaraokeRoom.sharedInstance(this);
mTRTCKaraokeRoom.setDelegate(this);
mTRTCKaraokeRoom.login(SDKAPPID, userId, userSig, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {![](https://main.qcloudimg.com/raw/7e61af0f3de8302260a1e10d7da6231e.png)
            // Logged in
        }
    }
});
:::
</dx-codeblock>

[](id:model.step5)
### Step 5. Create a room and become a speaker
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. A user calls `createRoom` to create a karaoke room, passing in room attributes (e.g., room ID, whether listeners require room owner’s consent to speak, number of seats).
3. After creating the room, call `enterSeat` to take a seat.
4. You will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
5. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat, and mic capturing will be enabled automatically.

<img src="https://qcloudimg.tencent-cloud.cn/raw/c925337d62289d8c3cdba4714145f5cb.png">


<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo.
mTRTCKaraokeRoom.setSelfProfile("my_name", "my_face_url", null);

// 2. Call `createRoom` to create a room
final TRTCKaraokeRoomDef.RoomParam roomParam = new TRTCKaraokeRoomDef.RoomParam();
roomParam.roomName = "Room name";
roomParam.needRequest = false; // Whether your consent is required for listeners to speak
roomParam.seatCount = 7; // Number of room seats. In this example, the number is 7. 6 seats are available after you take one.
roomParam.coverUrl = "URL of room cover image";
mTRTCKaraokeRoom.createRoom(mRoomId, roomParam, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. Take seat 0
            mTRTCKaraokeRoom.enterSeat(0, new TRTCKaraokeRoomCallback.ActionCallback() {
                @Override
                public void onCallback(int code, String msg) {
                    if (code == 0) {
                    }
                }
            });
        }
    }
});

// 4. After taking a seat, you receive an `onSeatListChange` notification
@Override
public void onSeatListChange(final List<TRTCKaraokeRoomDef.SeatInfo> seatInfoList) {
    // Display the seat list
}

// 5. You receive an `onAnchorEnterSeat` notification
@Override
public void onAnchorEnterSeat(TRTCKaraokeRoomDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step6)
### Step 6. Enter a room as a listener
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest karaoke room list from the backend.
>?The room list in the demo app is for demonstration only. The business logic of karaoke room lists varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by room owners when they call `createRoom`.
>!If your karaoke room list already contains enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select a karaoke room, and call `enterRoom` with the room ID passed in to enter the room.
5. After entering the room, you will receive an `onRoomInfoChange` notification about room change from the component. Record the room information, including room name, whether the room owner’s consent is required for listeners to speak, etc., and update it to the UI.
6. You will receive an `onSeatListChange` notification about seat change from the component. Update the change to the UI.
7. You will also receive an `onAnchorEnterSeat` notification that someone becomes a speaker.

<img src="https://qcloudimg.tencent-cloud.cn/raw/0a96afd3948228a6f1fd19eb0b7b1b3e.png">
<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo.
mTRTCKaraokeRoom.setSelfProfile("my_name", "my_face_url", null);

// 2. Get the room list from the backend. Suppose it is `roomList`.
List<Integer> roomList = GetRoomList();

// 3. Call `getRoomInfoList` to get details of the rooms.
mTRTCKaraokeRoom.getRoomInfoList(roomList, new TRTCKaraokeRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCKaraokeRoomDef.RoomInfo> list) {
        if (code == 0) {
            // Refresh the room list on your UI
        }
    }
});

// 4. Select a karaoke room and pass in the `roomId` to enter it
mTRTCKaraokeRoom.enterRoom(roomId, new TRTCKaraokeRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
                // Entered room successfully
            }
        }
});

// 5. After successful room entry, you receive an `onRoomInfoChange` notification.
@Override
public void onRoomInfoChange(TRTCKaraokeRoomDef.RoomInfo roomInfo) {
    mNeedRequest = roomInfo.needRequest;
    mRoomName = roomInfo.roomName;
    // The UI can display the title and other information
}

// 6. You receive an `onSeatListChange` notification
@Override
public void onSeatListChange(final List<TRTCKaraokeRoomDef.SeatInfo> seatInfoList) {
    // Display the seat list
}

// 7. You receive an `onAnchorEnterSeat` notification
@Override
public void onAnchorEnterSeat(TRTCKaraokeRoomDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step7)
### Step 7. Manage seats

<dx-tabs>
::: Room owner
1. Call `pickSeat`, passing in a seat number and the `userId` of a listener to place the listener in the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. Call `kickSeat`, passing in a seat number to remove the speaker from the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.
3. A room owner can mute or unmute a seat by passing in the seat number to `muteSeat`. All members in the room will receive an `onSeatListChange` notification and an `onSeatMute` notification.
4. Call `closeSeat`, passing in a seat number to block/unblock the seat. Listeners cannot take a blocked seat, and all users in the room will receive an `onSeatListChange` notification and an `onSeatClose` notification.
<img src="https://qcloudimg.tencent-cloud.cn/raw/b6074cf63c373e233b0a1a1d45422eda.png">

:::
::: Listener
1. Call `enterSeat`, passing in a seat number to take the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. Call `leaveSeat` to leave your seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

<img src="https://qcloudimg.tencent-cloud.cn/raw/32075b60078151ad6988efffeb9aa49f.png">

After a seat operation, the order in which different notifications are sent is: callbacks > `onSeatListChange` > independent events such as `onAnchorEnterSeat`.

<dx-codeblock>
::: java java
// 1. The room owner places a user in seat No. 1
mTRTCKaraokeRoom.pickSeat(1, "123", new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. A callback is returned.
        if (code == 0) {
        }
    }
});

// 3. The listener receives the `onSeatListChange` callback, and refreshes the seat list
@Override
public void onSeatListChange(final List<TRTCKaraokeRoomDef.SeatInfo> seatInfoList) {
}

// 4. The room owner receives a notification about the change of a specific seat, which can be used to determine whether the user has taken the seat
public void onAnchorEnterSeat(int index, TRTCKaraokeRoomDef.UserInfo user) {
}
:::
</dx-codeblock>

<dx-codeblock>
::: java java
// 1. A listener takes seat 2
mTRTCKaraokeRoom.enterSeat(2, new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. A callback is returned.
        if (code == 0) {
        }
    }
});

// 3. The listener receives the `onSeatListChange` callback, and refreshes the seat list
@Override
public void onSeatListChange(final List<TRTCKaraokeRoomDef.SeatInfo> seatInfoList) {
}

// 4. The listener receives a notification about the change of a specific seat and can determine whether he or she has taken the seat successfully
public void onAnchorEnterSeat(int index, TRTCKaraokeRoomDef.UserInfo user) {
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step8)
### Step 8. Use signaling for invitations
In [seat management](#model.step7), listeners can take and leave seats without the room owner’s consent, and the room owner can put listeners in seats without the listeners’ consent.
If you want listeners and room owners to obtain each other’s consent before performing the above actions in your application, you can use signaling for invitation sending.

<dx-tabs>
::: Listener requesting to take seat
1. A listener calls `sendInvitation`, passing in information including the room owner’s `userId` and custom command words. The API will return an `inviteId`, which should be recorded.
2. The room owner receives an `onReceiveNewInvitation` notification, and a window pops up on the UI asking the room owner whether to accept the request.
3. The room owner calls `acceptInvitation` with the `inviteId` passed in to accept the request.
4. The listener receives an `onInviteeAccepted` notification and calls `enterSeat` to become a speaker.

<img src="https://qcloudimg.tencent-cloud.cn/raw/1396c2611b83bcc5532edceb97d94f94.png">

<dx-codeblock>
::: java java
// Listener
// 1. Call `sendInvitation` to request to take seat 1
String inviteId = mTRTCKaraokeRoom.sendInvitation("ENTER_SEAT", ownerUserId, "1", null);

// 2. Place the user in the seat after the invitation is accepted
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCKaraokeRoom.enterSeat(1, null);
    }
}

// Room owner
// 1. The room owner receives the request.
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("ENTER_SEAT")) {
        // 2. The room owner accepts the request.
         mTRTCKaraokeRoom.acceptInvitation(id, null);
    }
}
:::
</dx-codeblock>
:::
::: Room owner inviting listener to take seat
1. The room owner calls `sendInvitation`, passing in information including the listener's `userId` and custom command words. The API will return an `inviteId`, which should be recorded.
2. The listener receives an `onReceiveNewInvitation` notification, and a window pops up asking the listener whether to agree to speak.
3. The listener calls `acceptInvitation` with the `inviteId` passed in to accept the invitation.
4. The room owner receives an `onInviteeAccepted` notification and calls `pickSeat` to make the listener a speaker.

<img src="https://qcloudimg.tencent-cloud.cn/raw/d9ae981d95441aa4e535ee1921d31ed6.png">

<dx-codeblock>
::: java java
// Room owner
// 1. Call `sendInvitation` to invite user `123` to take seat 2
String inviteId = mTRTCKaraokeRoom.sendInvitation("PICK_SEAT", "123", "2", null);

// 2. Place the user in the seat after the invitation is accepted
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCKaraokeRoom.pickSeat(2, null);
    }
}

// Listener
// 1. The listener receives the invitation.
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("PICK_SEAT")) {
        // 2. The listener accepts the invitation.
         mTRTCKaraokeRoom.acceptInvitation(id, null);
    }
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step9)
### Step 9. Enable text chat and on-screen comments
- Call `sendRoomTextMsg` to send common text messages. All users in the room will receive an `onRecvRoomTextMsg` callback.
 IM has its default content moderation rules. Text messages that contain restricted terms will not be forwarded by the cloud.
  <dx-codeblock>
  ::: java java
  // Sender: send text messages
  mTRTCKaraokeRoom.sendRoomTextMsg("Hello Word!", null);
  // Recipient: listen for text messages
  mTRTCKaraokeRoom.setDelegate(new TRTCKaraokeRoomDelegate() {
    @Override
    public void onRecvRoomTextMsg(String message, TRTCKaraokeRoomDef.UserInfo userInfo) {
        Log.d(TAG, "Received a message from" + userInfo.userName + ": " + message);
    }
  });
  :::
  </dx-codeblock>
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All users in the room will receive an `onRecvRoomCustomMsg` callback.
Custom messages are often used to transfer custom signals, e.g., to give and broadcast likes.
<dx-codeblock>
::: java java
// A sender can customize CMD to distinguish on-screen comments and likes.
// For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes.
mTRTCKaraokeRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mTRTCKaraokeRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// Recipient: listen for custom messages
mTRTCKaraokeRoom.setDelegate(new TRTCKaraokeRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCKaraokeRoomDef.UserInfo userInfo) {
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
