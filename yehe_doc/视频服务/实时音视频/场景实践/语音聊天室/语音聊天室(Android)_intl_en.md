## Demonstration
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC’s audio chat room features, including seat management, low-latency audio interaction, text chat, etc.

To quickly implement the audio chat room feature, you can modify the demo we provide and adapt it to your needs. You can also use the `TRTCVoiceRoom` component and customize your own UI.

[](id:DemoUI)
## Using the Demo UI

[](id:ui.step1)
### Step 1. Create an application.
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g. `TestVoiceRoom`, and click **Create**.

>!The audio chat room feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



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
The `trtcvoiceroomdemo` folder in the source code contains two subfolders: `ui` and `model`. In the `ui` subfolder is UI code. The table below lists the files (folders) and UI views they represent. You can refer to it when making UI changes.

| File or Folder | Use |
|-------|--------|
| base | Base class used by the UI |
| list | The list and room creation views |
| room | The main room views for anchors and viewers |
| widget | Common controls |

[](id:model)
## Implementing A Custom UI

The `trtcvoiceroomdemo` folder in the [source code] contains two subfolders: `ui` and `model`. In the `model` subfolder is the reusable open-source component `TRTCVoiceRoom`. You can find the component’s API functions in `TRTCVoiceRoom.java` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)

[](id:model.step1)
### Step 1. Integrate the SDKs.
The audio chat room component `TRTCVoiceRoom` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project.

**Method 1: adding dependencies via Maven**
1. Add the TRTC SDK and IM SDK dependencies to `dependencies`.
```
dependencies {
       complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       complie 'com.tencent.imsdk:imsdk:latest.release'
       compile 'com.google.code.gson:gson:2.3.1'
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
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">Integration document</a></td>
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
<uses-permission android:name="android.permission.READ_PHONE_STATE" />
```

In the `proguard-rules.pro` file, add the SDK classes to the "do not obfuscate" list.
```
-keep class com.tencent.** { *; }
```

[](id:model.step3)
### Step 3. Import the `TRTCVoiceRoom` component.
Copy all the files in the directory below to your project:
```
trtcvoiceroomdemo/src/main/java/com/tencent/liteav/trtcvoiceroom/model
```

<span id="model.step4"></span>
### Step 4. Create a `TRTCVoiceRoom` instance and log in.
1. Call the `sharedInstance` API to create an instance of the `TRTCVoiceRoom` component.
2. Call the `setDelegate` function to register event callbacks of the component.
3. Call the `login` function to log in to the component. Set the key parameters as described below.
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
<td>callback</td>
<td>Login callback. The code is 0 if login is successful.</td>
</tr>
</table>

```
TRTCVoiceRoom mTRTCVoiceRoom = TRTCVoiceRoom.sharedInstance(this);
mTRTCVoiceRoom.setDelegate(this);
mTRTCVoiceRoom.login(SDKAPPID, userId, userSig, new TRTCVoiceRoomCallback.ActionCallback() {
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
2. Call `createRoom` to create an audio chat room and pass in room-related parameters such as room ID, whether to request your consent for viewers to speak, and the number of seats.
3. After successfully creating a room, call `enterSeat` to take a seat.
4. You will receive an `onSeatListChange` notification about seat change from the component. Update the change to the UI.
5. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat, and mic capturing will be enabled automatically.

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)

```
// 1. Set your nickname and profile photo as an anchor.
mTRTCVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2. Call `createRoom` to create a room.
final TRTCVoiceRoomDef.RoomParam roomParam = new TRTCVoiceRoomDef.RoomParam();
roomParam.roomName = "Room ID";
roomParam.needRequest = false; // Whether your consent is required for viewers to speak
roomParam.seatCount = 7; // Number of room seats. In this example, the number is 7. 6 seats remain after you take one.
roomParam.coverUrl = "room cover URL";
mTRTCVoiceRoom.createRoom(mRoomId, roomParam, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. Take seat 0.
            mTRTCVoiceRoom.enterSeat(0, new TRTCVoiceRoomCallback.ActionCallback() {
                @Override
                public void onCallback(int code, String msg) {
                    if (code == 0) {
                    }
                }
            });
        }
    }
});

