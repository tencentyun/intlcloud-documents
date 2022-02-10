## Demo UI

To quickly enable the chat salon feature, you can modify the demo we provide and adapt it to your needs. You may also use the `TRTCChatSalon` component and customize your own UI.

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

[](id:DemoUI)

## Using the Demo UI

[](id:ui.step1)
### Step 1. Create an application
1. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g., `TestChatSalon`, and click **Create**.

>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and [demo source code](https://github.com/tencentyun/TRTCFlutterScenesDemo) for your platform.
2. Click **Next**.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:ui.step3)
### Step 3. Configure the demo project file
1. In the **Modify Configuration** step, select your platform.
2. Find and open `/example/lib/debug/GenerateTestUserSig.dart`.
3. Set parameters in `GenerateTestUserSig.dart` as follows.
<ul><li/>SDKAPPID: a placeholder by default. Set it to the actual `SDKAppID`.
	<li>`SECRETKEY`: a placeholder by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png"/>

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Compile and run

>! An Android project must be run on a real device rather than a simulator.

1. Run `flutter pub get`.
2. Compile, run, and test the project.
<dx-tabs>
:::  Android\s
1. Run `flutter run`.
2. Open the demo project with Android Studio (3.5 or above), and click **Run**.
:::
::: iOS\s
1. Open `\ios project` in the source code directory with Xcode (11.0 or above).
2. Compile and run the demo project.
:::
</dx-tabs>

