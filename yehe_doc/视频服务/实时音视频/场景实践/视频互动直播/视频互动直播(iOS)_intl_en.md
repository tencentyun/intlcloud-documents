## Effect Demo
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo to try out the interactive video live streaming capabilities of TRTC, such as co-anchoring, anchor competition, low-latency watch, and chat through on-screen comments.

To quickly implement the interactive video live streaming feature, you can directly modify the demo provided by TRTC for adaptation or use the provided `TRTCLiveRoom` component and implement custom UI.

<span id="DemoUI"> </span>
## Reusing Demo UI

<span id="ui.step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter the application name such as `TestLiveRoom`, and click **Create Application**.

>?This feature uses two basic PaaS services, namely, [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When TRTC is activated, IM will be activated automatically.

<span id="ui.step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)** to enter GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)**), and download the relevant SDK and supporting demo source code.
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAppID` and key information.

<span id="ui.step3"></span>
### Step 3. Configure demo project files
1. Decompress the source package downloaded in [step 2](#ui.step2).
2. Find and open the `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` file.
3. Set the relevant parameters in the `GenerateTestUserSig.h` file:
  <ul><li>SDKAPPID: it is 0 by default. Please replace it with your real `SDKAppID`.</li>
  <li>SECRETKEY: it is an empty string by default. Please replace it with your real key information.</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Return to the TRTC Console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console** to manage the application.

>!The scheme for generating `UserSig` mentioned in this document is to configure `SECRETKEY` in the client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic; therefore, **this method is only suitable for local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [Server-Side UserSig Generation](https://intl.cloud.tencent.com/document/product/647/35166).

<span id="ui.step4"></span>
### Step 4. Run the demo
Use Xcode (v11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` project and click **Run** to start debugging the demo.

<span id="ui.step5"></span>
### Step 5. Modify the demo source code
The `trtcliveroomdemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code. The following table lists the Swift files or folders and the corresponding UIs for easy adjustment:

| File or Folder | Feature Description |
|:-------:|:--------|
| Anchor | Implementation code for anchor UI. | 
| Audience | Implementation code for viewer UI. | 
| ChatRoom | Implementation code for UIs for text chat room and on-screen commenting. | 
| Common | Implementation code for some reusable UI components. | 
| StatusView | Status floating view, which will cover the video image for displaying log information and video loading animations. | 
| LiveRoomMainViewController.swift | UI for interactive video live streaming homepage. | 


<span id="model"> </span>
## Implementing Custom UI

The `trtcliveroomdemo` folder in the [source code](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCLiveRoomDemo) contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCLiveRoom`. You can find the APIs provided by this component in the `TRTCLiveRoom.swift` file and use the corresponding API to implement your own custom UI.
![](https://main.qcloudimg.com/raw/710358e4e170d44304cdb9bc991ad209.jpg)


<span id="model.step1"> </span>
### Step 1. Integrate SDKs
The video call component `TRTCLiveRoom` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project in the following steps:

**Method 1. Implement dependency through the CocoaPods repository**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?You can get the latest version numbers of the two SDKs on the [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK) homepages on GitHub.

**Method 2. Implement dependency through local files**
If the access to the CocoaPods repository is slow in your development environment, you can download the ZIP packages and manually integrate the SDKs into your project as instructed in the integration document.

| SDK | Download Page | Integration Guide |
|---------|---------|---------|
| TRTC SDK | [Download](https://intl.cloud.tencent.com/document/product/647/34615) | [Integration document](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [Download](https://intl.cloud.tencent.com/document/product/1047/33996) | [Integration document](https://intl.cloud.tencent.com/document/product/1047/34306) |

<span id="model.step2"> </span>
### Step 2. Configure permissions
Apply for the camera and mic permissions by adding `Privacy > Camera Usage Description` and `Privacy > Microphone Usage Description` in the `info.plist` file.

<span id="model.step3"> </span>
### Step 3. Import the TRTCLiveRoom component
Copy all files in the `iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCLiveRoomDemo/model` directory to your project.

<span id="model.step4"> </span>
### Step 4. Create and log in to the component
1. Call the `init` API of `TRTCLiveRoomImpl` to create an instance object of the `TRTCLiveRoom` component.
2. Create a `TRTCLiveRoomConfig` object, where the `useCDNFirst` and `CDNPlayDomain` attributes can be set:
 - `useCDNFirst` attribute: used to set the way how viewers will watch live streaming. `true` means that general viewers will watch live streaming over CDN, which is cheap but has a high latency. `false` means that general viewers will watch live streaming through the low latency scheme, the cost of which ranges between that of CDN and co-anchoring, but the delay can be controlled within 1 second.
 - `CDNPlayDomain` attribute: it will take effect only if `useCDNFirst` is set to `true`. It is used to specify the playback domain name for watching over CDN. You can set it in **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the LVB Console.
3. Call the `login` API to log in to the component. Enter key parameters as shown below:
<table>	
<tr>
<th>Parameter Name</th>
<th>Description</th>
</tr>
<tr>
<td>sdkAppId</td>
<td>You can view the `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC Console</a>.</td>
</tr>
<tr>
<td>userId</td>
<td>ID of current user, which is a string that can contain only letters (a–z and A–Z), digits (0–9), hyphens (-), and underscores (_).</td>
</tr>
<tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security protection signature. For more information on how to get it, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">How to Calculate UserSig</a>.</td>
</tr>
<tr>
<td>config</td>
<td>Global configuration information. Please initialize it during login as it cannot be modified after login.<ul style="margin:0;">
<li>`useCDNFirst` attribute: used to set the way how viewers will watch live streaming. `true` means that general viewers will watch live streaming over CDN, which is cheap but has a high latency. `false` means that general viewers will watch live streaming through the low latency scheme, the cost of which ranges between that of CDN and co-anchoring, but the delay can be controlled within 1 second.</li>
<li>`CDNPlayDomain` attribute: it will take effect only if `useCDNFirst` is set to `true`. It is used to specify the playback domain name for watching over CDN. You can set it in **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>** in the LVB Console.</li>
</ul></td>
</tr>
<tr>
<td>callback</td>
<td>Login callback. The `code` will be 0 if login is successful.</td>
</tr>
</table>
<pre>
class LiveRoomController: UIViewController {
	let mLiveRoom = TRTCLiveRoomImpl()
}
// useCDNFirst: `true` means that general viewers will watch live streaming over CDN, while `false` means that general viewers will watch live streaming through the low latency scheme
// CDNPlayDomain: the playback domain name set for watching over CDN
let config = TRTCLiveRoomConfig(useCDNFirst: useCDNFirst, cdnPlayDomain: yourCDNPlayDomain)
mLiveRoom.login(SDKAPPID, userID, userSig, config) { (code, error) in
	if code == 0 {
		// Logged in successfully
	}
}
</pre>

<span id="model.step5"> </span>
### Step 5. The anchor starts streaming
1. The anchor can call `setSelfProfile` to set the nickname and profile photo after logging in by performing [step 4](#model.step4).
2. Before starting streaming, the anchor can call `startCameraPreview` to enable camera preview, where the beauty filter adjusting buttons can be configured for setting beauty filters through `getBeautyManager`.
 >?Face changing and sticker pendant features are not supported for SDKs in editions other than the Enterprise Edition.
 >
3. The anchor can call `createRoom` to create a live room after adjusting the beauty filters.
4. The anchor can call `startPublish` to start pushing. To enable watching over CDN, please specify `useCDNFirst` and `CDNPlayDomain` in the `TRTCLiveRoomConfig` parameter passed in during login and specify the `streamID` for LVB pull during `startPublish`.

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

```swift
// 1. The anchor sets the nickname and profile photo
mLiveRoom.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2. The anchor previews and sets beauty filters before starting streaming
let view = UIView()
parentView.add(view)
mLiveRoom.startCameraPreview(frontCamera: true, view: view, callback: nil)
mLiveRoom.getBeautyManager().setBeautyStyle(.nature)
mLiveRoom.getBeautyManager().setBeautyLevel(6)

// 3. The anchor creates a room
let param = TRTCCreateRoomParam(roomName: "Test room", coverUrl: "")
mLiveRoom.createRoom(roomID: 123456789, roomParam: param) { [weak self] (code, error) in
	if code == 0 {
		// 4. The anchor enables push and publishes the stream to CDN
		self?.mLiveRoom.startPublish(streamID: mSelfUserId + "_stream", callback: nil)
	}
}
```

<span id="model.step6"> </span>
### Step 6. The viewer watches the live streaming
1. The viewer can call `setSelfProfile` to set the nickname and profile photo after logging in by performing [step 4](#model.step4).
2. The viewer gets the latest live room list from the business backend.
 >?The live room list in the demo is for demonstration purposes only. The business logic of the live room list varies greatly, and Tencent Cloud currently does not provide live room list management services. Please manage the live room list by yourself.
 >
3. The viewer can call `getRoomInfos` to get the detailed information of the room, which is a simple description set by the anchor when calling `createRoom` to create the live room.
 >!If your live room list contains enough information, you can skip the step of calling `getRoomInfos`.
 >
4. The viewer selects a live room and calls `enterRoom` and passes in the room ID to enter the room.
5. The viewer calls `startPlay` and pass in the `userId` of the anchor to start playback.
 - If the live room list contains the `userId` of the anchor, the viewer can directly call `startPlay` and pass in the `userId` of the anchor to start playback.
 - If the viewer does not have the anchor's `userId` before entering the room, they will receive the `onAnchorEnter` event callback from the anchor after entering the room, which carries the anchor's `userId`. Then, the viewer can call `startPlay` to start playback. 


![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

```swift
// 1. Assume that you get the room list `roomList` from the business backend
var roomList: [UInt32] = GetRoomList()

// 2. Call `getRoomInfos` to get the details of the room
mliveRoom.getRoomInfos(roomIDs: roomList, callback: { (code, msg, list) in
if code == 0 {
		// After getting the room details, you can display relevant information on the anchor list page, such as the anchor's nickname and profile photo
	}
})

// 3. Select the `roomid` to enter the room
mliveRoom.enterRoom(roomID: roomID, callback: callback)

// 4. The viewer receives the notification of room entry by the anchor, and playback starts
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onAnchorEnter userID: String) {
	// 5. The viewer plays back the anchor's video image
	mliveRoom.startPlay(userID: userID, view: renderView, callback: nil) 
}
```

<span id="model.step7"> </span>
### Step 7. The viewer co-anchors with the anchor
1. The viewer calls `requestJoinAnchor` to initiate a co-anchoring request to the anchor.
2. The anchor will receive the `TRTCLiveRoomDelegate#onRequestJoinAnchor` event notification (i.e., "a viewer has initiated a request to co-anchor with you").
3. The anchor can decide whether to accept the co-anchoring request from the viewer by calling `responseJoinAnchor`.
4. The viewer will receive the `TRTCLiveRoomDelegate#responseCallback` event notification, which will carry the processing result from the anchor.
5. If the anchor agrees to the co-anchoring request, the viewer can call `startCameraPreview` to enable local camera and then call `startPublish` to start push.
6. The anchor will receive the `TRTCLiveRoomDelegate#onAnchorEnter` notification (i.e., "another audio/video stream has arrived") after the viewer enables notification, which will carry the viewer's `userId`.
7. The anchor can call `startPlay` to view the co-anchoring viewer's video image.

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)

```swift
// Viewer:
// 1. The viewer initiates a co-anchoring request
mliveRoom.requestJoinAnchor(reason: mSelfUserId + "requested to co-anchor with you", responseCallback: { [weak self] (agreed, reason) in 
	  // 4. The anchor accepts the viewer's request
     if agreed {
     	 // 5. The viewer starts preview and enables push
     	 self?.mliveRoom.startCameraPreview(frontCamera: true, view: localView, callback: nil)
     	 self?.mliveRoom.startPublish(streamID: streamID, callback: nil)
     }        
}, callback: callback)

// Anchor:
// 2. The anchor receives the co-anchoring request
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onRequestJoinAnchor user: TRTCLiveUserInfo, reason: String?, timeout: Double) {
	// 3. The anchor agrees to the co-anchoring request
	mliveRoom.responseJoinAnchor(userID: userID, agree: true, reason: "agreed to co-anchor")
}

// 6. The anchor receives the notification of mic-on by the co-anchoring viewer
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onAnchorEnter userID: String) {
	// 7. The anchor plays back the viewer's video image
	mliveRoom.startPlay(userID: userID, view: view, callback: nil)
}
```

<span id="model.step8"> </span>
### Step 8. One anchor competes with another anchor
1. Anchor A calls `requestRoomPK` to initiate a competition request to anchor B.
2. Anchor B will receive the `TRTCLiveRoomDelegate onRequestRoomPK` callback notification.
3. Anchor B decides whether to accept the competition request from anchor A by calling `responseRoomPK`.
4. Anchor B accepts the request from anchor A, waits for the `TRTCLiveRoomDelegate onAnchorEnter` notification, and calls `startPlay` to display anchor A's video image.
5. Anchor A receives the `responseCallback` callback notification of whether the request to compete is accepted.
6. Anchor A's request is accepted, and anchor A waits for `TRTCLiveRoomDelegate onAnchorEnter` notification and calls `startPlay` to display anchor B's video image.

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

```swift
// Anchor A:
// Anchor A creates room 12345
mLiveRoom.createRoom(roomID: 12345, roomParam: param, callback: nil)

// 1. Anchor A initiates a repetition request to anchor B
mLiveRoom.requestRoomPK(roomID: 54321, userID: "B", responseCallback: { (agree, reason) in
	// 5. Anchor A receives the callback of whether anchor B accepts the request
	if agree {
	}       
}, callback: callback)

// Anchor A receives the callback of room entry by anchor B
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onAnchorEnter userID: String) {
	// 6. Anchor A receives notification of room entry by anchor B and plays back anchor B's video image
	mLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}

// Anchor B:
// Anchor B creates room 54321
mLiveRoom.createRoom(roomID: 54321, roomParam: param, callback: nil)

// 2. Anchor B receives the message from anchor A
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onRequestRoomPK user: TRTCLiveUserInfo, timeout: Double) {
	// 3. Anchor B replies to anchor A and accepts anchor A's request
	mLiveRoom.responseRoomPK(userID: userID, agree: true, reason: reason)
}

public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onAnchorEnter userID: String) {
	// 4. Anchor B receives notification of room entry by anchor A and plays back anchor A's video image
	mLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}
```

<span id="model.step9"> </span>
### Step 9. Implement text chat and on-screen commenting
- `sendRoomTextMsg` can be used to send general text messages, and all anchors and viewers in the room can receive the `onRecvRoomTextMsg` callback.
The backend of IM has default sensitive word filtering rules, and text messages that are considered to contain any sensitive words will not be forwarded by the cloud.
```swift
// Sender: sends text messages
mLiveRoom.sendRoomTextMsg(message: "Hello Word!", callback: callback)
// Receiver: listens on text messages
mLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onRecvRoomTextMsg message: String, fromUser user: TRTCLiveUserInfo) {
	debugPrint("A text message from \(user.userName) is received:\(message)")
}
```
- `sendRoomCustomMsg` can be used to send custom (signaling) messages, and all anchors and viewers in the room can receive the `onRecvRoomCustomMsg` callback.
 Custom messages are often used to transfer custom signals, such as sending and broadcasting likes.
```swift
// Sender: on-screen comments and likes can be distinguished between by custom `CMD`
// For example, "CMD_DANMU" indicates an on-screen comment, and "CMD_LIKE" indicates a like
mLiveRoom.sendRoomCustomMsg(command: "CMD_DANMU", message: "Hello world", callback: nil)
mLiveRoom.sendRoomCustomMsg(command: "CMD_LIKE", message: "", callback: nil)
// Receiver: listens on custom messages
mLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoomImpl, onRecvRoomCustomMsg command: String, message: String, fromUser user: TRTCLiveUserInfo) {
	if "CMD_DANMU" == command {
		// An on-screen comment is received
		debugPrint("An on-screen comment from \(user.userName) is received: \(message)")
	} else if "CMD_LIKE" == command {
		// A like is received
		debugPrint("\(user.userName) has liked you!")
	}
}
```