// 4. After taking a seat, you receive an `onSeatListChange` notification.
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
    // Display the seat list.
}

// 5. You receive an `onAnchorEnterSeat` notification.
@Override
public void onAnchorEnterSeat(TRTCVoiceRoomDef.UserInfo userInfo) {
}
```

[](id:model.step6)
### Step 6. Play as a viewer.
1. After performing [step 4](#model.step4) to log in, you can call `setSelfProfile` to set your nickname and profile photo as a viewer.
2. Get the latest audio chat room list from the backend.
 >?The audio chat room list in the demo is for demonstration only. The logic of audio chat room lists varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
 >
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by anchors when they call `createRoom` to create the rooms.
 >!If your audio chat room list already displays enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select an audio chat room, call `enterRoom`, and pass in the room ID to enter the room.
5. After entry, you will receive an `onRoomInfoChange` notification about room change from the component. Note the information, including the room name displayed on the UI, whether anchor’s consent is required for viewers to speak, etc., and make changes accordingly.
6. You will receive an `onSeatListChange` notification about the seat change from the component. Update the change to the UI.
7. You will also receive an `onAnchorEnterSeat` notification about the seating of the anchor.

![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)
```
// 1. Set your nickname and profile photo as a viewer.
mTRTCVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2. Get the room list from the backend. Suppose it is `roomList`.
List<Integer> roomList = GetRoomList();

// 3. Call `getRoomInfoList` to get the details of the rooms.
mTRTCVoiceRoom.getRoomInfoList(roomList, new TRTCVoiceRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCVoiceRoomDef.RoomInfo> list) {
        if (code == 0) {
            // Refresh the room list on your UI.
        }
    }
});

// 4. Select an audio chat room, and pass in the `roomId` to enter it.
mTRTCVoiceRoom.enterRoom(roomId, new TRTCVoiceRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
                // Entered room successfully.
            }
        }
});

// 5. After entering the room, you receive an `onRoomInfoChange` notification.
@Override
public void onRoomInfoChange(TRTCVoiceRoomDef.RoomInfo roomInfo) {
    mNeedRequest = roomInfo.needRequest;
    mRoomName = roomInfo.roomName;
    // The UI can display the title and other information.
}

// 6. After entering the room, you receive an `onSeatListChange` notification.
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
    // Display the seat list.
}

// 7. You receive an `onAnchorEnterSeat` notification.
@Override
public void onAnchorEnterSeat(TRTCVoiceRoomDef.UserInfo userInfo) {
}
```

<span id="model.step7"></span>
### Step 7. Manage seats.

#### Anchor
1. An anchor can place a viewer in a seat by passing the `userId` of the viewer and the seat number in `pickSeat`. All members in the room will receive the `onSeatListChange` and `onAnchorEnterSeat` notifications.
2. An anchor can remove a user from a seat by passing the seat number in `kickSeat`. All members in the room will receive the `onSeatListChange` and `onAnchorLeaveSeat` notifications.
3. An anchor can mute or unmute a viewer by passing the number of the seat occupied by the viewer in `muteSeat`. All members in the room will receive the `onSeatListChange` and `onSeatMute` notifications.
4. An anchor can block or unblock a seat by passing the seat number in `closeSeat`. Viewers cannot take a blocked seat, and all members in the room will receive the `onSeatListChange` and `onSeatClose` notifications.

![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)
#### Viewer

1. A viewer can take a seat by passing the seat number in `enterSeat`. All members in the room will receive the `onSeatListChange` and `onAnchorEnterSeat` notifications.
2. A viewer can leave a seat by calling `leaveSeat`. All members in the room will receive the `onSeatListChange` and `onAnchorLeaveSeat` notifications.

![](https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png)

After a seat operation, the order in which different notifications are sent is: callbacks > `onSeatListChange` > independent events such as `onAnchorEnterSeat`.

```
// Case 1: the anchor places a viewer in seat 1.
mTRTCVoiceRoom.pickSeat(1, "123", new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. A callback is received.
        if (code == 0) {
        }
    }
});

// 3. The viewer receives the `onSeatListChange` callback and refreshes the seat list.
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}

