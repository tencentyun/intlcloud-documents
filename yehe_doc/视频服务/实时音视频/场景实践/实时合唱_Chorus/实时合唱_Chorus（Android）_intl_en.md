## Demo UI
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC’s duet features, including low-latency karaoke, seat management, gift sending and receiving, text chat, etc.
<table>
     <tr>
         <th>Room Owner</th>  
         <th>Listener</th>  
     </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/206ba3492f4a2f18f36b1d5cba4e5558.jpg"/></td>
<td><img src="https://main.qcloudimg.com/raw/e52ccb64cd686f6af1c1f561d7969d36.jpg"/></td>
</tr>
</table>


To quickly enable the duet feature, you can modify the demo app we provide and adapt it to your needs. You may also use the `TUIChorus` component and customize your own UI.

[](id:DemoUI)
## Using the Demo App’s UI

[](id:ui.step1)
### Step 1. Create an application
1. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestChorus` and click **Create**.
3. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)
### Step 2. Download the app source code
Click [TUIChorus](https://github.com/tencentyun/TUIChorus) to clone or download the source code.

[](id:ui.step3)
### Step 3. Configure app project files
1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open `Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java`.
3. Set parameters in `GenerateTestUserSig.java`:
<ul style="margin:0"><li/>SDKAPPID: a placeholder by default. Set it to the actual `SDKAppID`.
<li>SECRETKEY: a placeholder by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.


>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the demo app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the demo app
Open the source code project `TUIChorus` with Android Studio (version 3.5 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the demo app’s source code
The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code. The table below lists the files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|-------|--------|
| base | Basic classes used by the UI |
| room | Main room views for room owner and listener |
| widget | Common controls |

## Tryout
>! You need at least two devices to try out the demo app.

### User A
1. Enter a username (**which must be unique**) and log in.
2. Click **Create Room**.
3. Enter a room subject and tap **Join**.

### User B
1. Enter a username (**which must be unique**) and log in.
2. Enter the ID of the room created by user A and tap **Join**.

>! You can find the room ID at the top of user A’s room view.



[](id:model)

## Customizing UI

The `Source` folder in the [source code](https://github.com/tencentyun/TUIChorus/tree/main/Android/Source/src/main/java/com/tencent/liteav/trtcChorus) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCChorusRoom`. You can find the component’s APIs in `TRTCChorusRoom.java` and use them to customize your own UI.
<img src="https://main.qcloudimg.com/raw/7613bd7ec5b4e665f32ee5df69e5de85.png">

[](id:model.step1)
### Step 1. Integrate the SDKs
The `TRTCChorusRoom` component depends on the TRTC SDK and IM SDK. Follow the steps below to integrate them into your project.

**Method 1: adding dependencies via Maven**
1. Add the TRTC SDK and IM SDK dependencies to `dependencies`.
<dx-codeblock>
::: java java
    dependencies {
       complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       complie 'com.tencent.imsdk:imsdk:latest.release'
       complie 'com.google.code.gson:gson:2.3.1'
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
### Step 3. Import the `TRTCChorus` component
Copy all the files in the directory below to your project:
<dx-codeblock>
::: java java
Source/src/main/java/com/tencent/liteav/tuichorus/model
:::
</dx-codeblock>

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` API to create an instance of the `TRTCChorus` component.
2. Call the `setDelegate` function to register event callbacks of the component.
3. Call the `login` function to log in to the component, and set the key parameters as described below.
 <table>
<tr>
<th>Parameter Name</th>
<th>Description</th>
</tr>
<tr>
<td>SDKAppID</td>
<td>You can view `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr>
<tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_)</td>
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
TRTCChorus mTRTCChorusRoom = TRTCChorusRoom.sharedInstance(this);
mTRTCChorusRoom.setDelegate(this);
mTRTCChorusRoom.login(SDKAPPID, userId, userSig, new TRTCChorusRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            //Login successful
        }
    }
});
:::
</dx-codeblock>

