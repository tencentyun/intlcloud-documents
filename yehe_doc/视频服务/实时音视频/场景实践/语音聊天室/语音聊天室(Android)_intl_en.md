## Demonstration
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC’s audio chat room features, including seat management, low-latency audio interaction, text chat, etc.


To quickly implement the audio chat room feature, you can modify the demo we provide and adapt it to your needs. You can also use the `TRTCVoiceRoom` component and customize your own UI.

[](id:DemoUI)
## Using the Demo UI

[](id:ui.step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g. `TestVoiceRoom`, and click **Create**.

>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code for your platform.
2. Click **Next**.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:ui.step3)
### Step 3. Configure demo project files.
1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open the `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` file.
3. Set parameters in `GenerateTestUserSig.java`:
<ul style="margin:0"><li/>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.


>!The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the demo
Open the `TRTCScenesDemo` project with Android Studio (version 3.5 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the demo source code
The `trtcvoiceroomdemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code. The table below lists the files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|-------|--------|
| base | Basic classes used by the UI |
| list | List view and room creation view |
| room | Main room views for room owner and listener |
| widget | Common controls |

[](id:model)
## Customizing UI

The `trtcvoiceroomdemo` folder in the [source code](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo/trtcvoiceroomdemo/src/main/java/com/tencent/liteav/trtcvoiceroom) contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCVoiceRoom`. You can find the component’s APIs in `TRTCVoiceRoom.java` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)

[](id:model.step1)
### Step 1. Integrate the SDKs
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
2. In `defaultConfig`, specify the CPU architecture to be used by your application.
```
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
```
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
### Step 3. Import the `TRTCVoiceRoom` component
Copy all the files in the directory below to your project:
```
trtcvoiceroomdemo/src/main/java/com/tencent/liteav/trtcvoiceroom/model
```

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` API to create an instance of the `TRTCVoiceRoom` component.
2. Call the `setDelegate` function to register event callbacks of the component.
3. Call the `login` function to log in to the component. Set the key parameters as described below.
 <table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>SDKAppID</td>
<td>You can view the `SDKAppID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
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
<dx-codeblock>
::: java java
TRTCVoiceRoom mTRTCVoiceRoom = TRTCVoiceRoom.sharedInstance(this);
mTRTCVoiceRoom.setDelegate(this);
mTRTCVoiceRoom.login(SDKAPPID, userId, userSig, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {![](https://main.qcloudimg.com/raw/be8ee8461f8e06295d5ae1ad1502d745.png)
            // Logged in
        }
    }
});
:::
</dx-codeblock>

[](id:model.step5)
### Step 5. Create a room and become a speaker
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Call `createRoom` to create an audio chat room and pass in room-related parameters such as room ID, whether to request your consent for listeners to speak, and the number of seats.
3. After creating the room, call `enterSeat` to take a seat.
4. You will receive an `onSeatListChange` notification about seat change from the component. Update the change to the UI.
5. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat, and mic capturing will be enabled automatically.

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)


<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo
mTRTCVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2. Call `createRoom` to create a room
final TRTCVoiceRoomDef.RoomParam roomParam = new TRTCVoiceRoomDef.RoomParam();
roomParam.roomName = "Room ID";
roomParam.needRequest = false; // Whether your consent is required for listeners to speak
roomParam.seatCount = 7; // Number of room seats. In this example, the number is 7. 6 seats are available after you take one.
roomParam.coverUrl = "room cover URL";
mTRTCVoiceRoom.createRoom(mRoomId, roomParam, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. Take seat 0
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

// 4. After taking a seat, you receive an `onSeatListChange` notification
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
    // Display the seat list.
}

// 5. You receive an `onAnchorEnterSeat` notification
@Override
public void onAnchorEnterSeat(TRTCVoiceRoomDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step6)
### Step 6. Enter a room as a listener
1. After performing [step 4](#model.step4) to log in, you can call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest audio chat room list from the backend.
 >?The audio chat room list in the demo is for demonstration only. The logic of audio chat room lists varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by the room owner during room creation via the calling of `createRoom`.
 >!If your audio chat room list already displays enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select an audio chat room, and call `enterRoom` with the room ID passed in to enter the room.
5. After entering the room, you will receive an `onRoomInfoChange` notification about room change from the component. Record the room information, including room name, whether the room owner’s consent is required for listeners to speak, etc., and update it to the UI.
6. You will receive an `onSeatListChange` notification about seat change from the component. Update the change to the UI.
7. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat.

![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)
<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo
mTRTCVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2. Get the room list from the backend. Suppose it is `roomList`.
List<Integer> roomList = GetRoomList();

// 3. Call `getRoomInfoList` to get details of the rooms
mTRTCVoiceRoom.getRoomInfoList(roomList, new TRTCVoiceRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCVoiceRoomDef.RoomInfo> list) {
        if (code == 0) {
            // Refresh the room list on your UI
        }
    }
});

