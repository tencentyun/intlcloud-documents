## Demo UI

You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo app we provide to try out TRTC features in the chat salon scenario, including audio chat, mic on/off, low-latency audio interaction, etc.

<table>
     <tr>
         <th>Room Owner</th>  
         <th>Listener</th>  
     </tr>
<tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/849c3cff658d82b0fe0d3e7b1a490e13.png"/ style="max-height:700px;"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/25cc9b7695cc208c946b50710e842e41.png"/  style="max-height:700px;"></td>
</tr>
</table>

To quickly enable the chat salon feature, you can modify the demo app we provide and adapt it to your needs. You may also use the `TUIChatSalon` component and customize your own UI.

[](id:DemoUI)
## Using the App’s UI

[](id:ui.step1)
### Step 1. Create an application
1. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TRTCChatSalon` and click **Create**.
3. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)
>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)
### Step 2. Download the application source code
Click [TUIChatSalon](https://github.com/tencentyun/TUIChatSalon) to clone or download the source code.

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
Open the source code project `TUIChatSalon` with Android Studio (version 3.5 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the app’s source code
The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code. The table below lists the files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
| ------------ | ------------------------------------ |
| base | Basic classes used by the UI |
| list | Room creation page. |
| room | The main room views for room owner and listener |
| widget | Common controls |


## Tryout
>! You need at least two devices to try out the application.

### User A

1. Enter a username (**which must be unique**) and log in.

   ![](https://qcloudimg.tencent-cloud.cn/raw/ae3d6bc2f1900dbc5537f2f3f4fca529.png)

2. Click **Create Room**.

   ![](https://qcloudimg.tencent-cloud.cn/raw/aef2012fdb5a6441dae9406f0539164d.png)

3. Type a subject for the conference and tap **Let’s go**.

### User B
1. Enter a username (**which must be unique**) and log in.

   ![](https://qcloudimg.tencent-cloud.cn/raw/7596d1bd53d84d61436a499a92d52240.png)

2. Enter the ID of the room created by user A and tap **Join**.<br>

   ![](https://qcloudimg.tencent-cloud.cn/raw/68eea3143e1d57158725d80da7895e51.png)

>! You can find the room ID at the top of user A’s room view.
>
>![](https://qcloudimg.tencent-cloud.cn/raw/ae36a652f641761fccd5bdad041a9220.png)

[](id:model)

## Customizing Your Own UI
The `Source` folder in the [source code](https://github.com/tencentyun/TUIChatSalon/tree/main/Android/Source/src/main/java/com/tencent/liteav/trtcchatsalon) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCChatSalon`. You can find the component’s APIs in `TRTCChatSalon.java` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png)

[](id:model.step1)
### Step 1. Integrate the SDKs

The chat salon component's `Source` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate them into your project.

[](id:model.step1_m1)
#### Method 1: adding dependencies via Maven
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

[](id:model.step1_m2)
#### Method 2: adding dependencies through local AAR files
If your access to the Maven repository is slow, you can download the ZIP files of the SDKs and manually integrate them into your project as instructed in the documents below.

<table>
<tr><th>SDK</th><th>Download Page</th><th>Integration Guide</th>
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

