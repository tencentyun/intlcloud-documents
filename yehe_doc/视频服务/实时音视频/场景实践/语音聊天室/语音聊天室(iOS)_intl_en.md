## Effect Demo
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo to try out the voice chat room capabilities of TRTC, such as seat management, low-latency voice interaction, and text chat.

To quickly implement the voice chat room feature, you can directly modify the demo provided by TRTC for adaptation or use the provided `TRTCVoiceRoom` component and implement custom UI.

<span id="DemoUI"> </span>
## Reusing Demo UI

<span id="ui.step1"></span>
### Step 1. Create an application
1. Log in to the TRTC Console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter the application name such as `TestVoiceRoom`, and click **Create Application**.

>?This feature uses two basic PaaS services, namely, [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When TRTC is activated, IM will be activated automatically.IM is a value-added service at the prices as detailed in [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350).

<span id="ui.step2"></span>
### Step 2. Download the SDK and demo source code
1. Mouse over the corresponding block, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)** to enter GitHub (or click **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)**), and download the relevant SDK and supporting demo source code.
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download is completed, return to the TRTC Console and click **Downloaded and Next**. Then, you can see the `SDKAPPID` and key information.

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
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can make a request to the business server for dynamic `UserSig`. For more information, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166).

<span id="ui.step4"></span>
### Step 4. Run the demo
Use Xcode (v11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` project and click **Run** to start debugging the demo.

<span id="ui.step5"></span>
### Step 5. Modify the demo source code
The `TRTCVoiceRoomDemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` folder contains the UI code and logic. The following table lists the Swift files or folders and the corresponding UIs for easy adjustment:

| File or Folder | Feature Description |
|:-------:|:--------|
|TRTCVoiceRoomEnteryController| This file contains all `ViewController` initialization methods. You can quickly get the `ViewController` object through this instance. |
| NetworkRoomManager | Related to business backend interaction. | 
| TRTCCreateVoiceRoomViewController | Logic for voice chat room creation page. | 
| TRTCVoiceRoomListViewController | Logic for list page. | 
| TRTCVoiceRoomViewController | Room homepage, including anchor and viewer UIs. | 

Each `TRTC'XXXX'ViewController` folder contains `ViewController`, `RootView`, and `ViewModel` as detailed below:

| File | Feature Description |
|:-------:|:--------|
| ViewController | Page controller, which is responsible for routing pages and binding `RootView` and `ViweModel`. | 
| RootView | View, i.e., all view layouts. | 
| ViewModel | View controller, which is responsible for responding to view interactions and returning view response status. | 

<span id="model"> </span>
## Implementing Custom UI
The `TRTCVoiceRoomDemo` folder in the [source code](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCVoiceRoomDemo) contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCVoiceRoom`. You can find the APIs provided by this component in the `TRTCVoiceRoom.swift` file and use the corresponding API to implement your own custom UI.
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)


<span id="model.step1"> </span>
### Step 1. Integrate SDKs
The voice chat component `TRTCVoiceRoom` depends on the TRTC SDK and IM SDK. You can integrate the two SDKs into your project in the following steps:

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
### Step 3. Import the TRTCVoiceRoom component
Copy all files in the `iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCVoiceRoomDemo/model` directory to your project.

<span id="model.step4"> </span>
### Step 4. Create and log in to the component
1. Call the `sharedInstance` class method of `TRTCVoiceRoomImp` to create an instance object that complies with the `TRTCVoiceRoom` protocol. You can also call the `shared` class method to get the `TRTCVoiceRoomImp` instance object for direct use. There is no difference between the two methods in the API use of `TRTCVoiceRoom`.
2. Call the `setDelegate` API to register the event callback notification of the component.
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
</tr>
<tr>
<td>callback</td>
<td>Login callback. The `code` will be 0 if login is successful.</td>
</tr>
</table>

```Swift
// Sample for Swift
// The class responsible for business logic in your code
class YourController {
    // Calculate attributes to get the singleton object
    var voiceRoom: TRTCVoiceRoomImp {
        return TRTCVoiceRoomImp.shared()
    }
    
    // Other code logic
    ......
}
// Set `voiceroom` delegation
self.vocieRoom. setDelegate(delegate: voiceRoomDelegate)

// The calling method is as follows. We recommend you use `weak self` in the closure to prevent circular reference (the `weak self` sample is omitted in the sample code below)
self.vocieRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // Your callback business logic        
}
```

<span id="model.step5"> </span>
### Step 5. The anchor starts streaming
1. The anchor can call `setSelfProfile` to set the nickname and profile photo after logging in by performing [step 4](#model.step4).
2. The anchor calls `createRoom` to create a voice chat room. At this time, room attribute information such as the room ID, whether mic-on needs confirmation by the anchor, and the number of seats is passed in.
3. After successfully creating the room, the anchor calls `enterSeat` to enter the seat.
4. The anchor receives the `onSeatListChange` seat list change event notification from the component. At this time, the seat list change can be refreshed and displayed on the UI.
5. The anchor will also receive the `onAnchorEnterSeat` event notification of that a member entered the seat list. At this time, mic capturing will be automatically enabled.

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)

