## Demonstration

You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC features in the chat salon scenario, including audio chat, mic on/off, low-latency audio interaction, etc.

To quickly enable the chat salon feature, you can modify the demo we provide and adapt it to your needs. You may also use the `TRTCChatSalon` component and customize your own UI.

[](id:DemoUI)
## Using the Demo UI

[](id:ui.step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g., `TestChatSalon`, and click **Create**.

>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)

### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code for your platform.
2. Click **Next**.
![](https://main.qcloudimg.com/raw/3b115019ddfd0866108ed1add30810d8.png)

[](id:ui.step3)

### Step 3. Configure demo project files

1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open the `Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java` file.
3. Set parameters in `GenerateTestUserSig.java` as follows.
<ul style="margin:0"><li/>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/586439966d8588888cecf80d3bb4fe46.png">
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.


>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4: run the demo
Open the `TRTCScenesDemo` project with Android Studio (version 3.5 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the demo source code
The `trtcliveroomdemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code. The table below lists the files (folders) and UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
| ------------ | ------------------------------------ |
| base | Basic classes used by the UI |
| list | The list and room creation views |
| room | The main room views for room owner and listener |
| widget | Common controls |

[](id:model)
## Customizing UI
The `trtcchatsalondemo` folder in the [source code](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCScenesDemo/trtcmeetingdemo/src/main/java/com/tencent/liteav/meeting) contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCChatSalon`. You can find the component’s API functions in `TRTCChatSalon.java` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/fcf694c8550664623414604d14ffcd94.png)

[](id:model.step1)
### Step 1. Integrate the SDKs

The chat salon component `trtcchatsalondemo` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project.

[](id:model.step1_m1)
#### Method 1: adding dependencies via Maven
1. Add the TRTC SDK and IM SDK dependencies to `dependencies`.
```
dependencies {
       complie "com.tencent.liteav:LiteAVSDK_TRTC:latest.release"
       complie 'com.tencent.imsdk:imsdk:latest.release'
       compile 'com.google.code.gson:gson:2.3.1'
}
```
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).
2. In `defaultConfig`, specify the CPU architecture to be used by the app.
```
defaultConfig {
      ndk {
          abiFilters "armeabi-v7a"
      }
}
```
3. Click **Sync Now** to automatically download the SDKs and integrate them into the project.

