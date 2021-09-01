## Demonstration
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC’s interactive live streaming features, including co-anchoring, anchor competition, low-latency watch, and on-screen comments.

To quickly enable the interactive live video streaming feature, you can modify the demo we provide and adapt it to your needs. You can also use the `TRTCLiveRoom` component and customize your own UI.

[](id:DemoUI)
## Using the Demo UI

[](id:ui.step1)
### Step 1. Create an application.
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g. `TestLiveRoom`, and click **Create**.

>?The video conferencing feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.


[](id:ui.step2)
### Step 2. Download the SDK and demo source code.
1. Download the SDK and demo source code for your platform.
2. Click **Next**.

[](id:ui.step3)
### Step 3. Configure demo project files.
1. In the **Modify Configuration** step, select the platform in line with the source package downloaded.
2. Find and open the `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` file.
3. Set parameters in `GenerateTestUserSig.h` as follows.
<ul style="margin:0"><li/>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the demo.
Use Xcode (version 11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` project and click **Run** to start debugging.

[](id:ui.step5)
### Step 5. Modify the demo source code.
The `trtcliveroomdemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code. The table below lists the Swift files (folders) and UI views they represent. You can refer to it when making UI changes.

| File or Folder | Use |
|:-------:|:--------|
| Anchor | Implementation code for anchor-end views |
| Audience | Implementation code for viewer-end views |
| ChatRoom | Implementation code for the text chat room and on-screen comment views |
| Common | Implementation code for some reusable UI components |
| StatusView | Floating status view, which floats over video images and displays log information and video loading animations |
| LiveRoomMainViewController.swift | The main view for interactive live video streaming |


[](id:model)
## Implementing A Custom UI

The `trtcliveroomdemo` folder in the [source code] contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCLiveRoom`. You can find the component’s APIs in `TRTCLiveRoom.swift` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/710358e4e170d44304cdb9bc991ad209.jpg)


[](id:model.step1)
### Step 1. Integrate the SDKs.
The `TRTCLiveRoom` component depends on the TRTC SDK and IM SDK. Follow the steps below to integrate them into your project.

**Method 1: adding dependencies via CocoaPods**
```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).

**Method 2: adding dependencies through local files**
If your access to the CocoaPods repository is slow, you can download the ZIP packages of the SDKs and manually integrate them into your project as instructed in the documents below.

