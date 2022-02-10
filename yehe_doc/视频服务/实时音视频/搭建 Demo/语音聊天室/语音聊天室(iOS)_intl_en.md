## Demo UI
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the app we provide to try out TRTC’s audio chat room features, including seat management, low-latency audio interaction, text chat, etc.


To quickly implement the audio chat room feature, you can modify the app we provide and adapt it to your needs. You can also use the `TUIVoiceRoom` component and customize your own UI.

[](id:DemoUI)
## Using the App’s UI

[](id:ui.step1)
### Step 1. Create an application
1. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestVoiceRoom` and click **Create**.
3. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>?The voice chat room feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)
### Step 2. Download the application source code
Clone or download the [TUIVoiceRoom](https://github.com/tencentyun/TUIVoiceRoom) source code.

[](id:ui.step3)
### Step 3. Configure application project files
1. In the **Modify Configuration** step, select your platform.
2. Find and open `TUIVoiceRoom/Debug/GenerateTestUserSig.swift`.
3. Set the following parameters in `GenerateTestUserSig.swift`:
<ul style="margin:0"><li/>SDKAPPID: `0` by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/87dc814a675692e76145d76aab91b414.png">

4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is suitable only for the local execution and debugging of the app**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)
### Step 4. Run the application
Open `TUIVoiceRoom/TUIVoiceRoomApp.xcworkspace` with Xcode (11.0 or above) and click the run button.

[](id:ui.step5)
### Step 5. Modify the app’s source code
The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code and UI-related logic. The table below lists the Swift files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|:-------:|:--------|
|TRTCVoiceRoomEnteryControl.swift| The initialization method for all view controllers. You can use the instance to quickly get a `ViewController` object. |
| TRTCCreateVoiceRoomViewController | Logic for the room creation view |
| TRTCVoiceRoomViewController | Logic for the main room views for room owners and listeners |

Each `TRTC'XXXX'ViewController` folder contains `ViewController`, `RootView`, and `ViewModel`, whose use is described below.

| File | Description |
|:-------:|:--------|
| ViewController.swift | Page controller, which is responsible for routing pages and binding `RootView` and `ViewModel` |
| RootView.swift | Layout of all views |
| ViewModel.swift | View controller, which is responsible for responding to users’ interactions with views and returning response status |

## Tryout
>! You need at least two devices to try out the application.

### User A

1. Enter a username (**which must be unique**) and log in.
2. Click **Create Room**.
2. Type a subject for the conference and tap **Let’s go**.

### User B
1. Enter a username (**which must be unique**) and log in.
2. Enter the ID of the room created by user A and tap **Join**.


>! You can find the room ID at the top of user A’s room view.

[](id:model)
## Customizing UI
The `Source` folder in the [source code](https://github.com/tencentyun/TUIVoiceRoom) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCVoiceRoom`. You can find the component's APIs in `TRTCVoiceRoom.h` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)


[](id:model.step1)
### Step 1. Integrate the SDK
The audio chat room component `TRTCVoiceRoom` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project.

- **Method 1: adding dependencies via CocoaPods**
<dx-codeblock>
::: swift
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
:::
</dx-codeblock>
>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).
- **Method 2: adding dependencies through local files**
If your access to the CocoaPods repository is slow, you can download the ZIP files of the SDKs and manually integrate them into your project as instructed in the documents below.
<table>
<tr><th>SDK</th><th>Download Page</th><th>Integration Guide</th></tr>
<tr>
<td>TRTC SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/35093">Integration document</a></td>
</tr><tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34306">Integration document</a></td>
</tr></table>

[](id:model.step2)
### Step 2. Configure permission requests
Configure the mic permission request by adding `Privacy > Microphone Usage Description` in `info.plist`.