[](id:model.step1_m2)
#### Method 2: adding dependencies through local AAR**
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
### Step 3. Import the `TRTCChatSalon` component
Copy all the files in the following directory to your project:
```
trtcchatsalondemo/src/main/java/com/tencent/liteav/trtcchatsalon/model
```

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` API to create an instance of the `TRTCChatSalon` component.
2. Call the `setDelegate` function to register event callbacks of the component.
3. Call the `login` function to log in to the component, and set the key parameters as described below.
 <table>
<tr><th>Parameter</th><th>Description</th></tr><tr>
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

![](https://main.qcloudimg.com/raw/bfdc392413adacb05325b065bc691c82.png)
<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo
mTRTCChatSalon.setSelfProfile("my_name", "my_face_url", null);

// 2. Call createRoom to create a room
final TRTCChatSalonDef.RoomParam roomParam = new TRTCChatSalonDef.RoomParam();
roomParam.roomName = "Room ID";
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

1. After performing [step 4](#model.step4) to log in, you can call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest chat salon room list from the backend.
 >?The chat salon list in the demo is for demonstration only. The business logic of the chat salon list varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by room owners when they call `createRoom` to create the rooms.
>!If your chat salon list already contains enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select a chat salon, and call `enterRoom` with the room ID passed in to enter.
5. After entering the room, you will receive an `onRoomInfoChange` notification about room change from the component. Record the room information, including room name, whether the room owner’s consent is required for listeners to speak, etc., and update it to the UI.
6. You will also receive an `onAnchorEnterSeat` notification that someone becomes a speaker.

![](https://main.qcloudimg.com/raw/24ba699e25f8a8cb2f892fbbf8d7fa00.png)

<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo
mTRTCChatSalon.setSelfProfile("my_name", "my_face_url", null);

// 2. Get the room list from the backend. Suppose it is `roomList`
List<Integer> roomList = GetRoomList();

// 3. Call `getRoomInfoList` to get the details of the rooms
mTRTCChatSalon.getRoomInfoList(roomList, new TRTCChatSalonCallback.RoomInfoCallback() {

    @Override
    public void onCallback(int code, String msg, List<TRTCChatSalonDef.RoomInfo> list) {
        if (code == 0) {
            // Refresh the room list on your UI
        }
    }

});

// 4. Pass in `roomid` to enter the room
mTRTCChatSalon.enterRoom(roomId, new TRTCChatSalonCallback.ActionCallback() {
        @Override
        public void onCallback(int code, String msg) {
            if (code == 0) {
                // Entered room
            }
        }
});

// 5. After successful room entry, you receive an `onRoomInfoChange` notification
@Override
public void onRoomInfoChange(TRTCChatSalonDef.RoomInfo roomInfo) {
    mNeedRequest = roomInfo.needRequest;
    mRoomName = roomInfo.roomName;
    // The UI can display the title and other information
}

// 6. You receive an `onAnchorEnterSeat` notification
@Override
public void onAnchorEnterSeat(TRTCChatSalonDef.UserInfo userInfo) {
}
:::
</dx-codeblock>

[](id:model.step7)

### Step 7. Mic on/off

<dx-tabs>
::: Room owner
1. A room owner can invite a listener to speak by passing in the `userId` of the listener to `pickSeat`. All members in the room will receive an `onAnchorEnterSeat` notification.
2. A room owner can remove a speaker by passing in the speaker’s `userId` to `kickSeat`. All members in the room will receive an `onAnchorLeaveSeat` notification.

![](https://main.qcloudimg.com/raw/6e23550a49c88b823dca96941c638394.png)
After a speaker list operation, the order in which different notifications are sent is: callbacks > independent events such as `onAnchorEnterSeat`.
<dx-codeblock>
::: java java
// 1. The room owner invites a listener to speak
mTRTCChatSalon.pickSeat("123", new TRTCChatSalonCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. The callback is received
        if (code == 0) {
        }
    }
});

// 3. The room owner receives a notification that someone became a speaker, and can determine whether it is the listener he or she invited
public void onAnchorEnterSeat(TRTCChatSalonDef.UserInfo user) {
}
:::
</dx-codeblock>
:::
::: Listener
1. A listener can become a speaker by calling `enterSeat`. All members in the room will receive an `onAnchorEnterSeat` notification.
2. A speaker can become a listener by calling `leaveSeat`. All members in the room will receive an `onAnchorLeaveSeat` notification.

![](https://main.qcloudimg.com/raw/d6a618277eb66ba629e9172844c57a60.png)
After a speaker list operation, the order in which different notifications are sent is: callbacks > independent events such as `onAnchorEnterSeat`.
<dx-codeblock>
::: java java
// 1. The listener becomes a speaker
mTRTCChatSalon.enterSeat(new TRTCChatSalonCallback.ActionCallback() {
    @Override
    public void onCallback(int code, String msg) {
        // 2. The callback is received
        if (code == 0) {
        }
    }
});

// 3. The listener receives a notification that someone became a speaker and can determine whether it is him/herself
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
::: Listener requesting to speak
1. A listener calls `sendInvitation`, passing in information including the room owner's `userId` and custom command words. The function will return an `inviteId`, which should be recorded.
2. The room owner receives an `onReceiveNewInvitation` notification, and a window pops up on the UI asking the room owner whether to accept the request.
3. The room owner calls `acceptInvitation` with the `inviteId` passed in to accept the request.
4. The listener receives an `onInviteeAccepted` notification and calls `enterSeat` to become a speaker.

![](https://main.qcloudimg.com/raw/1553acebea8b5a35b1b8e82365bdec3c.png)

<dx-codeblock>
::: java java
// Listener
// 1. Call `sendInvitation` to request to speak
String inviteId = mTRTCChatSalon.sendInvitation("ENTER_SEAT", ownerUserId, "123", null);

// 2. Become a speaker when the request is accepted by the room owner
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCChatSalon.enterSeat(null);
    }
}

// Room owner
// 1. Receive the request
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("ENTER_SEAT")) {
        // 2. Accept the request
         mTRTCChatSalon.acceptInvitation(id, null);
    }
}
:::
</dx-codeblock>
:::
::: Room owner inviting listener to speak
1. The room owner calls `sendInvitation`, passing in information including the listener's `userId` and custom command words. The function will return an `inviteId`, which should be recorded.
2. The listener receives an `onReceiveNewInvitation` notification, and a window pops up asking the listener whether to accept the invitation.
3. The listener calls `acceptInvitation` with the `inviteId` passed in to accept the invitation.
4. The room owner receives an `onInviteeAccepted` notification and calls `pickSeat` to make the listener a speaker.

![](https://main.qcloudimg.com/raw/7b920cb763f049c4d90a84c72ab4c87e.png)

<dx-codeblock>
::: java java
// Room owner
// 1. Call `sendInvitation` to invite user `123` to speak
String inviteId = mTRTCChatSalon.sendInvitation("PICK_SEAT", ownerUserId, "123", null);

// 2. Make the listener a speaker when the invitation is accepted by the listener
@Override
public void onInviteeAccepted(String id, String invitee) {
    if(id.equals(inviteId)) {
        mTRTCChatSalon.pickSeat(null);
    }
}

// Listener
// 1. Receive the invitation
 @Override
public void onReceiveNewInvitation(final String id, String inviter, String cmd, final String content) {
    if (cmd.equals("PICK_SEAT")) {
        // 2. Accept the invitation
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
       Log.d(TAG, "Received a message from" + userInfo.userName + ":" + message);
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
  mTRTCChatSalon.sendRoomCustomMsg("CMD_DANMU", "Hello world", null);
  mTRTCChatSalon.sendRoomCustomMsg("CMD_LIKE", "", null);
  // Recipient: listen for custom messages
  mTRTCChatSalon.setDelegate(new TRTCChatSalonDelegate() {
    @Override
    public void onRecvRoomCustomMsg(String cmd, String message, TRTCChatSalonDef.UserInfo userInfo) {
        if ("CMD_DANMU".equals(cmd)) {
            // Received an on-screen comment
            Log.d(TAG, "Received an on-screen comment from" + userInfo.userName + ":" + message);
        } else if ("CMD_LIKE".equals(cmd)) {
            // Received a like
            Log.d(TAG, userInfo.userName + "liked you.");
        }
    }
  });
  :::
  </dx-codeblock>