// 4. The anchor receives a notification about the change of a specific seat, which can be used to determine whether the viewer has taken the seat.
public void onAnchorEnterSeat(int index, TRTCVoiceRoomDef.UserInfo user) {
}
```

```
// Case 2: a viewer takes seat 2.
mTRTCVoiceRoom.enterSeat(2, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. A callback is received.
        if (code == 0) {
        }
    }
});

// 3. The viewer receives the `onSeatListChange` callback and refreshes the seat list.
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}

// 4. The viewer receives a notification about the change of a specific seat and, depending on whether the seat is the one he or she attempted to take, determines the next step.
public void onAnchorEnterSeat(int index, TRTCVoiceRoomDef.UserInfo user) {
}
```


[](id:model.step8)
### Step 8. Use signaling for invitations.
In [seat management](#model.step7), viewers can take and leave seats without the anchor’s permission, and the anchor can place viewers in seats without the viewers’ consent.
If you want viewers and anchors to obtain each other’s consent before performing the above actions in your app, you can use invitation signaling.

### Viewer requesting to take seat
1. A viewer calls `sendInvitation` and passes in information including the anchor’s `userId` and custom command words. The function will return an `inviteId`, which should be noted.
2. The anchor receives an `onReceiveNewInvitation` notification, and a window pops up on the UI asking the anchor whether to approve the request.
3. The anchor approves the request, calls `acceptInvitation` and passes in the `inviteId`.
4. The viewer receives a `onInviteeAccepted` notification and calls `enterSeat` to take the seat.

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

```
// Viewer
// 1. Call `sendInvitation` to request to take seat 1.
String inviteId = mTRTCVoiceRoom.sendInvitation("ENTER_SEAT", ownerUserId, "1", null);

// 4. Take the seat upon receiving approval from the anchor.
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.enterSeat(1, null);
    }
}

// Anchor
// 2. Receive the request.
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("ENTER_SEAT")) {
        // 3. Approve the request.
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
```
#### Anchor inviting viewer to seat
1. The anchor calls `sendInvitation` and passes in information including the viewer’s `userId` and custom command words. The function will return an `inviteId`, which should be noted.
2. The viewer receives an `onReceiveNewInvitation` notification, and a window pops up asking the viewer whether to agree to take the seat.
3. The viewer agrees, calls `acceptInvitation`, and passes in the `inviteId`.
4. The anchor receives an `onInviteeAccepted` notification and calls `pickSeat` to place the viewer in the seat.

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)

```
// Anchor
// 1. Call `sendInvitation` to request to place viewer `123` in seat 2.
String inviteId = mTRTCVoiceRoom.sendInvitation("PICK_SEAT", "123", "2", null);

// 4. Seat the viewer upon receiving approval from the viewer.
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.pickSeat(2, null);
    }
}

// Viewer
// 2. Receive the request.
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("PICK_SEAT")) {
        // 3. Approve the request.
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
```


[](id:model.step9)
### Step 9. Enable text chat and on-screen comments.
- Call `sendRoomTextMsg` to send common text messages. All anchors and viewers in the room will receive the `onRecvRoomTextMsg` callback.
 IM has its default content moderation rules. Text messages that contain blocked terms will not be forwarded by the cloud.
```
// Sender: send text messages
mTRTCVoiceRoom.sendRoomTextMsg("Hello Word!", null);
// Recipient: listen for text messages
mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    @Override
    public void onRecvRoomTextMsg(String message, TRTCVoiceRoomDef.UserInfo userInfo) {
        Log.d(TAG, "Received a message from" + userInfo.userName + ":" + message);
    }
});
```
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All anchors and viewers in the room will receive the `onRecvRoomCustomMsg` callback.
Custom messages are often used to transfer custom signals, e.g., sending and broadcasting likes.
```
// Sender: customize CMD to distinguish on-screen comments and likes
// E.g., use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes.
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// Recipient: listen for custom messages
mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCVoiceRoomDef.UserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // Receive an on-screen comment.
            Log.d(TAG, "Received an on-screen comment from" + userInfo.userName + ":" + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // Receive a like.
            Log.d(TAG, userInfo.userName + "liked you.");
        }
    }
});
```