[](id:model.step5)
### Step 5. Create a room and become a speaker
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Call `createRoom` to create a room, passing in room attributes such as room ID, whether listeners need the room owner’s consent to speak, and the number of seats.
3. After creating the room, call `enterSeat` to take seat No. 1.
4. You will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
5. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat, and mic capturing will be enabled automatically.

![](https://qcloudimg.tencent-cloud.cn/raw/7346adee3042426ca4c9f72777cebd2d.png)


<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo
mTRTCChorusRoom.setSelfProfile("my_name", "my_face_url", null);

// 2. Call `createRoom` to create a room
final TRTCChorusRoomDef.RoomParam roomParam = new TRTCChorusRoomDef.RoomParam();
roomParam.roomName = "Room name";
roomParam.needRequest = false; // Whether your consent is required for listeners to speak
roomParam.seatCount = 7; // Number of room seats. In this example, the number is 7. 6 seats are available after you take one.
roomParam.coverUrl = "URL of room cover image";
mTRTCChorusRoom.createRoom(mRoomId, roomParam, new TRTCChorusRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. Take seat 0
            mTRTCChorusRoom.enterSeat(0, new TRTCChorusRoomCallback.ActionCallback() {
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
public void onSeatListChange(final List<TRTCChorusRoomDef.SeatInfo> seatInfoList) {
    // Display the seat list
}

// 5. You receive an `onAnchorEnterSeat` notification
@Override
public void onAnchorEnterSeat(TRTCChorusRoomDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step6)
### Step 6. Enter a room as a listener
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest room list from the backend.
>?The room list in the demo app is for demonstration only. The business logic of room lists varies significantly. Tencent Cloud does not provide room list management services currently. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by room owners when they call `createRoom`.
>!If your room list already contains enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select a room, and call `enterRoom` with the room ID passed in to enter.
5. After entering the room, you will receive an `onRoomInfoChange` notification about room change from the component. Record the room information, including room name, whether the room owner’s consent is required for listeners to speak, etc., and update it to the UI.
6. You will receive an `onSeatListChange` notification about seat change from the component. Update the change to the UI.
7. You will also receive an `onAnchorEnterSeat` notification that someone becomes a speaker.

![](https://qcloudimg.tencent-cloud.cn/raw/f225633062cf83d749ae8137cbb26fe1.png)
<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo
mTRTCChorusRoom.setSelfProfile("my_name", "my_face_url", null);

// 2. Get the room list from the backend. Suppose it is `roomList`.
List<Integer> roomList = GetRoomList();

// 3. Call `getRoomInfoList` to get details of the rooms
mTRTCChorusRoom.getRoomInfoList(roomList, new TRTCChorusRoomCallback.RoomInfoCallback() {
    @Override
    public void onCallback(int code, String msg, List<TRTCChorusRoomDef.RoomInfo> list) {
        if (code == 0) {
            // Refresh the room list on your UI
        }
    }
});

// 4. Select a room, passing in `roomId` to enter
mTRTCChorusRoom.enterRoom(roomId, new TRTCChorusRoomCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
                // Entered room successfully
            }
        }
});

// 5. After entering the room, you receive an `onRoomInfoChange` notification
@Override
public void onRoomInfoChange(TRTCChorusRoomDef.RoomInfo roomInfo) {
    mNeedRequest = roomInfo.needRequest;
    mRoomName = roomInfo.roomName;
    // The UI can display the title and other information
}

// 6. You receive an `onSeatListChange` notification
@Override
public void onSeatListChange(final List<TRTCChorusRoomDef.SeatInfo> seatInfoList) {
    // Display the seat list
}

// 7. You receive an `onAnchorEnterSeat` notification
@Override
public void onAnchorEnterSeat(TRTCChorusRoomDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step7)
### Step 7. Manage seats

<dx-tabs>
::: Room owner
1. Call `pickSeat`, passing in a seat number and the `userId` of a listener to place the listener in the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. Call `kickSeat`, passing in a seat number to remove the speaker from the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.
3. Call `closeSeat`, passing in a seat number to block/unblock the seat. Listeners cannot take a blocked seat, and all users in the room will receive an `onSeatListChange` notification and an `onSeatClose` notification.
![](https://qcloudimg.tencent-cloud.cn/raw/bbb72bdc50cfd1b5d4b567239b035d32.png)

:::
::: Listener

1. Call `enterSeat`, passing in a seat number to take the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. Call `leaveSeat` to leave your seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

![](https://qcloudimg.tencent-cloud.cn/raw/9747219d17f955530c5e502745008dce.png)

After a seat operation, the order in which different notifications are sent is: callbacks > `onSeatListChange` > independent events such as `onAnchorEnterSeat`.

<dx-codeblock>
::: java java
// 1. The room owner places a user in seat No. 1
mTRTCChorusRoom.pickSeat(1, "123", new TRTCChorusRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. A callback is returned
        if (code == 0) {
        }
    }
});

// 3. The room owner receives the `onSeatListChange` callback, and refreshes the seat list
@Override
public void onSeatListChange(final List<TRTCChorusRoomDef.SeatInfo> seatInfoList) {
}

// 4. The room owner receives a notification about the change of a specific seat, which can be used to determine whether the user has taken the seat
public void onAnchorEnterSeat(int index, TRTCChorusRoomDef.UserInfo user) {
}
:::
</dx-codeblock>

<dx-codeblock>
::: java java
// 1. A listener takes the co-singer seat
mTRTCChorusRoom.enterSeat(1, new TRTCChorusRoomCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. A callback is returned
        if (code == 0) {
        }
    }
});

