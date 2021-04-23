## Demonstration

>! This project does not support Flutter 2.0 for the time being. If you are using Flutter 2.0, please downgrade it first.

You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC features in the chat salon scenario, including audio chat, mic on/off, low-latency audio interaction, etc.


To quickly enable the chat salon feature, you can modify the demo we provide and adapt it to your needs. You may also use the `TRTCChatSalon` component and customize your own UI.

[](id:DemoUI)

## Using Demo UI

[](id:ui.step1)
### Step 1. Create an application
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestChatSalon` and click **Create**.

>!This feature uses two basic PaaS services of Tencent Cloud, namely, [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)
### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code for your platform.
2. Click **Next**.

[](id:ui.step3)
### Step 3. Configure demo project files
1. In the **Modify Configuration** step, select the platform in line with the source package downloaded.
2. Find and open the `/example/lib/debug/GenerateTestUserSig.dart` file.
3. Set parameters in `GenerateTestUserSig.dart` as follows:
<ul style="margin:0"><li/>SDKAPPID: `PLACEHOLDER` by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: `PLACEHOLDER` by default. Set it to the actual key.</ul>
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.


>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, please see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Compile and run

>! An Android project must be run on a real device rather than a simulator.

1. Run `flutter pub get`.
2. Compile, run, and debug the project.
  ####  Android\s
    1. Run `flutter run`.
    2. Use Android Studio (3.5 or above) to open the demo and run the project.
  ####  iOS
    1. Open `\ios project` in the source code directory with Xcode (11.0 or above).
    2. Compile and run the demo project.

[](id:ui.step5)
### Step 5. Modify the demo source code
The `trtcchatsalondemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains the UI code. The table below lists some of the files or folders and the UI views they represent. You can use it for reference when making UI changes.

| File or Folder | Description |
| ------------ | ------------------------------------ |
| base | Basic classes used by the UI |
| list | List view and room creation view|
| room | Main room views for speakers and listeners |
| widget | Common control |