| SDK | Download Page | Integration Guide |
|---------|---------|---------|
| TRTC SDK | [Download](https://intl.cloud.tencent.com/document/product/647/34615) | [Integration document](https://intl.cloud.tencent.com/document/product/647/35093) |
| IM SDK | [Download](https://intl.cloud.tencent.com/document/product/1047/33996) | [Integration document](https://intl.cloud.tencent.com/document/product/1047/34306) |

[](id:model.step2)
### Step 2. Configure permission requests.
Configure camera and mic permission requests by adding `Privacy > Camera Usage Description` and `Privacy > Microphone Usage Description` in `info.plist`.

[](id:model.step3)
### Step 3. Import the `TRTCLiveRoom` component.
Copy all the files in `iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCLiveRoomDemo/model` to your project.


<span id="model.step4"></span>
### Step 4. Create a component instance and log in.
1. Call the `init` API of `TRTCLiveRoom` to create an instance of the `TRTCLiveRoom` component.
2. Create a `TRTCLiveRoomConfig` object, and set its `useCDNFirst` and `CDNPlayDomain` attributes.
 - `useCDNFirst` specifies the way viewers watch live streams. `true` means that viewers watch live streams over CDNs, which is cost-efficient but has high latency. `false` means that viewers watch live streams under the low latency mode, the cost of which is between that of CDN live streaming and co-anchoring, but the latency is lower than 1 second.
 - `CDNPlayDomain` attribute: specifies the domain name for CDN live streaming, which takes effect only if `useCDNFirst` is set to `true`. You can set it in CSS console > **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**.
3. Call the `login` function to log in to the component. Set the key parameters as described below.
<table>	
<tr>
<th>Parameter</th>
<th>Note</th>
</tr>
<tr>
<td>sdkAppId</td>
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
<td>config</td>
<td>Global configuration information. Please initialize it during login as it cannot be modified after login.<ul style="margin:0;">
<li>`useCDNFirst`: specifies the way viewers watch live streams. `true` means that viewers watch live streams over CDNs, which is cost-efficient but has high latency. `false` means that viewers watch live streams under the low latency mode, the cost of which is between that of CDN live streaming and co-anchoring, but the latency is lower than 1 second.</li>
<li>`CDNPlayDomain`: specifies the domain name for CDN live streaming, which takes effect only if `useCDNFirst` is set to `true`. You can set it in CSS console > **<a href="https://console.cloud.tencent.com/live/domainmanage">Domain Management</a>**.</li>
</ul></td>
</tr>
<tr>
<td>callback</td>
<td>Login callback. The code is 0 if login is successful.</td>
</tr>
</table>

```
class LiveRoomController: UIViewController {
	let mLiveRoom = TRTCLiveRoom()
}
// useCDNFirst: `true` means that viewers watch live streams over CDNs, and `false` means that viewers watch live streams under the low latency mode.
//CDNPlayDomain: the playback domain name for CDN live streaming
let config = TRTCLiveRoomConfig(useCDNFirst: useCDNFirst, cdnPlayDomain: yourCDNPlayDomain)
mLiveRoom.login(SDKAPPID, userID, userSig, config) { (code, error) in
	if code == 0 {
		//Login successful
	}
}
```


[](id:model.step5)
### Step 5. Start streaming as an anchor.
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo as an anchor.
2. Before streaming, you can call `startCameraPreview` to enable camera preview, add beauty filter buttons to the UI, and set beauty filters through `getBeautyManager`.
 >?Only the Enterprise Edition SDK supports face changing and stickers.
 >
3. After setting beauty filters, call `createRoom` to create a live streaming room.
4. Call `startPublish` to start streaming. To enable CDN live streaming, specify `useCDNFirst` and `CDNPlayDomain` in the `TRTCLiveRoomConfig` parameter passed in during login and specify the `streamID` for playback when calling `startPublish`.

![](https://main.qcloudimg.com/raw/eab281d702879ae87728d0064a090dca.jpg)

```swift
// 1. The anchor sets his or her nickname and profile photo.
mLiveRoom.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

// 2. The anchor enables camera preview and sets beauty filters before streaming.
let view = UIView()
parentView.add(view)
mLiveRoom.startCameraPreview(frontCamera: true, view: view, callback: nil)
mLiveRoom.getBeautyManager().setBeautyStyle(.nature)
mLiveRoom.getBeautyManager().setBeautyLevel(6)

// 3. The anchor creates a room.
let param = TRTCCreateRoomParam(roomName: "Test room", coverUrl: "")
mLiveRoom.createRoom(roomID: 123456789, roomParam: param) { [weak self] (code, error) in
	if code == 0 {
		// 4. The anchor starts streaming and publishes the streams to CDNs.
		self?.mLiveRoom.startPublish(streamID: mSelfUserId + "_stream", callback: nil)
	}
}
```


[](id:model.step6)
### Step 6. Play as a viewer.
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo as a viewer.
2. Gets the latest room list from the backend.
 >?The room list in the demo is for demonstration only. The business logic of live streaming room lists vary significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
 >
3. Call `getRoomInfos` to get short descriptions of the rooms, which are provided by anchors when they call `createRoom` to create the rooms.
 >!If your room list already displays enough information, you can skip the step of calling `getRoomInfos`.
 >
4. Select a room, call `enterRoom`, and pass in the room ID to enter the room.
5. Call `startPlay` and pass in the `userId` of the anchor to start playback.
 - If the room list displays the `userId` of the anchor, you can call `startPlay` and pass in the anchor’s `userId` to start playback.
 - If you do not know the anchor's `userId`, you can find it in the `onAnchorEnter` event callback, which you will receive after entering the room. You can then call `startPlay` to start playback. 


![](https://main.qcloudimg.com/raw/2ff8b30de38a3084c12af0513068dc6e.jpg)

```swift
// 1. Get the room list from the backend. Suppose it is `roomList`.
var roomList: [UInt32] = GetRoomList()

// 2. Call `getRoomInfos` to get the details of the room
mliveRoom.getRoomInfos(roomIDs: roomList, callback: { (code, msg, list) in
if code == 0 {
		// After getting the room information, you can display on the anchor list page the anchor's nickname, profile photo, and other information.
	}
})

// 3. Select a `roomid` and enter the room.
mliveRoom.enterRoom(roomID: roomID, callback: callback)

// 4. After receiving the notification about the anchor’s entry, start playback.
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
	// 5. Play the anchor's video image.
	mliveRoom.startPlay(userID: userID, view: renderView, callback: nil) 
}
```


[](id:model.step7)
### Step 7. Co-anchor as a viewer.
1. A viewer calls `requestJoinAnchor` to send a co-anchoring request to the anchor.
2. The anchor receives a notification (`TRTCLiveRoomDelegate#onRequestJoinAnchor`) that a viewer requested to co-anchor.
3. The anchor calls `responseJoinAnchor` to accept or decline the co-anchoring request.
4. The viewer receives the `TRTCLiveRoomDelegate#responseCallback` event notification, which carries the anchor’s response.
5. If the anchor accepts the co-anchoring request, the viewer can call `startCameraPreview` to turn on the local camera and then `startPublish` to push streams.
6. The anchor receives a notification (`TRTCLiveRoomDelegate#onAnchorEnter`) that a new stream from a viewer is available. The notification specifies the viewer’s `userId`.
7. The anchor calls `startPlay` to play the viewer's video image.

![](https://main.qcloudimg.com/raw/05a8c6af8bdc8b441f90b297e83106fc.jpg)

```swift
// Viewer:
// 1. The viewer sends a co-anchoring request.
mliveRoom.requestJoinAnchor(reason: mSelfUserId + "requested to co-anchor", responseCallback: { [weak self] (agreed, reason) in 
	  // 4. The anchor accepts the viewer's request.
     if agreed {
     	 // 5. The viewer turns on the camera and starts pushing streams.
     	 self?.mliveRoom.startCameraPreview(frontCamera: true, view: localView, callback: nil)
     	 self?.mliveRoom.startPublish(streamID: streamID, callback: nil)
     }        
}, callback: callback)

// Anchor:
// 2. The anchor receives the co-anchoring request.
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestJoinAnchor user: TRTCLiveUserInfo, reason: String?, timeout: Double) {
	// 3. The anchor accepts the co-anchoring request.
	mliveRoom.responseJoinAnchor(userID: userID, agree: true, reason: "agreed to co-anchor")
}

// 6. The anchor receives a notification that the co-anchoring viewer has turned on the mic.
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
	// 7. The anchor plays the viewer's video image.
	mliveRoom.startPlay(userID: userID, view: view, callback: nil)
}
```

[](id:model.step8)
### Step 8. Anchors compete with each other.
1. Anchor A calls `requestRoomPK` to send a competition request to anchor B.
2. Anchor B receives the `TRTCLiveRoomDelegate onRequestRoomPK` notification.
3. Anchor B calls `responseRoomPK` to accept or decline the competition request.
4. Anchor B accepts the request, waits for the `TRTCLiveRoomDelegate onAnchorEnter` notification, and calls `startPlay` to play anchor A's video image.
5. Anchor A receives the `responseCallback` notification, which specifies whether the competition request is accepted.
6. The request is accepted. Anchor A waits for the `TRTCLiveRoomDelegate onAnchorEnter` notification and calls `startPlay` to play anchor B's video image.

![](https://main.qcloudimg.com/raw/5632056b6d86541db841026e9488468b.jpg)

```swift
// Anchor A:
// Anchor A creates room 12345.
mLiveRoom.createRoom(roomID: 12345, roomParam: param, callback: nil)

// 1. Anchor A sends a competition request to anchor B.
mLiveRoom.requestRoomPK(roomID: 54321, userID: "B", responseCallback: { (agree, reason) in
	// 5. Anchor A receives a callback of whether anchor B accepts the request.
	if agree {
	}       
}, callback: callback)

// Anchor A receives the callback of anchor B’s entry.
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
	// 6. After receiving the notification of anchor B’s entry, anchor A plays anchor B's video image.
	mLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}

// Anchor B:
// Anchor B creates room 54321.
mLiveRoom.createRoom(roomID: 54321, roomParam: param, callback: nil)

// 2. Anchor B receives anchor A’s request.
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestRoomPK user: TRTCLiveUserInfo, timeout: Double) {
	// 3. Anchor B accepts anchor A's request.
	mLiveRoom.responseRoomPK(userID: userID, agree: true, reason: reason)
}

public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
	// 4. Anchor B receives a notification of anchor A’s entry and plays anchor A's video image.
	mLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}
```

[](id:model.step9)
### Step 9. Enable text chat and on-screen comments.
- Call `sendRoomTextMsg` to send text messages. All anchors and viewers in the room will receive the `onRecvRoomTextMsg` callback.
IM has its default content moderation rules. Text messages that contain blocked terms will not be forwarded by the cloud.
```swift
// Sender: send text messages
mLiveRoom.sendRoomTextMsg(message: "Hello Word!", callback: callback)
// Recipient: listen for text messages
mLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRecvRoomTextMsg message: String, fromUser user: TRTCLiveUserInfo) {
	debugPrint("Received a text message from \(user.userName): \(message)")
}
```
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All anchors and viewers in the room will receive the `onRecvRoomCustomMsg` callback.
 Custom messages are often used to transfer custom signals, e.g., sending and broadcasting likes.
```swift
// Sender: customize CMD to distinguish on-screen comments and likes
// E.g., use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes.
mLiveRoom.sendRoomCustomMsg(command: "CMD_DANMU", message: "Hello world", callback: nil)
mLiveRoom.sendRoomCustomMsg(command: "CMD_LIKE", message: "", callback: nil)
// Recipient: listen for custom messages
mLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRecvRoomCustomMsg command: String, message: String, fromUser user: TRTCLiveUserInfo) {
	if "CMD_DANMU" == command {
		// An on-screen comment is received.
		debugPrint("Received an on-screen comment from \(user.userName): \(message)")
	} else if "CMD_LIKE" == command {
		// A like is received.
		debugPrint("\(user.userName) liked you.")
	}
}
```
