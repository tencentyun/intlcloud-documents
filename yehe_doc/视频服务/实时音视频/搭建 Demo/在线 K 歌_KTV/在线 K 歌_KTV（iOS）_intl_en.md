## Demo UI
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC's karaoke features, including low-latency karaoke, seat management, gift sending and receiving, text chat, etc.
<table>
     <tr>
         <th>Room Owner</th>  
         <th>Listener</th>  
     </tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/206ba3492f4a2f18f36b1d5cba4e5558.jpg"/></td>
<td><img src="https://main.qcloudimg.com/raw/e52ccb64cd686f6af1c1f561d7969d36.jpg"/></td>
</tr>
</table>


To quickly enable the karaoke feature, you can modify the demo app we provide and adapt it to your needs. You may also use the `TUIKaraoke` component and customize your own UI.

[](id:DemoUI)
## Using the App’s UI

[](id:ui.step1)
### Step 1. Create an application
1. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestKaraoke` and click **Create**.
3. Click **Next** to skip this step.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>?The voice chat room feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://cloud.tencent.com/document/product/269). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)
### Step 2. Download the application source code
Clone or download the [TUIKaraoke](https://github.com/tencentyun/TUIKaraoke/tree/main/iOS/Source) source code.

[](id:ui.step3)
### Step 3. Configure application project files
1. In the **Modify Configuration** step, select your platform.
2. Find and open `TUIKaraoke/Debug/GenerateTestUserSig.swift`.
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
Open the source code project `TUIKaraoke/TUIKaraokeApp.xcworkspace` with Xcode (version 11.0 or above) and click **Run**.

[](id:ui.step5)
### Step 5. Modify the app’s source code
The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code and UI-related logic. The table below lists the Swift files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|:-------:|:--------|
|TRTCKaraokeEnteryControl.swift| The initialization method for all view controllers. You can use the instance to quickly get a `ViewController` object. |
| TRTCCreateKaraokeViewController | Logic for karaoke room creation page |
| TRTCKaraokeViewController | Main room views for room owner and listener |

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
2. Enter the room subject and click **Sing Together**.

### User B
1. Enter a username (**which must be unique**) and log in.
2. Enter the ID of the room created by user A, and tap **Join**.<br>


>! You can find the room ID at the top of user A’s room view.
<img src="https://qcloudimg.tencent-cloud.cn/raw/746497909c6a802c55205cf13461b804.png" width="320"/>

[](id:model)
## Customizing UI
The `Source` folder in the [source code](https://github.com/tencentyun/TUIKaraoke/tree/main/iOS/Source) contains two subfolders: `ui` and `model`. The `model` folder contains the reusable open-source component `TRTCKaraokeRoom`. You can find the component’s APIs in `TRTCKaraokeRoom.h` and use them to customize your own UI.
<img src="https://main.qcloudimg.com/raw/9c9b6537318b1fa8cd9c6e4e717c361a.png">


[](id:model.step1)
### Step 1. Integrate the SDKs
The `TRTCKaraokeRoom` component depends on the TRTC SDK and IM SDK. Follow the steps below to integrate them into your project.

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
<td><a href="https://intl.cloud.tencent.com/document/product/647/35092">Integration Documentation</a></td>
</tr><tr>
<td>IM SDK</td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/33996">Download</a></td>
<td><a href="https://intl.cloud.tencent.com/document/product/1047/34307">Integration Documentation</a></td>
</tr></table>

[](id:model.step2)
### Step 2. Configure permission requests
In `info.plist`, add `Privacy > Microphone Usage Description` to request mic access.

[](id:model.step3)
### Step 3. Import the `TUIKaraoke` component
**Import the component using CocoaPods**. See below for detailed directions.
1. Copy the `Source`, `Resources`, and `TXAppBasic` folders as well as the `TUIKaraoke.podspec` file in the demo directory to your project directory.
2. Add the following dependencies to your `Podfile` and run `pod install` to complete the import.
<dx-codeblock>
::: swift
pod 'TXAppBasic', :path => "TXAppBasic/"
pod 'TXLiteAVSDK_TRTC'
pod 'TUIKaraoke', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` class method of `TRTCKaraokeRoom` to create an instance that complies with `TRTCKaraokeRoom's` protocol, or call the `shared` class method to get a `TRTCKaraokeRoom` instance. There is no difference between the two methods with respect to API usage.
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
    var karaokeRoom: TRTCKaraokeRoom {
        return TRTCKaraokeRoom.shared()
    }
    
    // Other code logic
    ......
}
// Set the karaoke proxy
self.karaokeRoom.setDelegate(delegate: karaokeRoomDelegate)

