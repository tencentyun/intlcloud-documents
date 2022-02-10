## Demo UI

You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo app we provide to try out TRTC features in the chat salon scenario, including audio chat, mic on/off, low-latency audio interaction, etc.

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

To quickly enable the chat salon feature, you can modify the demo app we provide and adapt it to your needs. You may also use the `TUIChatSalon` component and customize your own UI.

[](id:DemoUI)

## Using the App’s UI

[](id:ui.step1)

### Step 1. Create an application

1. In the TRTC console, select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name such as `TestChatSalon` and click **Create**.
3. Click **Next** to skip the source code download step.

![](https://main.qcloudimg.com/raw/9f4c878c0a150d496786574cae2e89f9.png)

>!This feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)

### Step 2. Download the application source code
Click [TUIChatSalon](https://github.com/tencentyun/TUIChatSalon) to clone or download the source code.

[](id:ui.step3)
### Step 3. Configure application project files

1. In the **Modify Configuration** step, select your platform.
2. Find and open `TUIChatSalon/Debug/GenerateTestUserSig.swift`.
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

Open `TUIChatSalon/TUIChatSalonApp.xcworkspace` with Xcode (11.0 or above) and click the run button.

[](id:ui.step5)

### Step 5. Modify the app’s source code

The `Source` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains UI code and UI-related logic. The table below lists the Swift files (folders) and the UI views they represent. You can refer to it when making UI changes.

| File or Folder | Description |
| --------------------------------- | ------------------------------------ |
| TRTCChatSalonEntryControl.swift  | The initialization method for all view controllers. You can use the instance to quickly get a `ViewController` object. |
| TRTCCreateChatSalonViewController | Logic for the room creation view                   |
| TRTCChatSalonViewController       | The main room views for room owner and listener |

## Tryout
>! You need at least two devices to try out the application.

### User A

1. Enter a username (**which must be unique**) and log in.

   ![](https://qcloudimg.tencent-cloud.cn/raw/ae3d6bc2f1900dbc5537f2f3f4fca529.png)

2. Click **Create Room**.

   ![](https://qcloudimg.tencent-cloud.cn/raw/aef2012fdb5a6441dae9406f0539164d.png)

3. Type a subject for the conference and tap **Let’s go**.

### User B
1. Enter a username (**which must be unique**) and log in.

   ![](https://qcloudimg.tencent-cloud.cn/raw/7596d1bd53d84d61436a499a92d52240.png)

2. Enter the ID of the room created by user A and tap **Join**.

   ![](https://qcloudimg.tencent-cloud.cn/raw/68eea3143e1d57158725d80da7895e51.png)


>! You can find the room ID at the top of user A’s room view.
>
>![](https://qcloudimg.tencent-cloud.cn/raw/ae36a652f641761fccd5bdad041a9220.png)

[](id:model)

## Customizing Your Own UI

The `Source` folder in the [source code](https://github.com/tencentyun/TUIChatSalon) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TUIChatSalon`. You can find the component's APIs in `TRTCChatSalon.h` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/319beb14d72a43120e102380278aa1da.png)

[](id:model.step1)

### Step 1. Integrate the SDKs

The chat salon component `TUIChatSalon` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate them into your project.

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
Configure the mic permission request by adding `Privacy > Microphone Usage Description` in `info.plist`.

[](id:model.step3)
### Step 3. Import the `TUIChatSalon` component
**Import the component using CocoaPods**. See below for detailed directions.
1. Copy the `Source`, `Resources`, and `TXAppBasic` folders and the `TUIChatSalon.podspec` file to your project directory.
2. Add the following dependencies to your `Podfile` and run `pod install` to complete the import.
<dx-codeblock>
::: swift
pod 'TXAppBasic', :path => "TXAppBasic/"
pod 'TXLiteAVSDK_TRTC'
pod 'TUIChatSalon', :path => "./", :subspecs => ["TRTC"] 
:::
</dx-codeblock>

[](id:model.step4)
### Step 4. Create an instance and log in
1. Call the `sharedInstance` class method of `TUIChatSalon` to create an instance of the component.
2. Call the `setDelegate` method to register event callbacks of the component.
3. Call the `login` method to log in to the component. Set the key parameters as described below.
<table>    
<tr><th>Parameter</th><th>Description</th></tr><tr>
<td>SDKAppID</td>
<td>You can view `SDKAppID` in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend you set it based on your business account system.</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. For how to obtain it, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
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
    var chatSalon: TRTCChatSalon {
        return TRTCChatSalon.shared()
    }
    

    // Other code logic
    ......

}
// Set the `chatSalon` delegate.
self.chatSalon.setDelegate(delegate: self)

// Below is the calling method. We recommend that you use `weak self` in the closure to prevent circular references. The weak self part is not included in the sample code below.
self.chatSalon.login(sdkAppID: sdkAppID, userID: userId, userSig: userSig) { [weak self] (code, message) in
    guard let `self` = self else { return }
    // Your callback business logic        
}
:::
</dx-codeblock>

[](id:model.step5)

### Step 5. Create a room and become a speaker

1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Call `createRoom` to create a chat salon, passing in room-related parameters such as room ID, whether your consent is required for listeners to speak, and the room type.
3. You will receive an `onAnchorEnterSeat` notification that someone becomes a speaker, and mic capturing will be enabled automatically.

![](https://main.qcloudimg.com/raw/dfe6ed5d0c973e399e834eb233c96ec6.png)
<dx-codeblock>
::: Swift Swift
// 1. Set your nickname and profile photo.
self.chatSalon.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Callback of the result           
}


// 2. Create a room.
let param = ChatSalonParam.init()
param.roomName = "Room name"
param.needRequest = true // Whether your consent is required for listeners to speak
param.coverUrl = "Cover URL"
param.seatInfoList = []
self.chatSalon.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { return }
    // 3. Become a speaker.
    self.chatSalon.enterSeat { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // Seat taken successfully
        } else {
            // Failed to take a seat
        }
    }
}

// 4. You receive an `onAnchorEnterSeat` notification after becoming a speaker.
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
}
:::
</dx-codeblock>


[](id:model.step6)

### Step 6. Enter a room as a listener

1. After performing [step 4](#model.step4) to log in, call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest chat salon room list from the backend.
>?The chat salon list in the demo app is for demonstration only. The business logic of the chat salon list varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by room owners when they call `createRoom`.
>!If your chat salon list already contains enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select a chat salon, and call `enterRoom` with the room ID passed in to enter.
5. After entering the room, you will receive an `onRoomInfoChange` notification about room change from the component. Record the room information, including room name, whether the room owner’s consent is required for listeners to speak, etc., and update it to the UI.
6. You will also receive an `onAnchorEnterSeat` notification that someone becomes a speaker.

![](https://main.qcloudimg.com/raw/6fbabfa4e217022cf3d05677e4a45538.png)
<dx-codeblock>
::: Swift Swift
// 1. Set your nickname and profile photo.
self.chatSalon.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Callback of the result           
}

// 2. Get the room list from the backend. Suppose it is `roomList`.
let roomList: [Int] = getRoomIDList() // The function you use to get the list of room IDs

// 3. Call `getRoomInfoList` to get details of the rooms.
self.chatSalon.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [ChatSalonInfo]) in
    // Refresh the UI after getting the result.
}

// 4. Pass in `roomId` to enter a room.
self.chatSalon.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // Callback of the room entry result
    if code == 0 {
       // Entered room
    }
}

// 5. After successful room entry, you receive an `onRoomInfoChange` notification.
func onRoomInfoChange(roomInfo: ChatSalonInfo) {
    // Update the room name and other information.
}

// 6. You receive an `onAnchorEnterSeat` notification.
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // Handle the mic-on event.
}
:::
</dx-codeblock>