[](id:ui.step5)
### Step 5. Modify the demo source code
The `trtcchatsalondemo` folder in the [source code](https://github.com/tencentyun/TRTCFlutterScenesDemo) contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code. The table below lists the files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
| ------------ | ------------------------------------ |
| base | Basic classes used by the UI |
| list | The list and room creation views |
| room | The main room views for room owner and listener |
| widget | Common controls |

[](id:model)
## Customizing UI
The `trtcchatsalondemo` folder in the [source code](https://github.com/tencentyun/TRTCFlutterScenesDemo) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCChatSalon`. You can find the component's APIs in `TRTCChatSalon.dart` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/7613bd7ec5b4e665f32ee5df69e5de85.png)

[](id:model.step1)
### Step 1. Integrate the SDKs
The chat salon component `trtcchatsalondemo` depends on the [TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud) and [IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin). You can configure `pubspec.yaml` to download their updates automatically.

Add the following dependencies to `pubspec.yaml` of your project.
```
dependencies:
  tencent_trtc_cloud: latest version number
  tencent_im_sdk_plugin: latest version number
```

[](id:model.step2)

### Step 2. Configure permission requests and obfuscation rules
<dx-tabs>
::: iOS\s
Add requests for mic permission in `Info.plist`:
```
<key>NSMicrophoneUsageDescription</key>
<string>Audio calls are possible only with mic access.</string>
```
:::
::: Android\s
1. Open `/android/app/src/main/AndroidManifest.xml`.
2. Add `xmlns:tools="http://schemas.android.com/tools"` to `manifest`.
3. Add `tools:replace="android:label"` to `application`.
>? Without the above steps, the [Android Manifest merge failed](https://intl.cloud.tencent.com/document/product/647/39242) error will occur and the compilation will fail.

![Illustration](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)
:::
</dx-tabs>


[](id:model.step3)
### Step 3. Import the `TRTCChatSalon` component
Copy all the files in the directory below to your project:
```
lib/TRTCChatSalonDemo/model/
```

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` API to create an instance of the `TRTCChatSalon` component.
2. Call the `registerListener` function to register event callbacks of the component.
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
</table>

<dx-codeblock>
::: dart dart
TRTCChatSalon trtcVoiceRoom = await TRTCChatSalon.sharedInstance();
trtcVoiceRoom.registerListener(onVoiceListener);
ActionCallback resValue = await trtcVoiceRoom.login(
    GenerateTestUserSig.sdkAppId,
    userId,
    GenerateTestUserSig.genTestSig(userId),
);
if (resValue.code == 0) {
    // Logged in
}
:::
</dx-codeblock>

[](id:model.step5)

### Step 5. Create a room and become a speaker

1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Call `createRoom` to create a chat salon, passing in room attributes such as room ID and room name.
3. You will receive a `TRTCChatSalonDelegate.onAudienceEnter` notification that someone entered the room, and mic capturing will be enabled automatically.

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)

<dx-codeblock>
::: java java
// 1. Set your nickname and profile photo.
trtcVoiceRoom.setSelfProfile("my_name", "my_face_url", null);

// 2. Call `createRoom` to create a room
ActionCallback resp = await trtcVoiceRoom.createRoom(
    roomId,
    RoomParam(
    coverUrl: 'Room cover URL',
    roomName: 'Room name',
    ),
);
if (resp.code == 0) {
   //3. Become a speaker
}

// 4. Receive a `TRTCChatSalonDelegate.onAudienceEnter` notification
onVoiceListener(type, param) async {
    switch (type) {
        case TRTCChatSalonDelegate.onAudienceEnter:
            // A listener enters the room
            break;
    }
}
:::
</dx-codeblock>

[](id:model.step6)

### Step 6. Enter a room as a listener

1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest chat salon room list from the backend.
 >?The chat salon list in the demo is for demonstration only. The business logic of the chat salon list varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by the room owner during room creation via the calling of `createRoom`.
>!If your chat salon list already contains enough room information, you can skip the step of calling `getRoomList`. Just pass in the room ID to enter the room.
4. After room entry, you will receive the `TRTCChatSalonDelegate.onAudienceEnter` and `TRTCChatSalonDelegate.onAudienceExit` notifications about listeners’ entry/exit. Refresh the information on the UI accordingly.
5. You will also receive the `TRTCChatSalonDelegate.onAnchorEnterMic` and `TRTCChatSalonDelegate.onAnchorLeaveMic` notifications that someone becomes a speaker or listener.

![](https://main.qcloudimg.com/raw/6fbabfa4e217022cf3d05677e4a45538.png)
<dx-codeblock>
::: dart dart
// 1. Set your nickname and profile photo.
trtcVoiceRoom.setSelfProfile("my_name", "my_face_url");

// 2. Get the room list from the backend. Suppose it is `roomList`.
List<Integer> roomList = GetRoomList();

// 3. Call `getRoomInfoList` to get details of the rooms.
RoomInfoCallback resp = await trtcVoiceRoom.getRoomInfoList(roomList);
if (resp.code == 0) {
    //Refresh the room list on your UI
} 

// 4. Pass in `roomId` to enter a room.
ActionCallback enterRoomResp =
          await trtcVoiceRoom.enterRoom(_currentRoomId);
if (enterRoomResp.code == 0) {
    // Entered room successfully
}
// 5. After successful room entry, you receive an event notification
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onAudienceEnter:
            // A listener enters the room
        break;
      case TRTCChatSalonDelegate.onAudienceExit:
            //A listener leaves the room
        break;
      case TRTCChatSalonDelegate.onAnchorLeaveMic:
          //The room owner leaves the room
        break;
      case TRTCChatSalonDelegate.onAnchorEnterMic:
          //The room owner enters the room
        break;
    }
}
:::
</dx-codeblock>

[](id:model.step7)
### Step 7. Mic on/off
<dx-tabs>
::: Room owner
1. A room owner can call `leaveMic` to become a listener. All users in the room will receive an `onAnchorLeaveMic` notification.
2. A room owner can remove a speaker by passing in the speaker’s userId to `kickMic`. All users in the room will receive an `onAnchorLeaveMic` notification.

![](https://qcloudimg.tencent-cloud.cn/raw/0eb3dbe14b166a24252f0efb45a6b24f.png)
<dx-codeblock>
::: dart dart
// 1. Become a listener
trtcVoiceRoom.leaveMic();

//2. Remove a speaker
trtcVoiceRoom.kickMic(userId);
:::
</dx-codeblock>
:::
::: Listener
1. A listener can become a speaker by calling `enterMic`. All members in the room will receive an `onAnchorEnterMic` notification.
2. A speaker can become a listener by calling `leaveMic`. All members in the room will receive an `onAnchorLeaveMic` notification.

![](https://main.qcloudimg.com/raw/c9611b5017536604f63333ce7c19c309.png)
<dx-codeblock>
::: dart dart
// 1. A listener calls an API to become a speaker.
trtcVoiceRoom.enterMic();

// 2. Become a listener
trtcVoiceRoom.leaveMic();

:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step8)

### Step 8. Use signaling for invitations

If you want listeners and room owners to obtain each other’s consent before performing the above actions in your application, you can use signaling for invitation sending.

::: Listener requesting to speak

1. A listener calls `raiseHand` to request to speak.
2. The room owner receives an `onRaiseHand` notification, and a window pops up on the UI asking the room owner whether to accept the request.
3. The room owner accepts the request and calls `agreeToSpeak`, with the listener’s `userId` passed in.
4. The listener receives an `onAgreeToSpeak` notification and calls `enterMic` to become a speaker.

![](https://main.qcloudimg.com/raw/3543bf768896cfd78b0163dc9378e659.png)
<dx-codeblock>
::: dart dart
// Listener
// 1. A listener calls `sendInvitation` to request to speak.
trtcVoiceRoom.raiseHand();

// 2. Place the user in the seat after the invitation is accepted
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onRaiseHand:
           trtcVoiceRoom.enterMic();
        break;
    }
}

// Room owner
// 1. The room owner receives the request.
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onAgreeToSpeak:
           trtcVoiceRoom.agreeToSpeak();
        break;
    }
}
:::
</dx-codeblock>

[](id:model.step9)

### Step 9. Enable text chat and on-screen comments
Call `sendRoomTextMsg` to send common text messages. All users in the room will receive an `onRecvRoomTextMsg` callback.
  IM has its default content moderation rules. Text messages that contain restricted terms will not be forwarded by the cloud.
  <dx-codeblock>
  ::: dart dart
  // Sender: send text messages
  trtcVoiceRoom.sendRoomTextMsg("Hello Word!");

// Recipient: listen for text messages
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onRecvRoomTextMsg:
            // Group text messages are received. This feature can be used to enable text chat rooms.
        break;
    }
}
:::
</dx-codeblock>
