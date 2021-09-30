## Demonstration
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the app we provide to try out TRTC’s karaoke features, including low-latency karaoke, seat management, gifting, text chat, etc.
<table>
     <tr>
         <th>Room owner’s view</th>  
         <th>Listener’s view</th>  
     </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/e52ccb64cd686f6af1c1f561d7969d36.jpg"/></td>
<td><img src="https://main.qcloudimg.com/raw/206ba3492f4a2f18f36b1d5cba4e5558.jpg"/></td>
</tr>
</table>


To quickly enable the karaoke feature, you can modify the demo app we provide and adapt it to your needs. You can also use the `TUIKaraoke` component and customize your own UI.

[](id:DemoUI)
## Using the Demo App’s UI

[](id:ui.step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestKaraoke` and click **Create**.
3. Click **Next** to skip this step.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)
### Step 2. Download the app source code
Clone or download the [TUIKaraoke](https://github.com/tencentyun/TUIKaraoke/tree/main/Android/Source/src/main/java/com/tencent/liteav/tuikaraoke) source code.

[](id:ui.step3)
### Step 3. Configure app project files
1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`.
3. Set parameters in `GenerateTestUserSig.java` as follows:
<ul style="margin:0"><li/>SDKAPPID: a placeholder by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: a placeholder by default. Set it to the actual key.</ul>
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.


>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the demo app**.
>- The correct UserSig distribution method is to integrate the computing code of UserSig into your server and provide an app-oriented API. When UserSig is required, your app can send a request to the business server to obtain the dynamic UserSig. For more information, please see "Generating a UserSig on the Server" in [Generating UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the demo app
Open the source code project `TUIKaraoke` with Android Studio (version 3.5 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the demo app’s source code
The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code. The table below lists the files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|-------|--------|
| base | Base class used by the UI |
| room | Main room views for room owner and listener |
| widget | Common controls |

## Tryout
>! You need at least two devices to try out the demo app.

### User A
1. Enter a username (**which must be unique**) and log in.
2. Tap **Create Room**.
2. Enter the room subject and click **Sing Together**.

### User B
1. Enter a username (**which must be unique**) and log in.
2. Enter the room ID created by user A and click **Enter Room**. <br>

>! You can find the room ID at the top of user A’s room view.

[](id:model)

## Customizing Your Own UI

The `Source` folder in the [source code](https://github.com/tencentyun/TUIKaraoke/tree/main/Android/Source/src/main/java/com/tencent/liteav/tuikaraoke) contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCKaraokeRoom`. You can find the component’s APIs in `TRTCKaraokeRoom.java` and use them to customize your own UI.
<img src="https://main.qcloudimg.com/raw/9c9b6537318b1fa8cd9c6e4e717c361a.png">

[](id:model.step1)
### Step 1. Integrate the SDK
The karaoke component `TRTCKaraokeRoom` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate them into your project.

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
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">DOWNLOAD</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">Integration document</a></td>
</tr>
<tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">DOWNLOAD</a></td>
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
-keep class com.tencent.** { *; }
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
2. Call the `setDelegate` function to register event callbacks of the component.
3. Call the `login` function to log in to the component, and set the key parameters as described below.
 <table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>sdkAppId</td>
<td>You can view the `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
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
<td>callback</td>
<td>Login callback. The code is 0 if login is successful.</td>
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
4. The user will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
5. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker, and mic capturing will be enabled automatically.

<img src="https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png">


<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo
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
1. After performing [step 4](#model.step4) to log in, you can call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest karaoke room list from the backend.
>?The room list in the demo app is for demonstration only. The business logic of karaoke room lists varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by the room owner during room creation via the calling of `createRoom`.
>!If your karaoke list already contains enough room information, you can skip the step of calling `getRoomInfoList`.
4. The user selects a karaoke room, and calls `enterRoom` with the room ID passed in to enter.
5. After entering the room, the user receives an `onRoomInfoChange` notification about room attribute change from the component. The attributes can be recorded, and corresponding changes can be made to the UI, including room name, whether room owner’s consent is required for listeners to speak, etc.
6. The user will receive an `onSeatListChange` notification about the change of the seat list and can update the change to the UI.
7. The user will also receive an `onAnchorEnterSeat` notification that someone became a speaker.

<img src="https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png">
<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo
mTRTCKaraokeRoom.setSelfProfile("my_name", "my_face_url", null);

// 2. Assume that you get the room list `roomList` from the business backend
List<Integer> roomList = GetRoomList();

// 3. Call `getRoomInfoList` to get details of the rooms
mTRTCKaraokeRoom.getRoomInfoList(roomList, new TRTCKaraokeRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCKaraokeRoomDef.RoomInfo> list) {
        if (code == 0) {
            // Refresh the room list on your UI
        }
    }
});

// 4. Select a karaoke room, and pass in the `roomId` to enter it
mTRTCKaraokeRoom.enterRoom(roomId, new TRTCKaraokeRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
                // Entered room successfully
            }
        }
});

// 5. After entering the room, you receive an `onRoomInfoChange` notification
@Override
public void onRoomInfoChange(TRTCKaraokeRoomDef.RoomInfo roomInfo) {
    mNeedRequest = roomInfo.needRequest;
    mRoomName = roomInfo.roomName;
    // The UI can display the title and other information
}

// 6. After entering the room, you receive an `onSeatListChange` notification
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
1. A room owner can put a listener in a seat by passing the `userId` of the listener and the seat number in `pickSeat`. All members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. A room owner can remove a user from a seat by passing the seat number in `kickSeat`. All members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.
3. A room owner can mute or unmute a seat by passing the seat number in `muteSeat`. All members in the room will receive an `onSeatListChange` notification and an `onSeatMute` notification.
4. A room owner can block or unblock a seat by passing the seat number in `closeSeat`. Listeners cannot take a blocked seat, and all members in the room will receive an `onSeatListChange` notification and an `onSeatClose` notification.
<img src="https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png">

:::
::: Listener
1. A listener can take a seat by passing the seat number in `enterSeat`. All members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. A listener can leave a seat by calling `leaveSeat`. All members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

<img src="https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png">

After a seat operation, the order in which different notifications are sent is: callbacks > `onSeatListChange` > independent events such as `onAnchorEnterSeat`.

<dx-codeblock>
::: java java
// 1. The room owner puts a user in seat 1
mTRTCKaraokeRoom.pickSeat(1, "123", new TRTCKaraokeRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. A callback is returned
        if (code == 0) {
        }
    }
});

// 3. The listener receives the `onSeatListChange` callback and refreshes the seat list
@Override
public void onSeatListChange(final List<TRTCKaraokeRoomDef.SeatInfo> seatInfoList) {
}

// 4. The anchor receives a notification about the change of a specific seat, which can be used to determine whether the listener has taken the seat
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
        // 2. A callback is returned
        if (code == 0) {
        }
    }
});

// 3. The listener receives the `onSeatListChange` callback and refreshes the seat list
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
If you want listeners and room owners to obtain each other’s consent before performing the above actions in your app, you can use signaling for invitation sending.

<dx-tabs>
::: Listener requesting to speak
1. A listener calls `sendInvitation`, passing in information including the room owner’s `userId` and custom command words. The API will return an `inviteId`, which should be recorded.
2. The room owner receives an `onReceiveNewInvitation` notification, and a window pops up on the UI asking the room owner whether to accept the request.
3. The room owner calls `acceptInvitation` with the `inviteId` passed in to accept the request.
4. The listener receives an `onInviteeAccepted` notification and calls `enterSeat` to become a speaker.

<img src="https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png">

<dx-codeblock>
::: java java
// Listener
// 1. Call `sendInvitation` to request to take seat 1
String inviteId = mTRTCKaraokeRoom.sendInvitation("ENTER_SEAT", ownerUserId, "1", null);

// 2. Put the user in the seat when the invitation is accepted by the listener
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCKaraokeRoom.enterSeat(1, null);
    }
}

// Room owner
// 1. Receive the request
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("ENTER_SEAT")) {
        // 2. Accept the request
         mTRTCKaraokeRoom.acceptInvitation(id, null);
    }
}
:::
</dx-codeblock>
:::
::: Room owner inviting listener to take seat
1. The room owner calls `sendInvitation`, passing in information including the listener's `userId` and custom command words. The API will return an `inviteId`, which should be recorded.
2. The listener receives an `onReceiveNewInvitation` notification, and a window pops up asking the listener whether to accept the invitation.
3. The listener calls `acceptInvitation` with the `inviteId` passed in to accept the invitation.
4. The room owner receives an `onInviteeAccepted` notification and calls `pickSeat` to make the listener a speaker.

<img src="https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png">

<dx-codeblock>
::: java java
// Room owner
// 1. Call `sendInvitation` to invite user `123` to take seat 2
String inviteId = mTRTCKaraokeRoom.sendInvitation("PICK_SEAT", "123", "2", null);

// 2. Put the user in the seat when the invitation is accepted by the listener
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCKaraokeRoom.pickSeat(2, null);
    }
}

// Listener
// 1. Receive the request
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("PICK_SEAT")) {
        // 2. Accept the request
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
// Sender: customize CMD to distinguish between on-screen comments and likes
// For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes
mTRTCKaraokeRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mTRTCKaraokeRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// Recipient: listen for custom messages
mTRTCKaraokeRoom.setDelegate(new TRTCKaraokeRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCKaraokeRoomDef.UserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // Receive an on-screen comment
            Log.d(TAG, "Received an on-screen comment from" + userInfo.userName + ": " + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // Receive a like
            Log.d(TAG, userInfo.userName + "liked you.");
        }
    }
});
:::
</dx-codeblock>
