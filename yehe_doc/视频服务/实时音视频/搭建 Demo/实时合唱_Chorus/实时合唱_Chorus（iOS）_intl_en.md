## Demo UI
You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC’s duet features, including low-latency duet, gift sending and receiving, text chat, etc.
<table>
     <tr>
         <th style="text-align:center">Room Owner</th>  
         <th style="text-align:center">Listener</th>  
     </tr>
<tr>
<tr>
<td><img src="https://main.qcloudimg.com/raw/206ba3492f4a2f18f36b1d5cba4e5558.jpg"/></td>
<td><img src="https://main.qcloudimg.com/raw/e52ccb64cd686f6af1c1f561d7969d36.jpg"/></td>
</tr>
</table>


To quickly enable the duet feature, you can modify the demo app we provide and adapt it to your needs. You may also use the `TUIChorus` component and customize your own UI.
[](id:DemoUI)
## Using the App’s UI
[](id:ui.step1)
### Step 1. Create an application
1. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestChorus` and click **Create**.
3. Click **Next**.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>?This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.


[](id:ui.step2)
### Step 2. Download the application source code
Click [TUIChorus](https://github.com/tencentyun/TUIChorus) to clone or download the source code.

[](id:ui.step3)
### Step 3. Configure application project files
1. In the **Modify Configuration** step, select your platform.
2. Find and open `TUIChorus/Debug/GenerateTestUserSig.swift`.
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
Open `TUIChorus/TUIChorusApp.xcworkspace` with Xcode (11.0 or above) and click the run button.

[](id:ui.step5)
### Step 5. Modify the app’s source code
The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code and UI-related logic. The table below lists the Swift files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
|:-------:|:--------|
| TRTCChorusEnteryControl.swift| The initialization method for all view controllers. You can use the instance to quickly get a `ViewController` object. |
| TRTCCreateChorusViewController | Logic for the room creation view |
| TRTCChorusViewController | Main room views for room owner and listener |

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
2. Enter a room subject and tap **Join**.

### User B
1. Enter a username (**which must be unique**) and log in.
2. Enter the ID of the room created by user A and tap **Join**.<br>

>! You can find the room ID at the top of user A’s room view.

[](id:model)
## Customizing UI
The `Source` folder in the [source code](https://github.com/tencentyun/TUIChorus) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCChorusRoom`. You can find the component's APIs in `TRTCChorusRoom.h` and use them to customize your own UI.
<img src="https://main.qcloudimg.com/raw/2ac6fe9df1b43dae59271f4288f54ef3.png">

[](id:model.step1)
### Step 1. Integrate the SDKs
The `TRTCChorusRoom` component depends on the TRTC SDK and IM SDK. Follow the steps below to integrate them into your project.

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
### Step 3. Import the `TUIChorus` component
**Import the component using CocoaPods**. See below for detailed directions.
1. Copy the `Source`, `Resources`, and `TXAppBasic` folders and the `TUIChorus.podspec` file to your project directory.
2. Add the following dependencies to your `Podfile` and run `pod install` to complete the import.
<dx-codeblock>
::: swift
pod 'TXAppBasic', :path => "TXAppBasic/"
pod 'TXLiteAVSDK_TRTC'
pod 'TUIChorus', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)

### Step 4. Create an instance and log in
1. Call `sharedInstance` of `TRTCChorusRoom` to create an instance that complies with the protocol of `TRTCChorusRoom`, or call `shared` to get a `TRTCChorusRoom` instance. There is no difference between the two methods with respect to API usage.
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
    var chorusRoom: TRTCChorusRoom {
        return TRTCChorusRoom.shared()
    }
    
    // Other code logic
    ......
}
// Set a delegate
self.chorusRoom.setDelegate(delegate: chorusRoomDelegate)

// Below is the calling method. We recommend that you use `weak self` in the closure to prevent circular references. The weak self part is not included in the sample code below.
self.chorusRoom.login(sdkAppId: sdkAppID, userId: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // Your callback business logic        
}
:::
</dx-codeblock>

[](id:model.step5)
### Step 5. Create a room
1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Call `createRoom` to create a room, passing in room attributes such as room ID and whether listeners need the room owner’s consent to speak.
3. After creating the room, call `enterSeat` to take seat No. 1.
4. You will receive an `onSeatListChanget` notification about the change of the seat list, and can update the change to the UI.
5. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat, and mic capturing will be enabled automatically.

![](https://qcloudimg.tencent-cloud.cn/raw/7346adee3042426ca4c9f72777cebd2d.png)

Sample code:
<dx-codeblock>
::: swift
// 1. Set your nickname and profile photo.
self.chorusRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Callback of the result           
}

// 2. Create a room.
let param = RoomParam.init()
param.roomName = "Room name"
param.needRequest = true // Whether your consent is required for listeners to speak
param.coverUrl = "Cover URL"
param.seatCount = 2 // Number of seats in the room. Set it to `2`, one for the room owner and the other for the co-singer.
param.seatInfoList = []

for _ in 0..< param.seatCount {
    let seatInfo = SeatInfo.init()
    param.seatInfoList.append(seatInfo)
}

