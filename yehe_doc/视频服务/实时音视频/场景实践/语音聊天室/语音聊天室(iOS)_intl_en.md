## Demonstration
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demos we provide to try out TRTC features in the voice chat room scenario, including seat management, low-latency voice interaction, text chat, etc.











To quickly enable the video chat room feature, you can modify the demos we provide and adapt it to your needs. You may also use the `TRTCVoiceRoom` component and customize your own UI.

<span id="DemoUI"> </span>
## Using the Demo UI

<span id="ui.step1"></span>
### Step 1. Create an application.
1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Click **Start Now**, enter an application name, e.g. `TestLiveRoom`, and click **Create Application**.

>?The voice chat room feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



<span id="ui.step2"></span>
### Step 2. Download the SDK and demo source code.
1. Hover over the block of the platform you use, click **[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS)** (or **[ZIP](http://liteavsdk-1252463788.cosgz.myqcloud.com/TXLiteAVSDK_TRTC_iOS_latest.zip)**) to download the SDK and demo source code.
 ![](https://main.qcloudimg.com/raw/b0f6f1bd5e0bc083bafddcc7c04a1593.png)
2. After the download, return to the TRTC console and click **Downloaded and Next** to view your `SDKAppID` and key.

<span id="ui.step3"></span>
### Step 3. Configure demo project files.
1. Decompress the source package downloaded in [step 2](#ui.step2).
2. Find and open the `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` file.
3. Set parameters in `GenerateTestUserSig.h` as follows.
  <ul><li>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.</li>
  <li>SECRETKEY: left empty by default. Set it to the actual key.</li></ul> 
    <img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">
4. Return to the TRTC console and click **Pasted and Next**.
5. Click **Close Guide and Enter Console**.

>!The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

<span id="ui.step4"></span>
### Step 4. Run the demo.
Use Xcode (version 11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` project and click **Run** to start debugging the demo.

<span id="ui.step5"></span>
### Step 5. Modify the demo source code.
The `TRTCVoiceRoomDemo` folder in the source code contains two subfolders: `ui` and `model`. In the `ui` subfolder are UI code and UI-related logics. The table below lists some of the files or folders and the UI views they are responsible for. You can use it for reference when making UI changes.

| File or Folder | Use |
|:-------:|:--------|
|TRTCVoiceRoomEnteryController| The initialization method of all `ViewControllers`. You can use the instance to quickly get a `ViewController` object. |
| NetworkRoomManager | Code and logic related to backend interactions | 
| TRTCCreateVoiceRoomViewController | Logic for the room creation view | 
| TRTCVoiceRoomListViewController | Logic for the room list view | 
| TRTCVoiceRoomViewController | Logic for the main room views for anchors and viewers | 

Each `TRTC'XXXX'ViewController` folder contains `ViewController`, `RootView`, and `ViewModel`, whose use is described below.

| File | Use |
|:-------:|:--------|
| ViewController | Page controller, which is responsible for routing pages and binding `RootView` and `ViweModel` | 
| RootView | Layout of all views | 
| ViewModel | View controller, which is responsible for responding to user interactions with views and returning response status | 

<span id="model"> </span>
## Customizing UI
The `TRTCVoiceRoomDemo` folder in the [source code](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCVoiceRoomDemo) contains two subfolders: `ui` and `model`. In the `model` subfolder is the reusable open-source component `TRTCVoiceRoom`. You can find the component’s APIs in `TRTCVoiceRoom.swift` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)


<span id="model.step1"> </span>
### Step 1. Integrate the SDKs.
The voice chat room component `TRTCVoiceRoom` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project.

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

<span id="model.step2"> </span>
### Step 2. Configure permission requests.
Configure camera and mic permission requests by adding `Privacy > Camera Usage Description` and `Privacy > Microphone Usage Description` in `info.plist`.

<span id="model.step3"> </span>
### Step 3. Import the `TRTCVoiceRoom` component.
Copy all files in `iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCVoiceRoomDemo/model` to your project.

<span id="model.step4"> </span>
### Step 4. Create a `TRTCVoiceRoom` instance and log in.
1. Call the `sharedInstance` class method of `TRTCVoiceRoomImp` to create an instance that complies with `TRTCVoiceRoom`’s protocol, or call the `shared` class method to get a `TRTCVoiceRoomImp` instance. There is no difference between the two methods with respect to API usage.
2. Call the `setDelegate` function to register event callbacks of the component.
3. Call the `login` function to log in to the component. Set the key parameters as described below.
<table>    
<tr><th>Parameter</th><th>Note</th></tr><tr>
<td>sdkAppId</td>
<td>You can view the `SDKAppID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_).</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. To obtain one, see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr></tr>
<tr>
<td>callback</td>
<td>Login callback. The code is 0 if login is successful.</td>
</tr>
</table>

```Swift
// Swift sample
// The class responsible for business logic in your code
class YourController {
    // Calculate attributes to get a singleton object.
    var voiceRoom: TRTCVoiceRoomImp {
        return TRTCVoiceRoomImp.shared()
    }
    
    // Other code logic
    ......
}
// Set `voiceroom` delegate.
self.vocieRoom. setDelegate(delegate: voiceRoomDelegate)

// Below is the calling method. We recommend you use `weak self` in the closure to prevent circular references. The `weak self` part is not included in the sample code below.
self.vocieRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // Your callback business logic        
}
```

<span id="model.step5"> </span>
### Step 5. Start streaming as an anchor.
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo as an anchor.
2. Call `createRoom` to create a voice chat room and pass in room-related parameters such as room ID, whether mic enabling by viewers needs your permission, and the number of seats in the room.
3. After successfully creating a room, call `enterSeat` to take a seat.
4. You will receive an `onSeatListChange` notification about seat change from the component. Update the change to the UI.
5. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat, and mic capturing will be enabled automatically.

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)

Sample code:

```swift
// 1. Set your nickname and profile photo as an anchor.
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Result callback           
}



// 2. Create a room as an anchor.
let param = VoiceRoomParam.init()
param.roomName = "Room ID"
param.needRequest = true // Whether mic enabling by viewers needs your permission.
param.coverUrl = "Cover URL"
param.seatCount = 7 // Number of room seats. In this example, the number is 7. 6 seats remain after you take one.
param.seatInfoList = []
for _ in 0..<param.seatCount {
    let seatInfo = VoiceRoomSeatInfo.init()
    param.seatInfoList.append(seatInfo)
}
self.voiceRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // Take a seat after successfully creating a room.
    self.voiceRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // Seat taken successfully.
        } else {
            // Failed to take a seat.
        }
    }
}



// 3. After taking a seat successfully, you receive an `onSeatListChange` notification.
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refresh your seat list.
}



// 4. You receive an `onAnchorEnterSeat` notification.
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the anchor mic-on event.
}
```

<span id="model.step6"> </span>
### Step 6. Play back as a viewer.
1. After performing [step 4](#model.step4) to log in, you can call `setSelfProfile` to set your nickname and profile photo as a viewer.
2. Get the latest voice chat room list from the backend.
 >?The voice chat room list in the demo is for demonstration only. The business logic of the voice chat room list varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided when anchors call `createRoom` to create the rooms.
 >!If your voice chat room list already contains enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select a voice chat room, call `enterRoom`, and pass in the room ID to enter the room.
5. After entry, you will receive an `onRoomInfoChange` notification about room change from the component. Note the room information, including the room name displayed on the UI, whether mic enabling requires permission from the anchor, etc., and update your existing information.
6. You will receive an `onSeatListChange` notification about the seat change from the component. Update the change to the UI.
7. You will also receive an `onAnchorEnterSeat` notification about the seating of the anchor.


![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)

```Swift
// 1. Set your nickname and profile photo as a viewer.
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Result callback           
}

// 2. Get the room list from the backend. Suppose it is `roomList`.
let roomList: [Int] = getRoomIDList() // The function you use to get the list of room IDs

// 3. Call `getRoomInfoList` to get the details of the rooms.
self.voiceRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [VoiceRoomInfo]) in
    // Get the result. Refresh the UI.
}

// 4. Select a voice chat room, and pass in the `roomId` to enter it.
self.voiceRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // Callback of the room entry result
    if code == 0 {
       // Room entered successfully.
    }
}

// 5. After successful room entry, you receive an `onRoomInfoChange` notification.
func onRoomInfoChange(roomInfo: VoiceRoomInfo) {
    // Update the room name and other information
}

// 6. After successful room entry, you receive an `onSeatListChange` notification.
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refresh the seat list.
}

// 7. You receive an `onAnchorEnterSeat` notification.
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the mic-on event.
}

```

<span id="model.step7"> </span>
### Step 7. Manage seats.
Anchor
1. An anchor can put a viewer in a seat by passing the `userId` of the viewer and the seat number to `pickSeat`. All members in the room will receive `onSeatListChange` and `onAnchorEnterSeat` notifications.
2. An anchor can remove a user from a seat by passing the seat number to `kickSeat`. All members in the room will receive `onSeatListChange` and `onAnchorLeaveSeat` notifications.
3. An anchor can mute or unmute a viewer by passing the number of the seat occupied by the viewer to `muteSeat`. All members in the room will receive `onSeatListChange` and `onSeatMute` notifications.
4. An anchor can close or reopen a seat by passing the seat number to `closeSeat`. Viewers will be unable to take the closed seat, and all members in the room will receive `onSeatListChange` and `onSeatClose` notifications.
![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)

Viewer
1. A viewer can take a seat by passing the seat number to `enterSeat`. All members in the room will receive `onSeatListChange` and `onAnchorEnterSeat` notifications.
2. A viewer can leave a seat by calling `leaveSeat`. All members in the room will receive `onSeatListChange` and `onAnchorLeaveSeat` notifications.

![](https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png)

After a seat operation, the order in which different notifications are sent is: callbacks > `onSeatListChange` > independent events such as `onAnchorEnterSeat`.

```Swift
// Case 1: the anchor puts a viewer in seat 1.
self.voiceRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // Result callback
}

// 3. The anchor receives a `onSeatListChange` callback, and refreshes the seat list.
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refreshed seat list
}

// 4. The anchor receives a notification about the change of a specific seat, which can be used to determine whether the viewer has successfully taken the seat.
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the mic-on event.
}
```

```Swift
// Case 2: a viewer takes seat 2.
voiceRoom.enterSeat(seatIndex: 2) { (code, message) in
    // Callback of the seat taking result
}

// 3. The viewer receives a `onSeatListChange` callback and refreshes the seat list.
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refreshed seat list
}

// 4. The viewer receives a notification about the change of a specific seat and, depending on whether the seat is the one he or she attempted to take, determines the next step.
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the mic-on event.
}
```

<span id="model.step8"> </span>
### Step 8. Use signaling for invitations.
In [seat management](#model.step7), viewers can take and leave seats without permission from the anchor, and the anchor can put viewers in seats without the viewers’ consent.
If you want viewers and anchors to obtain each other’s consent before performing the above actions in your app, you can use signaling for invitation sending.
Viewer requesting to take seat
1. A viewer calls `sendInvitation` and passes in information including the anchor’s `userId` and custom command words. The function will return an `inviteId`, which should be noted.
2. The anchor receives an `onReceiveNewInvitation` notification, and a window pops up on the UI asking the anchor whether to approve the request.
3. The anchor approves the request, calls `acceptInvitation` and passes in the `inviteId`.
4. The viewer receives a `onInviteeAccepted` notification and calls `enterSeat` to take a seat.

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

```Swift
// Viewer
// 1. Call `sendInvitation` to request to take seat 1.
let inviteId = self.voiceRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // Callback of the request sending result
}
// 4. Take the seat upon receiving approval from the anchor.
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.enterSeat(seatIndex: ) { (code, message) in
            // Callback of the seat taking result
        }
    }
}

// Anchor
// 2. Receive the request.
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 3. Approve the request.
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```

Anchor inviting viewer to seat
1. The anchor calls `sendInvitation` and passes in information including the viewer’s `userId` and custom command words. The function will return an `inviteId`, which should be noted.
2. The viewer receives an `onReceiveNewInvitation` notification, and a window pops up asking the viewer whether to agree to take the seat.
3. The viewer agrees, calls `acceptInvitation`, and passes in the `inviteId`.
4. The anchor receives an `onInviteeAccepted` notification and calls `pickSeat` to put the viewer in the seat.

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)

```java
// Anchor
// 1. Call `sendInvitation` to request to put viewer `123` in seat 2.
let inviteId = self.voiceRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "2") { (code, message) in
    // Callback of the request sending result
}

// 4. Seat the viewer upon receiving approval from the viewer.
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.pickSeat(seatIndex: ) { (code, message) in
            // Callback of the seat taking result
        }
    }
}

// Viewer
// 2. Receive the request.
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 3. Approve the request.
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```

<span id="model.step9"> </span>
### Step 9. Enable text chat and on-screen comments.
- Call `sendRoomTextMsg` to send common text messages. All anchors and viewers in the room will receive the `onRecvRoomTextMsg` callback.
IM has its default content moderation rules. Text messages that contain blocked terms will not be forwarded by the cloud.

```Swift
// Sender: send text messages
self.voiceRoom.sendRoomTextMsg(message: message) { (code, message) in
         
}
// Recipient: listen for text messages
func onRecvRoomTextMsg(message: String, userInfo: VoiceRoomUserInfo) {
    // Handling of the messages received        
}
```
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All anchors and viewers in the room will receive the `onRecvRoomCustomMsg` callback.
 Custom messages are often used to transfer custom signals, e.g., sending and broadcasting likes.
```swift
// For example, a sender can customize commands to distinguish on-screen comments and likes.
// E.g., use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes.
self.vocieRoom.sendRoomCustomMsg(cmd: “CMD_DANMU”, message: "hello world", callback: nil)
self.voiceRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
// Recipient: listen for custom messages
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: VoiceRoomUserInfo) {
    if cmd == "CMD_DANMU" {
        // An on-screen comment is received.
    }
    if cmd == "CMD_LIKE" {
        // A like is received.
    }
}
```