[](id:model.step3)
### Step 3. Import the `TUIVoiceRoom` component
**Import the component using CocoaPods**. See below for detailed directions.
1. Copy the `Source`, `Resources`, and `TXAppBasic` folders and the `TUIVoiceRoom.podspec` file to your project directory.
2. Add the following dependencies to your `Podfile` and run `pod install` to complete the import.
<dx-codeblock>
::: swift
pod 'TXAppBasic', :path => "TXAppBasic/"
pod 'TXLiteAVSDK_TRTC'
pod 'TUIVoiceRoom', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` class method of `TRTCVoiceRoom` to create an instance that complies with `TRTCVoiceRoom`’s protocol, or call the `shared` class method to get a `TRTCVoiceRoomImp` instance. There is no difference between the two methods with respect to API usage.
2. Call the `setDelegate` function to register event callbacks of the component.
3. Call the `login` API to log in to the component, and set the key parameters as described below.
<table>    
<tr><th>Parameter</th><th>Description</th></tr><tr>
<td>SDKAppID</td>
<td>You can view `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend you set it based on your business account system.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. To obtain one, see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr></tr>
<tr>
<td>callback</td>
<td>Login callback. The code is `0` if login is successful.</td>
</tr></table>
<dx-codeblock>
::: Swift Swift
// Swift example
// The class responsible for business logic in your code
class YourController {
    // Calculate attributes to get a singleton object.
    var voiceRoom: TRTCVoiceRoomImp {
        return TRTCVoiceRoomImp.shared()
    }
    
    // Other code logic
    ......
}
// Set a `voiceroom` delegate
self.vocieRoom. setDelegate(delegate: voiceRoomDelegate)

// Below is the calling method. We recommend that you use `weak self` in the closure to prevent circular references. The weak self part is not included in the sample code below.
self.vocieRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // Your callback business logic        
}
:::
</dx-codeblock>

[](id:model.step5)
### Step 5. Create a room and become a speaker
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. A user calls `createRoom` to create an audio chat room, passing in room attributes (e.g. room ID, whether listeners require room owner’s consent to speak, number of seats).
3. After creating the room, the user calls `enterSeat` to become a speaker.
4. You will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
5. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat, and mic capturing will be enabled automatically.

![](https://main.qcloudimg.com/raw/256ebe5ce1426b3f175c8c8b68095d5b.png)

Sample code:
<dx-codeblock>
::: swift
// 1. Set your nickname and profile photo.
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Callback of the result           
}

// 2. Create a room.
let param = VoiceRoomParam.init()
param.roomName = "Room name"
param.needRequest = true // Whether your consent is required for listeners to speak
param.coverUrl = "Cover URL"
param.seatCount = 7 // Number of room seats. In this example, the number is 7. 6 seats are available after you take one.
param.seatInfoList = []

for _ in 0..< param.seatCount {
    let seatInfo = VoiceRoomSeatInfo.init()
    param.seatInfoList.append(seatInfo)
}

self.voiceRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { return }
    // Take a seat after creating the room
    self.voiceRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // Seat taken successfully
        } else {
            // Failed to take a seat
        }
    }
}

// 3. After taking a seat, you receive an `onSeatListChange` notification
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refresh your seat list
}

// 4. You receive an `onAnchorEnterSeat` notification
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
  // Handle the seat taking event
}

:::
</dx-codeblock>

[](id:model.step6)
### Step 6. Enter a room as a listener
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest audio chat room list from the backend.
>?The audio chat room list in the app is for demonstration only. The logic of audio chat room lists varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by the room owner during room creation via the calling of `createRoom`.
>!If your audio chat room list already displays enough room information, you can skip the step of calling `getRoomInfoList`.
4. The user selects a room, and calls `enterRoom` with the room ID passed in to enter the room.
5. After entering the room, you will receive an `onRoomInfoChange` notification about room change from the component. Record the room information, including room name, whether the room owner’s consent is required for listeners to speak, etc., and update it to the UI.
6. You will receive an `onSeatListChange` notification about seat change from the component. Update the change to the UI.
7. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat.


![](https://main.qcloudimg.com/raw/33432f97eb632fbb9710a59cba9e4469.png)


<dx-codeblock>
::: Swift Swift
// 1. Set your nickname and profile photo.
self.voiceRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Callback of the result           
}

// 2. Get the room list from the backend. Suppose it is `roomList`
let roomList: [Int] = getRoomIDList() // The function you use to get the list of room IDs

// 3. Call `getRoomInfoList` to get details of the rooms.
self.voiceRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [VoiceRoomInfo]) in
    // Refresh the UI after getting the result.
}

// 4. Select an audio chat room, and pass in the `roomId` to enter it
self.voiceRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // Callback of the room entry result
    if code == 0 {
       // Entered room
    }
}

// 5. After successful room entry, you receive an `onRoomInfoChange` notification.
func onRoomInfoChange(roomInfo: VoiceRoomInfo) {
    // Update the room name and other information.
}

// 6. You receive an `onSeatListChange` notification
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refresh the seat list
}

// 7. You receive an `onAnchorEnterSeat` notification
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the seat taking event
}
:::
</dx-codeblock>