// 4. Select an audio chat room, and pass in the `roomId` to enter it
mTRTCVoiceRoom.enterRoom(roomId, new TRTCVoiceRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
                // Entered room successfully
            }
        }
});

// 5. After successful room entry, you receive an `onRoomInfoChange` notification
@Override
public void onRoomInfoChange(TRTCVoiceRoomDef.RoomInfo roomInfo) {
    mNeedRequest = roomInfo.needRequest;
    mRoomName = roomInfo.roomName;
    // The UI can display the title and other information
}

// 6. After entering the room, you receive an `onSeatListChange` notification
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
    // Display the seat list
}

// 7. You receive an `onAnchorEnterSeat` notification
@Override
public void onAnchorEnterSeat(TRTCVoiceRoomDef.UserInfo userInfo) {
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
![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)

:::
::: Listener
1. A listener can take a seat by passing the seat number in `enterSeat`. All members in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. A listener can leave a seat by calling `leaveSeat`. All members in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

After a seat operation, the order in which different notifications are sent is: callbacks > `onSeatListChange` > independent events such as `onAnchorEnterSeat`.

<dx-codeblock>
::: java java
// 1. The room owner puts a user in seat 1
mTRTCVoiceRoom.pickSeat(1, "123", new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. A callback is returned
        if (code == 0) {
        }
    }
});

// 3. The anchor receives an `onSeatListChange` callback and refreshes the seat list
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}

// 4. The anchor receives a notification about the change of a specific seat, which can be used to determine whether the listener has taken the seat
public void onAnchorEnterSeat(int index, TRTCVoiceRoomDef.UserInfo user) {
}
:::
</dx-codeblock>

<dx-codeblock>
::: java java
// 1. A listener takes seat 2
mTRTCVoiceRoom.enterSeat(2, new TRTCVoiceRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. A callback is returned
        if (code == 0) {
        }
    }
});

// 3. The listener receives the `onSeatListChange` callback and refreshes the seat list
@Override
public void onSeatListChange(final List<TRTCVoiceRoomDef.SeatInfo> seatInfoList) {
}

// 4. The listener receives a notification about the change of a specific seat and can determine whether he or she has taken the seat successfully
public void onAnchorEnterSeat(int index, TRTCVoiceRoomDef.UserInfo user) {
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
4. The listener receives an `onInviteeAccepted` notification and calls `enterSeat` to take a seat.

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

<dx-codeblock>
::: java java
// Listener
// 1. Call `sendInvitation` to request to take seat 1
String inviteId = mTRTCVoiceRoom.sendInvitation("ENTER_SEAT", ownerUserId, "1", null);

// 2. Take the seat when the request is accepted by the room owner
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.enterSeat(1, null);
    }
}

// Room owner
// 1. Receive the request
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("ENTER_SEAT")) {
        // 2. Accept the request
         mTRTCVoiceRoom.acceptInvitation(id, null);
    }
}
:::
</dx-codeblock>
:::
::: Room owner inviting listener to take seat

1. The room owner calls `sendInvitation`, passing in information including the listener's `userId` and custom command words. The API will return an `inviteId`, which should be recorded.
2. The listener receives an `onReceiveNewInvitation` notification, and a window pops up asking the listener whether to agree to speak.
3. The listener agrees, and calls `acceptInvitation` with the `inviteId` passed in.
4. The room owner receives an `onInviteeAccepted` notification and calls `pickSeat` to put the listener in a seat.

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)

<dx-codeblock>
::: java java
// Room owner
// 1. Call `sendInvitation` to invite user `123` to take seat 2
String inviteId = mTRTCVoiceRoom.sendInvitation("PICK_SEAT", "123", "2", null);

// 2. Put the user in the seat when the invitation is accepted by the user
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCVoiceRoom.pickSeat(2, null);
    }
}

// Listener
// 1. Receive the request
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("PICK_SEAT")) {
        // 2. Accept the request
         mTRTCVoiceRoom.acceptInvitation(id, null);
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
 // Sender: sends text messages
 mTRTCVoiceRoom.sendRoomTextMsg("Hello Word!", null);
 // Recipient: listen for text messages
 mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    @Override
    public void onRecvRoomTextMsg(String message, TRTCVoiceRoomDef.UserInfo userInfo) {
        Log.d(TAG, "Received a message from" + userInfo.userName + ": " + message);
    }
 });
 :::
 </dx-codeblock>
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All users in the room will receive an `onRecvRoomCustomMsg` callback.
Custom messages are often used to transfer custom signals, e.g., giving and broadcasting likes.
<dx-codeblock>
::: java java
// A sender can customize commands to distinguish on-screen comments and likes
// For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mTRTCVoiceRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// Recipient: listen for custom messages
mTRTCVoiceRoom.setDelegate(new TRTCVoiceRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCVoiceRoomDef.UserInfo userInfo) {
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

