To quickly enable the interactive live video streaming feature, you can modify the demo we provide and adapt it to your needs. You can also use the `TRTCLiveRoom` component and customize your own UI.

[](id:DemoUI)

## Using the Demo UI

[](id:ui.step1)

### Step 1. Create an application

1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestLive` and click **Create**.

>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)
### Step 2. Download the SDK and demo source code

1. Download the SDK and demo source code for your platform.
2. Click **Next**.
![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

[](id:ui.step3)
### Step 3. Configure demo project files

1. In the **Modify Configuration** step, select the development platform in line with the source package downloaded.
2. Find and open `/example/lib/debug/GenerateTestUserSig.dart`.
3. Set parameters in `GenerateTestUserSig.dart` as follows.
<ul style="margin:0"><li/>SDKAPPID: a placeholder by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: a placeholder by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
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

The `TRTCLiveRoom` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code. The table below lists the files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
| ------------ | ------------------------------------ |
| base | Basic classes used by the UI |
| list | List view and room creation view |
| room | Main room views for speakers and listeners |

[](id:model)

## Customizing Your Own UI

The `TRTCLiveRoom` folder in the [source code](https://github.com/tencentyun/TRTCFlutterScenesDemo) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCLiveRoom`. You can find the component's APIs in `TRTCLiveRoom.dart` and use them to customize your own UI.

[](id:model.step1)

### Step 1. Integrate the SDK

The interactive live streaming component `TRTCLiveRoom` depends on the [TRTC SDK](https://pub.dev/packages/tencent_trtc_cloud) and [IM SDK](https://pub.dev/packages/tencent_im_sdk_plugin). You can configure `pubspec.yaml` to download their updates automatically.

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
Add request for mic permission in `Info.plist`:
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

### Step 3. Import the `TRTCLiveRoom` component

Copy all the files in the directory below to your project:

```
lib/TRTCLiveRoom/model/
```

[](id:model.step4)

### Step 4. Create an instance and log in

1. Call the `sharedInstance` API to create an instance of the `TRTCLiveRoom` component.
2. Call the `registerListener` function to register event callbacks of the component.
3. Call the `login` function to log in to the component, and set the key parameters as described below.
<table>
<tr>
<th>Parameter</th>
<th>Description</th>
</tr>
<tr>
<td>SDKAPPID</td>
<td>You can view the `SDKAppID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
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
<td>useCDNFirst</td>
<td>Specifies the way audience watch live streams. `true` means that audience watch live streams over CDNs, which is cost-efficient but has high latency. `false` means that audience watch live streams in the low latency mode, the cost of which is between that of CDN live streaming and co-anchoring, but the latency is within 1 second.</td>
</tr>
<tr>
<td>CDNPlayDomain</td>
<td>Specifies the domain name for CDN live streaming, which takes effect only if `useCDNFirst` is set to `true`. You can set it in CSS console > **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>**.</td>
</tr>
</table>

[](id:model.step5)
### Step 5. Create a room and become a speaker

1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Before streaming, you can call `startCameraPreview` to enable camera preview, add beauty filter buttons to the UI, and set beauty filters through `getBeautyManager`.
>?Only the Enterprise Edition SDK supports face changing and stickers.
3. After setting beauty filters, call `createRoom` to create a live streaming room.
4. Call `startPublish` to start streaming. To enable CDN live streaming, specify `useCDNFirst` and `CDNPlayDomain` in the `TRTCLiveRoomConfig` parameter, which is passed in during login, and specify `streamID` for playback when calling `startPublish`.

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

[](id:model.step6)
### Step 6. Enter a room as a listener

1. After performing [step 4](#model.step4) to log in, you can call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest room list from the backend.
>?The room list in the demo is for demonstration only. The business logic of live streaming room lists vary significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfos` to get short descriptions of the rooms, which are provided by anchors when they call `createRoom` to create the rooms.
 >!If your room list already displays enough information, you can skip the step of calling `getRoomInfos`.
4. Select a room, call `enterRoom`, with the room ID passed in to enter the room.
5. Call `startPlay`, with the anchor's `userId` passed in to start playback.
 - If the room list displays the `userId` of the anchor, you can call `startPlay`, passing in the anchor's `userId` to start playback.
 - If you do not know the anchor's `userId`, you can find it in the `onAnchorEnter` event callback, which you will receive after entering the room. You can then call `startPlay` to start playback. 

![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

[](id:model.step7)
### Step 7. Co-anchor

1. Audience calls `requestJoinAnchor` to send a co-anchoring request to the anchor.
2. The anchor receives a notification (`TRTCLiveRoomDelegate#onRequestJoinAnchor`) about the co-anchoring request.
3. The anchor calls `responseJoinAnchor` to accept or decline the co-anchoring request.
4. The audience receives the `onAnchorAccepted` event notification, which carries the anchor's response.
5. If the anchor accepts the co-anchoring request, the audience can call `startCameraPreview` to turn the local camera on and then `startPublish` to push streams.
6. The anchor receives a notification (`TRTCLiveRoomDelegate#onAnchorEnter`) that a new stream is available, which carries the audience's `userId`.
7. The anchor calls `startPlay` to play the audience's video.

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)


[](id:model.step8)

### Step 8. Compete across rooms

1. Anchor A calls `requestRoomPK` to send a competition request to anchor B.
2. Anchor B receives the `TRTCLiveRoomDelegate onRequestRoomPK` notification.
3. Anchor B calls `responseRoomPK` to accept or decline the competition request.
4. Anchor B accepts the request and, after receiving the `TRTCLiveRoomDelegate onAnchorEnter` notification, calls `startPlay` to play anchor A's video.
5. Anchor A receives the `onRoomPKAccepted` notification, which specifies whether the competition request is accepted.
6. The request is accepted, and after receiving the `TRTCLiveRoomDelegate onAnchorEnter` notification, anchor A calls `startPlay` to play anchor B's video.

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

[](id:model.step9)
### Step 9. Enable text chat and on-screen comments
- Call `sendRoomTextMsg` to send common text messages. All users in the room will receive an `onRecvRoomTextMsg` callback.
  IM has its default content moderation rules. Text messages that contain restricted terms will not be forwarded by the cloud.
<dx-codeblock>
::: dart dart
// Sender: send text messages
trtcLiveCloud.sendRoomTextMsg("Hello Word!");
  

// Recipient: listen for text messages
onListenerFunc(type, params) async {
  switch (type) {
    case TRTCLiveRoomDelegate.onRecvRoomTextMsg:
          // Group text messages are received. This feature can be used to enable text chat rooms.
      break;
  }
}
:::
</dx-codeblock>
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All users in the room will receive an `onRecvRoomCustomMsg` callback.
  Custom messages are often used to transfer custom signals, e.g., to give and broadcast likes.