// Below is the calling method. We recommend that you use `weak self` in the closure to prevent circular references. The weak self part is not included in the sample code below.
self.karaokeRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // Your callback business logic        
}
:::
</dx-codeblock>

[](id:model.step5)
### Step 5. Create a room
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. A user calls `createRoom` to create a karaoke room, passing in room attributes (e.g., room ID, whether listeners require room owner’s consent to speak, number of seats).
3. After creating the room, call `enterSeat` to take a seat.
4. You will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
5. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat, and mic capturing will be enabled automatically.

<img src="https://qcloudimg.tencent-cloud.cn/raw/c925337d62289d8c3cdba4714145f5cb.png">

Sample code:
<dx-codeblock>
::: swift
// 1. Set your nickname and profile photo.
self.karaokeRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Callback of the result           
}

// 2. Create a room.
let param = RoomParam.init()
param.roomName = "Room name"
param.needRequest = true // Whether your consent is required for listeners to speak
param.coverUrl = "Cover URL"
param.seatCount = 8 // Number of seats in the room. Set it to `8`.
param.seatInfoList = []

for _ in 0..< param.seatCount {
    let seatInfo = SeatInfo.init()
    param.seatInfoList.append(seatInfo)
}

self.karaokeRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { return }
    // Room created successfully
    
    // 3. Take a seat
    self.karaokeRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // Seat taken successfully
        } else {
            // Failed to take a seat
        }
    }
} 

// 4. After taking a seat, you receive an `onSeatListChange` notification
func onSeatListChange(seatInfoList: [SeatInfo]) {
    // Refresh your seat list
}

// 5. You receive an `onAnchorEnterSeat` notification
func onAnchorEnterSeat(index: Int, user: UserInfo) {
  // Handle the seat taking event
}

:::
</dx-codeblock>

[](id:model.step6)
### Step 6. Enter a room as a listener
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest karaoke room list from the backend.
>?The room list in the demo app is for demonstration only. The business logic of karaoke room lists varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the karaoke rooms, which are provided by room owners when they call `createRoom`.
>!If your karaoke room list already contains enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select a karaoke room, and call `enterRoom` with the room ID passed in to enter the room.
5. After entering the room, you will receive an `onRoomInfoChange` notification about room change from the component. Record the room information, including room name, whether the room owner’s consent is required for listeners to speak, etc., and update it to the UI.
6. You will receive an `onSeatListChange` notification about seat change from the component. Update the change to the UI.
7. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat.

<img src="https://qcloudimg.tencent-cloud.cn/raw/0a96afd3948228a6f1fd19eb0b7b1b3e.png">
<dx-codeblock>
::: Swift Swift
// 1. Set your nickname and profile photo.
self.karaokeRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Callback of the result           
}

// 2. Get the room list from the backend. Suppose it is `roomList`.
let roomList: [Int] = getRoomIDList() // The function you use to get the list of room IDs

// 3. Call `getRoomInfoList` to get details of the rooms.
self.karaokeRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [RoomInfo]) in
    // Refresh the UI after getting the result.
}

// 4. Select a karaoke room and pass in the `roomId` to enter it
self.karaokeRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // Callback of the room entry result
    if code == 0 {
       // Entered room
    }
}

// 5. After successful room entry, you receive an `onRoomInfoChange` notification.
func onRoomInfoChange(roomInfo: RoomInfo) {
    // Update the room name and other information.
}