[](id:model)
## Customizing UI
The `trtcchatsalondemo` folder in the [source code](https://github.com/c1avie/TRTCChatSalon) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCChatSalon`. You can find the component's APIs in `TRTCChatSalon.dart` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/7613bd7ec5b4e665f32ee5df69e5de85.png)

[](id:model.step1)
### Step 1. Integrate SDKs
The chat salon component `trtcchatsalondemo` depends on the [TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud) and [IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin). You can configure `pubspec.yaml` to download updates automatically.

Add the following dependencies to `pubspec.yaml` of your project.
```
dependencies:
  tencent_trtc_cloud: latest version number
  tencent_im_sdk_plugin: latest version number
```

[](id:model.step2)

### Step 2. Configure permission requests and obfuscation rules
#### iOS
Add requests for camera and mic permissions in `Info.plist`:
```
<key>NSMicrophoneUsageDescription</key>
<string>Audio calls are possible only with mic permission.</string>
```
#### Android
1. Open `/android/app/src/main/AndroidManifest.xml`.
2. Add `xmlns:tools="http://schemas.android.com/tools"` to "manifest".
3. Add `tools:replace="android:label"` to "application".
>? Without the above steps, the ["Android Manifest merge failed"](https://intl.cloud.tencent.com/document/product/647/39242) error will occur and the compilation will fail.

![](https://main.qcloudimg.com/raw/7a37917112831488423c1744f370c883.png)


[](id:model.step3)
### Step 3. Import the TRTCChatSalon component
Copy all the files in the following directory to your project:
```
lib/TRTCChatSalonDemo/model/
```

<span id="model.step4"></span>
### Step 4. Create an instance and log in
1. Call the `sharedInstance` API to create an instance of the `TRTCChatSalon` component.
2. Call the `registerListener` function to register event callbacks of the component.
3. Call the `login` function to log in to the component. Set the key parameters as described below.
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>sdkAppId</td>
<td>You can view the `SDKAppID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr>
<tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_).</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. To get one, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr>
</table>

```
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
```

[](id:model.step5)

### Step 5. Create a room and become a speaker

1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Call `createRoom` to create a chat salon, passing in room-related parameters such as room ID and room name.
3. You will receive a `TRTCChatSalonDelegate.onAnchorEnterSeat` notification that someone becomes a speaker, and mic capturing will be enabled automatically.

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)

```
// 1. Set your nickname and profile photo
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
   // Became a speaker
}

// 4. You receive a `TRTCChatSalonDelegate.onAudienceEnter` notification after becoming a speaker
onVoiceListener(type, param) async {
    switch (type) {
        case TRTCChatSalonDelegate.onAudienceEnter:
            // A listener enters the room
            break;
    }
}
```

[](id:model.step6)

### Step 6. Enter a room as a listener

1. After performing [step 4](#model.step4) to log in, you can call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest chat salon room list from the backend.
 >?The chat salon list in the demo is for demonstration only. The business logic of the chat salon list varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomList` to get short descriptions of the rooms, which are provided by room owners when they call `createRoom` to create the rooms.
>!If your chat salon list already contains enough room information, you can skip the step of calling `getRoomList`. Just pass in the room ID to enter.
4. After room entry, you will receive `TRTCChatSalonDelegate.onAudienceEnter` and `TRTCChatSalonDelegate.onAudienceExit` notifications about listeners’ room entry/exit from the component. Display the changes on the UI afterwards.
5. You will also receive `TRTCChatSalonDelegate.onAnchorEnterMic` and `TRTCChatSalonDelegate.onAnchorLeaveMic` notifications about speaker list change.

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)
```
// 1. Set your nickname and profile photo
trtcVoiceRoom.setSelfProfile("my_name", "my_face_url");

// 2. Get the room list from the backend. Suppose it is `roomList`
List<Integer> roomList = GetRoomList();

// 3. Call `getRoomInfoList` to get the details of the rooms
RoomInfoCallback resp = await trtcVoiceRoom.getRoomInfoList(roomList);
if (resp.code == 0) {
    // Refresh the room list on your UI
} 

// 4. Pass in `roomId` to enter the room
ActionCallback enterRoomResp =
          await trtcVoiceRoom.enterRoom(_currentRoomId);
if (enterRoomResp.code == 0) {
    // Entered room
}
// 5. After successful room entry, you receive a handling notification
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onAudienceEnter:
            // A listener enters the room
        break;
      case TRTCChatSalonDelegate.onAudienceExit:
            // A listener exits the room
        break;
      case TRTCChatSalonDelegate.onAnchorLeaveMic:
          // A speaker exits the room
        break;
      case TRTCChatSalonDelegate.onAnchorEnterMic:
          // A speaker enters the room
        break;
    }
}
```

[](id:model.step7)
### Step 7. Mic on/off
#### Room owner
1.  A room owner can call `leaveMic` to become a listener. All users in the room will receive an `onAnchorLeaveMic` notification.
2.  A room owner can remove a speaker by passing in the speaker’s `userId` in `kickMic`. All users in the room will receive an `onAnchorLeaveMic` notification.

![](https://main.qcloudimg.com/raw/b47e4ce248aa71f9a68f28f57c699db6.png)
```
// 1. Become a listener
trtcVoiceRoom.leaveMic();

//2. Remove a speaker
trtcVoiceRoom.kickMic(userId);
```
#### Listener
1. A listener can become a speaker by calling `enterMic`. All members in the room will receive an `onAnchorEnterMic` notification.
2. A speaker can become a listener by calling `leaveMic`. All members in the room will receive an `onAnchorLeaveMic` notification.

![](https://main.qcloudimg.com/raw/8b68a5c714bf024c8598a52a7281c745.png)
```
// 1. Become a speaker
trtcVoiceRoom.enterMic();

// 2. Become a listener
trtcVoiceRoom.leaveMic();
```


[](id:model.step8)

### Step 8. Use signaling to send messages about hand raising

If you want listeners and room owners to obtain each other’s consent before performing the above actions in your app, you can use signaling for invitation sending.

#### Listener requesting to speak

1. The listener calls `raiseHand` to request to speak.
2. The room owner receives an `onRaiseHand` notification, and a window pops up on the UI asking the room owner whether to approve the request.
3. The room owner approves the request and calls `agreeToSpeak`, with the `userId` passed in.
4. The listener receives an `onAgreeToSpeak` notification and calls `enterMic` to become a speaker.

![](https://main.qcloudimg.com/raw/72e4ddc8e1d13b47c6713355145c297e.png)
```
// Listener
// 1. Call `sendInvitation` to request to speak
trtcVoiceRoom.raiseHand();

// 2. Become a speaker upon receiving approval from the room owner
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onRaiseHand:
           trtcVoiceRoom.enterMic();
        break;
    }
}

// Room owner
// 1. Receive the request
onVoiceListener(type, param) async {
    switch (type) {
      case TRTCChatSalonDelegate.onAgreeToSpeak:
           trtcVoiceRoom.agreeToSpeak();
        break;
    }
}
```

[](id:model.step9)

### Step 9. Enable text chat and on-screen comments
Call `sendRoomTextMsg` to send common text messages. All users in the room will receive an `onRecvRoomTextMsg` callback.
IM has its default content filtering rules. Text messages that contain restricted terms will not be forwarded by the cloud.
```
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
```