[](id:model.step7)

### Step 7. Mic on/off

<dx-tabs>
::: Room owner

1. A room owner can make a listener speaker by passing in the `userId` of the listener to `pickSeat`. All members in the room will receive an `onAnchorEnterSeat` notification.
2. A room owner can remove a speaker by passing in the speaker’s `userId` to `kickSeat`. All members in the room will receive an `onAnchorLeaveSeat` notification.

![](https://qcloudimg.tencent-cloud.cn/raw/0eb3dbe14b166a24252f0efb45a6b24f.png)

After a speaker list operation, the order in which different notifications are sent is: callbacks > independent events such as `onAnchorEnterSeat`.

<dx-codeblock>
::: Swift Swift
// 1. The room owner makes a listener speaker.
self.chatSalon.pickSeat(userID: "123") { (code, message) in
    // 2. A callback is returned.
}

// 3. The room owner receives a notification that someone became a speaker, and can determine whether it is the listener he or she intended to make speaker.
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // Handle the mic-on event.
}
:::
</dx-codeblock>

:::
::: Listener

1. A listener can become a speaker by calling `enterSeat`. All members in the room will receive an `onAnchorEnterSeat` notification.
2. A speaker can become a listener by calling `leaveSeat`. All members in the room will receive an `onAnchorLeaveSeat` notification.