// 3. The listener receives the `onSeatListChange` callback, and refreshes the seat list
@Override
public void onSeatListChange(final List<TRTCChorusRoomDef.SeatInfo> seatInfoList) {
}

// 4. The listener receives a notification about the change of a specific seat and can determine whether he or she has taken the seat successfully
public void onAnchorEnterSeat(int index, TRTCChorusRoomDef.UserInfo user) {
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

![](https://qcloudimg.tencent-cloud.cn/raw/1b37fa84f59c81dc89bf50ce4e30551f.png)

<dx-codeblock>
::: java java
// Listener
// 1. Call `sendInvitation` to request to take seat 1
String inviteId = mTRTCChorusRoom.sendInvitation("ENTER_SEAT", ownerUserId, "1", null);

// 2. Take the seat after the request is accepted by the room owner
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCChorusRoom.enterSeat(1, null);
    }
}

// Room owner
// 1. Receive the request
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("ENTER_SEAT")) {
        // 2. Accept the request
         mTRTCChorusRoom.acceptInvitation(id, null);
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

![](https://qcloudimg.tencent-cloud.cn/raw/3a8b31dac680c70d1adac92287e645dd.png)

<dx-codeblock>
::: java java
// Room owner
// 1. Call `sendInvitation` to invite user `123` to take the co-singer seat
String inviteId = mTRTCChorusRoom.sendInvitation("PICK_SEAT", "123", "1", null);

// 2. Place the user in the seat after the invitation is accepted
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCChorusRoom.pickSeat(2, null);
    }
}

// Listener
// 1. Receive the invitation
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("PICK_SEAT")) {
        // 2. Accept the invitation
         mTRTCChorusRoom.acceptInvitation(id, null);
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
  mTRTCChorusRoom.sendRoomTextMsg("Hello Word!", null);
  // Recipient: listen for text messages
  mTRTCChorusRoom.setDelegate(new TRTCChorusRoomDelegate() {
    @Override
    public void onRecvRoomTextMsg(String message, TRTCChorusRoomDef.UserInfo userInfo) {
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
// For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes
mTRTCChorusRoom.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
mTRTCChorusRoom.sendRoomCustomMsg("CMD_LIKE", "", null);
// Recipient: listen for custom messages
mTRTCChorusRoom.setDelegate(new TRTCChorusRoomDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCChorusRoomDef.UserInfo userInfo) {
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