self.chorusRoom.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { return }
    // Room created successfully
    
    // 3. Take a seat
    self.chorusRoom.enterSeat(seatIndex: 0) { [weak self] (code, message) in
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
2. Get the latest room list from the backend.
>?The room list in the demo app is for demonstration only. The business logic of room lists varies significantly. Tencent Cloud does not provide room list management services currently. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by room owners when they call `createRoom`.
>!If your room list already contains enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select a room, and call `enterRoom` with the room ID passed in to enter.
5. After entering the room, you will receive an `onRoomInfoChange` notification about room change from the component. Record the room information, including room name, whether the room owner’s consent is required for listeners to speak, etc., and update it to the UI.
6. You will receive an `onSeatListChange` notification about seat change from the component. Update the change to the UI.
7. You will also receive an `onAnchorEnterSeat` notification about the occupation of a seat.

![](https://qcloudimg.tencent-cloud.cn/raw/f225633062cf83d749ae8137cbb26fe1.png)
<dx-codeblock>
::: Swift Swift
// 1. Set your nickname and profile photo.
self.chorusRoom.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Callback of the result           
}

// 2. Get the room list from the backend. Suppose it is `roomList`.
let roomList: [Int] = getRoomIDList() // The function you use to get the list of room IDs

// 3. Call `getRoomInfoList` to get details of the rooms.
self.chorusRoom.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [RoomInfo]) in
    // Refresh the UI after getting the result.
}

// 4. Select a room, passing in `roomId` to enter
self.chorusRoom.enterRoom(roomID: roomInfo.roomID) { (code, message) in
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
2. After a duet ends, call `kickSeat`, passing in the seat number to remove the speaker from the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.
3. Call `closeSeat`, passing in a seat number to block/unblock the seat. Listeners cannot take a blocked seat, and all users in the room will receive an `onSeatListChange` notification and an `onSeatClose` notification.
![](https://qcloudimg.tencent-cloud.cn/raw/bbb72bdc50cfd1b5d4b567239b035d32.png)
:::
::: Listener
1. Call `enterSeat`, passing in a seat number to take the seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorEnterSeat` notification.
2. After a duet ends, call `leaveSeat` to leave your seat. All users in the room will receive an `onSeatListChange` notification and an `onAnchorLeaveSeat` notification.

![](https://qcloudimg.tencent-cloud.cn/raw/9747219d17f955530c5e502745008dce.png)

After a seat operation, the order in which different notifications are sent is: callbacks > `onSeatListChange` > independent events such as `onAnchorEnterSeat`.

<dx-codeblock>
::: swift
// Case 1: the room owner places a user in seat No. 1
self.chorusRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    // Callback of the result
}

// 3. The listener receives the `onSeatListChange` callback, and refreshes the seat list
func onSeatListChange(seatInfoList: [ChorusRoomSeatInfo]) {
    // Refreshed seat list
}

// 4. The room owner receives a notification about the change of a specific seat, which can be used to determine whether the user has taken the seat
func onAnchorEnterSeat(index: Int, user: ChorusRoomSeatInfo) {
    // Handle the mic-on event.
}
:::
</dx-codeblock>

<dx-codeblock>
::: swift
// Case 2: a listener takes the co-singer seat
chorusRoom.enterSeat(seatIndex: 1) { (code, message) in
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

![](https://qcloudimg.tencent-cloud.cn/raw/1b37fa84f59c81dc89bf50ce4e30551f.png)

<dx-codeblock>
::: Swift Swift
// Listener
// 1. Call `sendInvitation` to request to take seat 1
let inviteId = self.chorusRoom.sendInvitation(cmd: "ENTER_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // Callback of the result
}
// 2. Place the user in the seat after the invitation is accepted
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chorusRoom.enterSeat(seatIndex: ) { (code, message) in
            // Callback of the result
        }
    }
}

// Room owner
// 1. The room owner receives the request.
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2. The room owner accepts the request.
        self.chorusRoom.acceptInvitation(identifier: identifier, callback: nil)
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

![](https://qcloudimg.tencent-cloud.cn/raw/3a8b31dac680c70d1adac92287e645dd.png)


<dx-codeblock>
::: Swift Swift
// Room owner
// 1. Call `sendInvitation` to invite user `123` to take the co-singer seat
let inviteId = self.chorusRoom.sendInvitation(cmd: "PICK_SEAT", userId: ownerUserId, content: "1") { (code, message) in
    // Callback of the result
}

// 2. Place the user in the seat after the invitation is accepted
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chorusRoom.pickSeat(seatIndex: ) { (code, message) in
            // Callback of the result
        }
    }
}

// Listener
// 1. The listener receives the invitation.
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2. The listener accepts the invitation.
        self.chorusRoom.acceptInvitation(identifier: identifier, callback: nil)
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
  ::: Swift Swift
  // Sender: send text messages
  self.chorusRoom.sendRoomTextMsg(message: message) { (code, message) in
         

}
// Recipient: listen for text messages
func onRecvRoomTextMsg(message: String, userInfo: UserInfo) {
    // Handling of the messages received        
}
:::
</dx-codeblock>
- Call `sendRoomCustomMsg` to send custom (signaling) messages. All speakers and listeners in the room will receive the `onRecvRoomCustomMsg` callback.
 Custom messages are often used to transfer custom signals, e.g., to give and broadcast likes.
  <dx-codeblock>
  ::: Swift Swift
  // For example, a sender can customize commands to distinguish on-screen comments and likes.
  // For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes.
  self.chorusRoom.sendRoomCustomMsg(cmd: “CMD_DANMU”, message: "hello world", callback: nil)
  self.chorusRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
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