Configure permission requests for your app in `AndroidManifest.xml`. The SDKs need the following permissions (on Android 6.0 and above, the read storage permissions must be requested at runtime):

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
### Step 3. Import the `TRTCChatSalon` component
Copy all the files in the directory below to your project:
<dx-codeblock>
::: java java
Source/src/main/java/com/tencent/liteav/trtcchatsalon/model
:::
</dx-codeblock>

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` API to create an instance of the `TRTCChatSalon` component.
2. Call the `setDelegate` API to register event callbacks of the component.
3. Call the `login` API to log in to the component, and set the key parameters as described below.
 <table>
<tr><th>Parameter</th><th>Description</th></tr><tr>
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
TRTCChatSalon mTRTCChatSalon = TRTCChatSalon.sharedInstance(this);
mTRTCChatSalon.setDelegate(this);
mTRTCChatSalon.login(SDKAPPID, userId, userSig, new TRTCChatSalonCallback.ActionCallback() {
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
2. Call `createRoom` to create a chat salon, passing in room-related parameters such as room ID, whether your consent is required for listeners to speak, and the room type.
3. You will receive an `onAnchorEnterSeat` notification that someone becomes a speaker, and mic capturing will be enabled automatically.

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)
<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo.
mTRTCChatSalon.setSelfProfile("my_name", "my_face_url", null);

// 2. Call `createRoom` to create a room
final TRTCChatSalonDef.RoomParam roomParam = new TRTCChatSalonDef.RoomParam();
roomParam.roomName = "Room name";
roomParam.needRequest = true; // Whether your consent is required for listeners to speak
roomParam.coverUrl = "URL of room cover image";
mTRTCChatSalon.createRoom(mRoomId, roomParam, new TRTCChatSalonCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        if (code == 0) {
            // 3. Become a speaker
            mTRTCChatSalon.enterSeat(new TRTCChatSalonCallback.ActionCallback() {
                @Override
                public void onCallback(int code, String msg) {
                    if (code == 0) {
                    }
                }
            });
        }
    }
});

// 4. You receive an `onAnchorEnterSeat` notification after becoming a speaker
@Override
public void onAnchorEnterSeat(TRTCChatSalonDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step6)
### Step 6. Enter a room as a listener

1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest chat salon room list from the backend.
>?The chat salon list in the demo app is for demonstration only. The business logic of the chat salon list varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by room owners when they call `createRoom`.
>!If your chat salon list already contains enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select a chat salon, and call `enterRoom` with the room ID passed in to enter.
5. After entering the room, you will receive an `onRoomInfoChange` notification about room change from the component. Record the room information, including room name, whether the room owner’s consent is required for listeners to speak, etc., and update it to the UI.
6. You will also receive an `onAnchorEnterSeat` notification that someone becomes a speaker.

![](https://main.qcloudimg.com/raw/117b4dbdaf146cc89b681d067503f0f0.png)

<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo.
mTRTCChatSalon.setSelfProfile("my_name", "my_face_url", null);

// 2. Get the room list from the backend. Suppose it is `roomList`.
List<Integer> roomList = GetRoomList();

// 3. Call `getRoomInfoList` to get details of the rooms.
mTRTCChatSalon.getRoomInfoList(roomList, new TRTCChatSalonCallback.RoomInfoCallback() {

    @Override
    public void onCallback(int code, String msg, List<TRTCChatSalonDef.RoomInfo> list) {
        if (code == 0) {
            // Refresh the room list on your UI
        }
    }

});

// 4. Pass in `roomId` to enter a room.
mTRTCChatSalon.enterRoom(roomId, new TRTCChatSalonCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
                // Entered room successfully
            }
        }
});

// 5. After successful room entry, you receive an `onRoomInfoChange` notification.
@Override
public void onRoomInfoChange(TRTCChatSalonDef.RoomInfo roomInfo) {
    mNeedRequest = roomInfo.needRequest;
    mRoomName = roomInfo.roomName;
    // The UI can display the title and other information
}

// 6. You receive an `onAnchorEnterSeat` notification.
@Override
public void onAnchorEnterSeat(TRTCChatSalonDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step7)
### Step 7. Mic on/off

<dx-tabs>
::: Room owner
1. A room owner can make a listener speaker by passing in the `userId` of the listener to `pickSeat`. All members in the room will receive an `onAnchorEnterSeat` notification.
2. A room owner can remove a speaker by passing in the speaker’s `userId` to `kickSeat`. All members in the room will receive an `onAnchorLeaveSeat` notification.

![](https://qcloudimg.tencent-cloud.cn/raw/0eb3dbe14b166a24252f0efb45a6b24f.png)
After a speaker list operation, the order in which different notifications are sent is: callbacks > independent events such as `onAnchorEnterSeat`.
<dx-codeblock>
::: java java
// 1. The room owner makes a listener speaker.
mTRTCChatSalon.pickSeat("123", new TRTCChatSalonCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. A callback is returned.
        if (code == 0) {
        }
    }
});

// 3. The room owner receives a notification that someone became a speaker, and can determine whether it is the listener he or she intended to make speaker.
public void onAnchorEnterSeat(TRTCChatSalonDef.UserInfo user) {
}
:::
</dx-codeblock>
:::
::: Listener
1. A listener can become a speaker by calling `enterSeat`. All members in the room will receive an `onAnchorEnterSeat` notification.
2. A speaker can become a listener by calling `leaveSeat`. All members in the room will receive an `onAnchorLeaveSeat` notification.

![](https://main.qcloudimg.com/raw/c9611b5017536604f63333ce7c19c309.png)
After a speaker list operation, the order in which different notifications are sent is: callbacks > independent events such as `onAnchorEnterSeat`.
<dx-codeblock>
::: java java
// 1. A listener calls an API to become a speaker.
mTRTCChatSalon.enterSeat(new TRTCChatSalonCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. A callback is returned.
        if (code == 0) {
        }
    }
});

// 3. The listener receives a notification that someone became a speaker and can determine whether it is him/herself.
public void onAnchorEnterSeat(int index, TRTCChatSalonDef.UserInfo user) {
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step8)
### Step 8. Use signaling for invitations
If you want listeners and room owners to obtain each other’s consent before performing the above actions in your application, you can use signaling for invitation sending.

<dx-tabs>
::: Listener requesting to take seat
1. A listener calls `sendInvitation`, passing in information including the room owner’s `userId` and custom command words. The API will return an `inviteId`, which should be recorded.
2. The room owner receives an `onReceiveNewInvitation` notification, and a window pops up on the UI asking the room owner whether to accept the request.
3. The room owner calls `acceptInvitation` with the `inviteId` passed in to accept the request.
4. The listener receives an `onInviteeAccepted` notification and calls `enterSeat` to become a speaker.

![](https://main.qcloudimg.com/raw/3543bf768896cfd78b0163dc9378e659.png)

<dx-codeblock>
::: java java
// Listener
// 1. A listener calls `sendInvitation` to request to speak.
String inviteId = mTRTCChatSalon.sendInvitation("ENTER_SEAT", ownerUserId, "123", null);

// 2. Place the user in the seat after the invitation is accepted
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCChatSalon.enterSeat(null);
    }
}

// Room owner
// 1. The room owner receives the request.
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("ENTER_SEAT")) {
        // 2. The room owner accepts the request.
         mTRTCChatSalon.acceptInvitation(id, null);
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

![](https://main.qcloudimg.com/raw/60025544abae69e22de22a4b81bf6951.png)

<dx-codeblock>
::: java java
// Room owner
// 1. The room owner calls `sendInvitation` to invite user `123` to speak.
String inviteId = mTRTCChatSalon.sendInvitation("PICK_SEAT", ownerUserId, "123", null);

// 2. Place the user in the seat after the invitation is accepted
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCChatSalon.pickSeat(null);
    }
}

// Listener
// 1. The listener receives the invitation.
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("PICK_SEAT")) {
        // 2. The listener accepts the invitation.
         mTRTCChatSalon.acceptInvitation(id, null);
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
  mTRTCChatSalon.sendRoomTextMsg("Hello Word!", null);
  // Recipient: listen for text messages
  mTRTCChatSalon.setDelegate(new TRTCChatSalonDelegate() {
   @Override
   public void onRecvRoomTextMsg(String message, TRTCChatSalonDef.UserInfo userInfo) {
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
  mTRTCChatSalon.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
  mTRTCChatSalon.sendRoomCustomMsg("CMD_LIKE", "", null);
  // Recipient: listen for custom messages
  mTRTCChatSalon.setDelegate(new TRTCChatSalonDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCChatSalonDef.UserInfo userInfo) {
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