// 6. You receive an `onSeatListChange` notification
func onSeatListChange(seatInfoList: [SeatInfo]) {
    // Refresh the seat list
}

// 7. You receive an `onAnchorEnterSeat` notification
func onAnchorEnterSeat(index: Int, user: UserInfo) {
    // Handle the mic-on event.
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
<img src="https://qcloudimg.tencent-cloud.cn/raw/b6074cf63c373e233b0a1a1d45422eda.png">
:::
::: Listener
1. Call `enterSeat`, passing in a seat number to take the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. Call `leaveSeat` to leave the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

<img src="https://qcloudimg.tencent-cloud.cn/raw/32075b60078151ad6988efffeb9aa49f.png">

After a seat operation, the order in which different notifications are sent is: callbacks > `onSeatListChange` > independent events such as `onAnchorEnterSeat`.

<dx-codeblock>
::: swift
// Case 1: the room owner places a user in seat No. 1
self.karaokeRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // Callback of the result
}

// 3. The listener receives the `onSeatListChange` callback, and refreshes the seat list
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refreshed seat list
}

// 4. The room owner receives a notification about the change of a specific seat, which can be used to determine whether the user has taken the seat
func onAnchorEnterSeat(index: Int, user: VoiceRoomUserInfo) {
    // Handle the mic-on event.
}
:::
</dx-codeblock>

<dx-codeblock>
::: swift
// Case 2: a listener takes seat 2
karaokeRoom.enterSeat(seatIndex: 2) { (code, message) in
    // Callback of the result
}

// 3. The listener receives the `onSeatListChange` callback, and refreshes the seat list
func onSeatListChange(seatInfoList: [SeatInfo]) {
    // Refreshed seat list
}

// 4. The listener receives a notification about the change of a specific seat and can determine whether he or she has taken the seat successfully
func onAnchorEnterSeat(index: Int, user: UserInfo) {
    // Handle the mic-on event.
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

<img src="https://qcloudimg.tencent-cloud.cn/raw/1396c2611b83bcc5532edceb97d94f94.png">

<dx-codeblock>
::: Swift Swift
// Listener
// 1. Call `sendInvitation` to request to take seat 1
let inviteId = self.karaokeRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // Callback of the result
}
// 2. Place the user in the seat after the invitation is accepted
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.karaokeRoom.enterSeat(seatIndex: ) { (code, message) in
            // Callback of the result
        }
    }
}

// Room owner
// 1. The room owner receives the request.
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2. The room owner accepts the request.
        self.karaokeRoom.acceptInvitation(identifier: identifier, callback: nil)
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

<img src="https://qcloudimg.tencent-cloud.cn/raw/d9ae981d95441aa4e535ee1921d31ed6.png">


<dx-codeblock>
::: java java
// Room owner
// 1. Call `sendInvitation` to invite user `123` to take seat 2
let inviteId = self.karaokeRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "2") { (code, message) in
    // Callback of the result
}

// 2. Place the user in the seat after the invitation is accepted
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.karaokeRoom.pickSeat(seatIndex: ) { (code, message) in
            // Callback of the result
        }
    }
}

// Listener
// 1. The listener receives the invitation.
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2. The listener accepts the invitation.
        self.karaokeRoom.acceptInvitation(identifier: identifier, callback: nil)
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
self.karaokeRoom.sendRoomTextMsg(message: message) { (code, message) in
         

}
// Recipient: listen for text messages
func onRecvRoomTextMsg(message: String, userInfo: UserInfo) {
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
self.karaokeRoom.sendRoomCustomMsg(cmd: "CMD_DANMU", message: "hello world", callback: nil)
self.karaokeRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
// Recipient: listen for custom messages
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: UserInfo) {
    if cmd == "CMD_DANMU" {
        // An on-screen comment is received.
    }
    if cmd == "CMD_LIKE" {
        // A like is received.
    }
}
:::
</dx-codeblock>