[](id:model.step7)
### Step 7. Manage seats
<dx-tabs>
::: Room owner
1. Call `pickSeat`, passing in a seat number and the `userId` of a listener to place the listener in the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. Call `kickSeat`, passing in a seat number to remove the speaker from the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.
3. Call `muteSeat`, passing in a seat number to mute/unmute the seat. All members in the room will receive an `onSeatListChange` notification and an `onSeatMute` notification.
4. Call `closeSeat`, passing in a seat number to block/unblock the seat. Listeners cannot take a blocked seat, and all users in the room will receive an `onSeatListChange` notification and an `onSeatClose` notification.
![](https://main.qcloudimg.com/raw/367a0c670d2f9899d0b311ed1f322ea3.png)
:::
::: Listener
1. Call `enterSeat`, passing in a seat number to take the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. Call `leaveSeat` to leave the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

![](https://main.qcloudimg.com/raw/8d385dd387b6255b8512dbff5829e88a.png)

After a seat operation, the order in which different notifications are sent is: callbacks > `onSeatListChange` > independent events such as `onAnchorEnterSeat`.

<dx-codeblock>
::: swift
// Case 1: 1. The room owner places a user in seat No. 1
self.voiceRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // 2. A callback of the result is returned
	if code == 0 {
	}
}

// 3. The listener receives the `onSeatListChange` callback, and refreshes the seat list
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refreshed seat list
}

// 4. The room owner receives a notification about the change of a specific seat, which can be used to determine whether the user has taken the seat
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the seat taking event
}
:::
</dx-codeblock>

<dx-codeblock>
::: swift
// Case 2: 1. A listener takes seat 2
voiceRoom.enterSeat(seatIndex: 2) { (code, message) in
    // 2. A callback of the result is returned
	if code == 0 {
	}
}

// 3. The listener receives the `onSeatListChange` callback, and refreshes the seat list
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refreshed seat list
}

// 4. The listener receives a notification about the change of a specific seat and can determine whether he or she has taken the seat successfully
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the seat taking event
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

![](https://main.qcloudimg.com/raw/5ccdb15f63efa127aa883ca6a7bcd80d.png)

<dx-codeblock>
::: Swift Swift
// Listener
// 1. Call `sendInvitation` to request to take seat 1
let inviteId = self.voiceRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // Callback of the result
}
// 2. Place the user in the seat after the invitation is accepted
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.enterSeat(seatIndex: ) { (code, message) in
            // Callback of the result
        }
    }
}

// Room owner
// 1. The room owner receives the request.
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2. The room owner accepts the request.
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
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

![](https://main.qcloudimg.com/raw/5515f49d6e30410e12cd828b75a8db0b.png)


<dx-codeblock>
::: java java
// Room owner
// 1. Call `sendInvitation` to invite user `123` to take seat 2
let inviteId = self.voiceRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "2") { (code, message) in
    // Callback of the result
}

// 2. Place the user in the seat after the invitation is accepted
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.voiceRoom.pickSeat(seatIndex: ) { (code, message) in
            // Callback of the result
        }
    }
}

// Listener
// 1. The listener receives the invitation.
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2. The listener accepts the invitation.
        self.voiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
</dx-tabs>

[](id:model.step9)
### Step 9. Enable text chat and on-screen comments
- Call `sendRoomTextMsg` to send a common text message. All users in the room will receive an `onRecvRoomTextMsg` callback.
IM has its default content moderation rules. Text messages that contain restricted terms will not be forwarded by the cloud.
<dx-codeblock>
::: Swift Swift
// Sender: send text messages
self.voiceRoom.sendRoomTextMsg(message: message) { (code, message) in
         

}
// Recipient: listen for text messages
func onRecvRoomTextMsg(message: String, userInfo: VoiceRoomUserInfo) {
    // Handling of the messages received        
}
:::
</dx-codeblock>
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All users in the room will receive an `onRecvRoomCustomMsg` callback.
 Custom messages are often used to transfer custom signals, e.g., to give and broadcast likes.
<dx-codeblock>
::: Swift Swift
// For example, a sender can customize commands to distinguish on-screen comments and likes.
// For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes.
self.vocieRoom.sendRoomCustomMsg(cmd: “CMD_DANMU”, message: "hello world", callback: nil)
self.voiceRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
// Receiver: listen for custom messages
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: VoiceRoomUserInfo) {
    if cmd == "CMD_DANMU" {
        // An on-screen comment is received.
    }
    if cmd == "CMD_LIKE" {
        // A like is received.
    }
}
:::
</dx-codeblock>