![](https://main.qcloudimg.com/raw/c9611b5017536604f63333ce7c19c309.png)
After a speaker list operation, the order in which different notifications are sent is: callbacks > independent events such as `onAnchorEnterSeat`.
<dx-codeblock>
::: Swift Swift
// 1. A listener calls an API to become a speaker.
self.chatSalon.enterSeat { (code, message) in
    // 2. A callback is returned.
}

// 3. The listener receives a notification that someone became a speaker and can determine whether it is him/herself.
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // Handle the mic-on event.
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step8)

### Step 8. Use signaling for invitations

If you want listeners and room owners to obtain each other’s consent before performing the above actions in your application, you can use signaling for invitation sending.

<dx-tabs>
::: Listener requesting to take seat

1. A listener calls `sendInvitation`, passing in information including the room owner’s `userId` and custom command words. The API will return an `inviteId`, which should be recorded.
2. The room owner receives an `onReceiveNewInvitation` notification, and a window pops up on the UI asking the room owner whether to accept the request.
3. The room owner calls `acceptInvitation` with the `inviteId` passed in to accept the request.
4. The listener receives an `onInviteeAccepted` notification and calls `enterSeat` to become a speaker.

![](https://main.qcloudimg.com/raw/71b657c495cb52317c4c32a919407b36.png)
<dx-codeblock>
::: Swift Swift
// Listener
// 1. A listener calls `sendInvitation` to request to speak.
let inviteId = self.chatSalon.sendInvitation(cmd: "ENTER_SEAT", userID: ownerUserId, content: "1") { (code, message) in
    // Callback of the result
}
// 2. Place the user in the seat after the invitation is accepted
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chatSalon.enterSeat { (code, message) in
            // Callback of the result
        }
    }
}

// Room owner
// 1. The room owner receives the request.
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2. The room owner accepts the request.
        self.chatSalon.acceptInvitation(identifier: identifier, callback: nil)
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

![](https://main.qcloudimg.com/raw/60025544abae69e22de22a4b81bf6951.png)

<dx-codeblock>
::: Swift Swift
// Room owner
// 1. The room owner calls `sendInvitation` to invite user `123` to speak.
let inviteId = self.chatSalon.sendInvitation(cmd: "PICK_SEAT", userID: ownerUserId, content: "2") { (code, message) in
    // Callback of the result
}

// 2. Place the user in the seat after the invitation is accepted
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chatSalon.pickSeat(userID: ) { (code, message) in
            // Callback of the result
        }
    }
}

// Listener
// 1. The listener receives the invitation.
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2. The listener accepts the invitation.
        self.chatSalon.acceptInvitation(identifier: identifier, callback: nil)
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
  self.chatSalon.sendRoomTextMsg(message: message) { (code, message) in
        

}
// Recipient: listen for text messages
func onRecvRoomTextMsg(message: String, userInfo: ChatSalonUserInfo) {
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
  self.chatSalon.sendRoomCustomMsg(cmd: “CMD_DANMU”, message: "hello world", callback: nil)
  self.chatSalon.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
  // Recipient: listen for custom messages
  func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: ChatSalonUserInfo) {
    if cmd == "CMD_DANMU" {
        // An on-screen comment is received.
    }
    if cmd == "CMD_LIKE" {
        // A like is received.
    }
  }
  :::
  </dx-codeblock>