Sample code:

```swift
// 1. The anchor sets the nickname and profile photo
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Callback for result           
}

// 2. The anchor previews and sets beauty filters before starting streaming
let param = VoiceRoomParam.init()
param.roomName = roomInfo.roomName
param.needRequest = roomInfo.needRequest
param.seatCount = roomInfo.memberCount
param.coverUrl = roomInfo.coverUrl
param.seatCount = 7 // Number of room seats. In this example, there are 7 seats in total. After the anchor takes one, 6 seats remain available
param.seatInfoList = []
for _ in 0..<param.seatCount {
    let seatInfo = VoiceRoomSeatInfo.init()
    param.seatInfoList.append(seatInfo)
}
self.voiceRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // Start taking a seat after successful room creation
    self.voiceRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // The anchor took a seat successfully
        } else {
            // The anchor failed to take a seat
        }
    }

    }
}

// 4. After the seat is successfully taken, the `onSeatListChange` event notification will be received
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refresh the seat list
}
// 5. The `onAnchorEnterSeat` event notification is received
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Process the anchor mic-on event
}
```

<span id="model.step6"> </span>
### Step 6. The viewer watches the live streaming
1. The viewer can call `setSelfProfile` to set the nickname and profile photo after logging in by performing [step 4](#model.step4).
2. The viewer gets the latest voice chat room list from the business backend.
 >?The list of voice chat rooms in the demo is for demonstration only. The business logic of the voice chat room list varies greatly, and Tencent Cloud currently does not provide voice chat room list management services. Please manage the voice chat room list by yourself.
3. The viewer can call `getRoomInfoList` to get the detailed information of the room, which is a simple description set by the anchor when calling `createRoom` to create the voice chat room.
 >!If your voice chat room list contains enough information, you can skip the step of calling `getRoomInfoList`.
4. The viewer selects a voice chat room and calls `enterRoom` and passes in the room ID to enter the room.
5. After room entry, the component's `onRoomInfoChange` room attribute change event notification will be received. At this time, the room attributes can be recorded, and corresponding changes can be made, such as the room name displayed on the UI and whether mic-on requires approval by the anchor.
6. After room entry, the `onSeatListChange` seat list change event notification will be received from the component. At this time, the seat list change can be refreshed and displayed on the UI.
7. After room entry, the `onAnchorEnterSeat` event notification that the anchor entered the seat list will also be received.


![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)

```Swift
// 1. The viewer sets the nickname and profile photo
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Callback for result           
}

// 2. Assume that you get the room list `roomList` from the business backend
let roomList: [Int] = getRoomIDList() // Your API to get the room ID list

// 3. Call `getRoomInfoList` to get the details of the room
self.voiceRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [VoiceRoomInfo]) in
    // Get the result. The UI can be refreshed at this time
}

// 4. After selecting the voice chat room, pass in the `roomId` to enter it
self.voiceRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // Callback for room entry
    if code == 0 {
       // Entered room successfully
    }
}

// 5. After successful room entry, the `onRoomInfoChange` event notification will be received
func onRoomInfoChange(roomInfo: VoiceRoomInfo) {
    // Update the room name and other information
}

// 6. After successful room entry, the `onSeatListChange` event notification will be received
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refresh the seat list
}

// 7. The `onAnchorEnterSeat` event notification is received
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Process the mic-on event
}

```

<span id="model.step7"> </span>
### Step 7. Manage seats
Anchor:
1. `pickSeat` can be called to pass in the corresponding seat number and viewer `userId` to pick the viewer for mic-on, and all members in the room will receive the event notifications of `onSeatListChange` and `onAnchorEnterSeat`.
2. `kickSeat` can be called to pass in the corresponding seat number to kick off a viewer for mic-off, and all members in the room will receive the event notifications of `onSeatListChange` and `onAnchorLeaveSeat`.
3. `muteSeat` can be called to pass in the corresponding seat number to mute/unmute the seat, and all members in the room will receive the event notifications of `onSeatListChange` and `onSeatMute`.
4. `closeSeat` can be called to pass in the corresponding seat number to block/unblock the seat. After the seat is blocked, the viewer cannot mic on, and all members in the room will receive the event notifications of `onSeatListChange` and `onSeatClose`.
![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)

Viewer:
1. `enterSeat` can be called to pass in the corresponding seat to mic on, and all members in the room will receive the event notifications of `onSeatListChange` and `onAnchorEnterSeat`.
2. `leaveSeat` can be called to actively mic off, and all members in the room will receive the event notifications of `onSeatListChange` and `onAnchorLeaveSeat`.

![](https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png)

After a seat operation is performed, the sequence of event notifications will be as follows:
`callback` > `onSeatListChange` > independent events such as `onAnchorEnterSeat`

```Swift
// Case 1. The anchor picks a viewer on seat 1 for mic-on
self.voiceRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // Callback for result
}

// 3. The `onSeatListChange` callback is received, and the seat list is refreshed
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refreshed seat list
}

// 4. A notification of one single seat change is received, based on which it can be determined whether the viewer successfully miced on
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Process the mic-on event
}
```

```Swift
// Case 2. The viewer actively chooses seat 2 for mic-on
voiceRoom.enterSeat(seatIndex: 2) { (code, message) in
    // Callback for mic-on result
}

// 3. The `onSeatListChange` callback is received, and the seat list is refreshed
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refreshed seat list
}

// 4. A notification of one single seat change is received, based on which it can be determined whether the seat was changed locally and corresponding operations can be performed
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Process the mic-on event
}
```

<span id="model.step8"> </span>
### Step 8. Use invitation signaling
In [seat management](#model.step7), viewers can directly mic on/off and the anchor can directly pick a viewer for mic-on without the approval of the other party.
If your application has business processes where the next operation can be performed only with the other party's approval, you can use invitation signaling.
If your viewers can mic on only after being approved:
1. The viewer calls `sendInvitation` to pass in information such as anchor `userId` and custom business command words. Then, the API will return an `inviteId`, which needs to be recorded.
2. The anchor receives the `onReceiveNewInvitation` event notification, and the UI can pop up a window to ask the anchor whether to approve the operation.
3. After approving the operation, the anchor calls `acceptInvitation` and passes in the `inviteId`.
4. The viewer receives the `onInviteeAccepted` event notification and calls `enterSeat` to mic on.

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

```Swift
// From the viewer's perspective
// 1. Call `sendInvitation` to request to choose seat 1 for mic-on
let inviteId = self.voiceRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // Callback for sending result
}
// 4. Mic on after receiving the approval for the invitation
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.enterSeat(seatIndex: ) { (code, message) in
            // Callback for mic-on result
        }
    }
}

// From the anchor's perspective
// 2. The anchor receives the request
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 3. The anchor approves the viewer's request
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```

If your anchor needs to send an invitation to pick a viewer for mic-on:
1. The anchor calls `sendInvitation` to pass in information such as viewer `userId` and custom business command words. Then, the API will return an `inviteId`, which needs to be recorded.
2. The viewer receives the `onReceiveNewInvitation` event notification, and the UI can pop up a window to ask the viewer whether to agree to mic on.
3. After agreeing, the viewer calls `acceptInvitation` and passes in the `inviteId`.
4. The anchor receives the `onInviteeAccepted` event notification and calls `pickSeat` to pick the viewer for mic-on.

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)

```java
// From the anchor's perspective
// 1. The anchor calls `sendInvitation` to request to pick viewer 123 on seat 2 for mic-on
let inviteId = self.voiceRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "2") { (code, message) in
    // Callback for sending result
}

// 4. Mic on after receiving the approval for the invitation
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.pickSeat(seatIndex: ) { (code, message) in
            // Callback for mic-on result
        }
    }
}

// From the viewer's perspective
// 2. The viewer receives the request
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 3. The viewer agrees to the anchor's request
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```

<span id="model.step9"> </span>
### Step 9. Implement text chat and on-screen commenting
- `sendRoomTextMsg` can be used to send general text messages, and all anchors and viewers in the room can receive the `onRecvRoomTextMsg` callback.
The backend of IM has default sensitive word filtering rules, and text messages that are considered to contain any sensitive words will not be forwarded by the cloud.

```Swift
// Sender: sends text messages
self.voiceRoom.sendRoomTextMsg(message: message) { (code, message) in
         
}
// Receiver: listens on text messages
func onRecvRoomTextMsg(message: String, userInfo: VoiceRoomUserInfo) {
    // Processing method for the received message        
}
```
- `sendRoomCustomMsg` can be used to send custom (signaling) messages, and all anchors and viewers in the room can receive the `onRecvRoomCustomMsg` callback.
 Custom messages are often used to transfer custom signals, such as sending and broadcasting likes.
 
```swift
// Example: sender: on-screen comments and likes can be distinguished between by custom `CMD`
// For example, "CMD_DANMU" indicates an on-screen comment, and "CMD_LIKE" indicates a like
self.vocieRoom.sendRoomCustomMsg(cmd: “CMD_DANMU”, message: "hello world", callback: nil)
self.voiceRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
// Receiver: listens on custom messages
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: VoiceRoomUserInfo) {
    if cmd == "CMD_DANMU" {
        // An on-screen comment is received
    }
    if cmd == "CMD_LIKE" {
        // A like is received
    }
}
```


