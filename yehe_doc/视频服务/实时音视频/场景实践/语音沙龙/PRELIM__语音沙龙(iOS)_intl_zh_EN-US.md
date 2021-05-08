## Demonstration

You can [download](https://intl.cloud.tencent.com/document/product/647/35076) and install the demo we provide to try out TRTC features in the chat salon scenario, including audio chat, mic on/off, low-latency audio interaction, etc.

To quickly enable the chat salon feature, you can modify the demo we provide and adapt it to your needs. You may also use the `TRTCChatSalon` component and customize your own UI.

[](id:DemoUI)

## Using the Demo UI

[](id:ui.step1)

### Step 1. Create an application

1. Log in to the TRTC console and select **Development Assistance** > **[Demo Quick Run](https://console.cloud.tencent.com/trtc/quickstart)**.
2. Enter an application name, e.g., `TestChatSalon`, and click **Create**.

>!The chat salon feature uses two basic PaaS services of Tencent Cloud, namely [TRTC](https://intl.cloud.tencent.com/document/product/647/35078) and [IM](https://intl.cloud.tencent.com/document/product/1047). When you activate TRTC, IM will be activated automatically. IM is a value-added service. See [Value-added Service Pricing](https://intl.cloud.tencent.com/document/product/1047/34350) for its billing details.



[](id:ui.step2)

### Step 2. Download the SDK and demo source code
1. Download the SDK and demo source code for your platform.
2. Click **Next**.
   ![](https://main.qcloudimg.com/raw/3b115019ddfd0866108ed1add30810d8.png)

[](id:ui.step3)
### Step 3. Configure demo project files

1. In the **Modify Configuration** step, select the platform in line with the source package downloaded.
2. Find and open the `iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h` file.
3. Set parameters in `GenerateTestUserSig.h` as follows.
<ul style="margin:0"><li/>SDKAPPID: 0 by default. Set it to the actual `SDKAppID`.
<li/>SECRETKEY: left empty by default. Set it to the actual key.</ul>
<img src="https://main.qcloudimg.com/raw/144433d5562569cd6d0e9ad9804d6c48.png">
4. Click **Next** to complete the creation.
5. After compilation, click **Return to Overview Page**.

>!
>- The method for generating `UserSig` described in this document involves configuring `SECRETKEY` in client code. In this method, `SECRETKEY` may be easily decompiled and reversed, and if your key is leaked, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for the local execution and debugging of the demo**.
>- The correct `UserSig` distribution method is to integrate the calculation code of `UserSig` into your server and provide an application-oriented API. When `UserSig` is needed, your application can send a request to the business server for a dynamic `UserSig`. For more information, see [How do I calculate UserSig on the server?](https://intl.cloud.tencent.com/document/product/647/35166).

[](id:ui.step4)

### Step 4. Run the demo

Use Xcode (version 11.0 or above) to open the `iOS/TRTCScenesDemo/TXLiteAVDemo.xcworkspace` project and click **Run** to start debugging.

[](id:ui.step5)

### Step 5. Modify the demo source code

The `TRTCChatSalonDemo` folder in the source code contains two subfolders: `ui` and `model`. The `ui` subfolder contains the UI code and logic. The table below lists the SWIFT files/folders and the UI views they represent. You can use it for reference when making UI changes.

| File or Folder | Description |
| --------------------------------- | ------------------------------------ |
| NetworkRoomManager | Logic for interactions with the business backend |
| TRTCCreateChatSalonViewController | Logic for the room creation view                   |
| TRTCChatSalonListViewController   | Logic for the list view                        |
| TRTCChatSalonViewController       | Main room views for speakers and listeners |

[](id:model)

## Customizing UI

The `trtcchatsalondemo` folder in the [source code](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCChatSalonDemo) contains two subfolders: `ui` and `model`. The `model` subfolder contains the reusable open-source component `TRTCChatSalon`. You can find the component's APIs in `TRTCChatSalon.h` and use them to customize your own UI.
![](https://main.qcloudimg.com/raw/fcf694c8550664623414604d14ffcd94.png)

[](id:model.step1)

### Step 1. Integrate SDKs

The chat salon component `TRTCChatSalon` depends on the TRTC SDK and IM SDK. Follow the steps below to integrate the two SDKs into your project.

**Method 1: adding dependencies via CocoaPods**

```
pod 'TXIMSDK_iOS'
pod 'TXLiteAVSDK_TRTC'
```

>?You can view the latest version numbers of the two SDKs by visiting their GitHub pages at [TRTC](https://github.com/tencentyun/TRTCSDK) and [IM](https://github.com/tencentyun/TIMSDK).

**Method 2: adding dependencies through local files**
If your access to the CocoaPods repository is slow, you can download the ZIP packages of the SDKs and manually integrate them into your project as instructed in the documents below.

| SDK | Download Page | Integration Guide |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| TRTC SDK | [Download](https://intl.cloud.tencent.com/document/product/647/34615) | [Integration document](https://intl.cloud.tencent.com/document/product/647/35092) |
| IM SDK | [Download](https://intl.cloud.tencent.com/document/product/1047/33996) | [Integration document](https://intl.cloud.tencent.com/document/product/1047/34307) |

[](id:model.step2)

### Step 2. Configure permission requests

Configure the mic permission request by adding `Privacy > Microphone Usage Description` in `info.plist`.

[](id:model.step3)

### Step 3. Import the `TRTCChatSalon` component.

Copy all the files in `iOS/TRTCScenesDemo/TXLiteAVDemo/TRTCChatSalonDemo/model` to your project.


[](id:model.step4)

### Step 4. Create an instance and log in

1. Call the `sharedInstance` class method of `TRTCChatSalon` to create an instance of the component.
2. Call the `setDelegate` method to register event callbacks of the component.
3. Call the `login` method to log in to the component. Set the key parameters as described below.
<table>    
<tr><th>Parameter</th><th>Description</th></tr><tr>
<td>sdkAppId</td>
<td>You can view the `SDKAppID` of your application in the <a href="https://console.cloud.tencent.com/trtc/app">TRTC console</a>.</td>
</tr><tr>
<td>userId</td>
<td>ID of the current user, which is a string that can contain letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_).</td>
</tr><tr>
<td>userSig</td>
<td>Tencent Cloud's proprietary security signature. To obtain one, please see <a href="https://intl.cloud.tencent.com/document/product/647/35166">UserSig</a>.</td>
</tr></tr>
<tr>
<td>callback</td>
<td>Login callback. The code is 0 if login is successful.</td>
</tr></table>
<dx-codeblock>
::: Swift Swift
// Swift sample
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

// Below is the calling method. We recommend you use `weak self` in the closure to prevent circular references. The `weak self` part is not included in the sample code below.
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

![](https://main.qcloudimg.com/raw/0b06ef225f749caa8b1f3a16c2316890.png)
<dx-codeblock>
::: Swift Swift
// 1. Set your nickname and profile photo
self.chatSalon.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Result callback           
}


// 2. Create a room
let param = ChatSalonParam.init()
param.roomName = "Room name"
param.needRequest = true // Whether your consent is required for listeners to speak
param.coverUrl = "Cover URL"
param.seatInfoList = []
self.chatSalon.createRoom(roomID: yourRoomID, roomParam: param) { (code, message) in
    guard code == 0 else { reutrn }
    // 3. Become a speaker after creating the room
    self.chatSalon.enterSeat { [weak self] (code, message) in
        guard let `self` = self else { return }
        if code == 0 {
            // Became a speaker
        } else {
            // Failed to become a speaker
        }
    }
}

// 4. You receive an `onAnchorEnterSeat` notification after becoming a speaker
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
}
:::
</dx-codeblock>


[](id:model.step6)

### Step 6. Enter a room as a listener

1. After performing [step 4](#model.step4) to log in, you can call `setSelfProfile` to set your nickname and profile photo.
2. Get the latest chat salon room list from the backend.
 >?The chat salon list in the demo is for demonstration only. The business logic of the chat salon list varies significantly. Tencent Cloud does not provide list management services for the time being. Please manage the list by yourself.
3. Call `getRoomInfoList` to get short descriptions of the rooms, which are provided by room owners when they call `createRoom` to create the rooms.
 >!If your chat salon list already contains enough room information, you can skip the step of calling `getRoomInfoList`.
4. Select a chat salon, and call `enterRoom` with the room ID passed in to enter.
5. After room entry, you will receive an `onRoomInfoChange` notification about room change from the component. Record the room information, including the room name displayed on the UI, whether the room owner’s consent is required for listeners to speak, etc., and make corresponding changes.
6. You will also receive an `onAnchorEnterSeat` notification that someone becomes a speaker.

![](https://main.qcloudimg.com/raw/b08253d1835ca6e571378af76c84e275.png)
<dx-codeblock>
::: Swift Swift
// 1. Set your nickname and profile photo
self.chatSalon.setSelfProfile(userName: userName, avatarUrl: avatarURL) { (code, message) in
    // Result callback           
}

// 2. Get the room list from the backend. Suppose it is `roomList`
let roomList: [Int] = getRoomIDList() // The function you use to get the list of room IDs

// 3. Call `getRoomInfoList` to get the details of the room
self.chatSalon.getRoomInfoList(roomIdList: roomIdsInt) { (code, message, roomInfos: [ChatSalonInfo]) in
    // Get the result. Refresh the UI
}

// 4. Pass in `roomid` to enter the room
self.chatSalon.enterRoom(roomID: roomInfo.roomID) { (code, message) in
    // Callback for the room entry result
    if code == 0 {
       // Entered room
    }
}

// 5. After successful room entry, you receive an `onRoomInfoChange` notification
func onRoomInfoChange(roomInfo: ChatSalonInfo) {
    // Update the room name and other information
}

// 6. You receive an `onAnchorEnterSeat` notification.
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // Handle the mic-on event
}
:::
</dx-codeblock>

[](id:model.step7)

### Step 7. Mic on/off

<dx-tabs>
::: Room owner

1. A room owner can invite a listener to speak by passing in the `userId` of the listener to `pickSeat`. All members in the room will receive an `onAnchorEnterSeat` notification.
2. A room owner can remove a speaker by passing in the speaker’s `userId` to `kickSeat`. All members in the room will receive an `onAnchorLeaveSeat` notification.

![](https://main.qcloudimg.com/raw/5a590df748b3cedd6eccd7d8e3027168.png)

After a speaker list operation, the order in which different notifications are sent is: callbacks > independent events such as `onAnchorEnterSeat`.

<dx-codeblock>
::: Swift Swift
// 1. The room owner invites a listener to speak
self.chatSalon.pickSeat(userID: "123") { (code, message) in
    // 2. The callback is received
}

// 3. The room owner receives a notification that someone became a speaker, and can determine whether it is the listener he or she invited
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // Handle the mic-on event
}
:::
</dx-codeblock>

:::
::: Listener

1. A listener can become a speaker by calling `enterSeat`. All members in the room will receive an `onAnchorEnterSeat` notification.
2. A speaker can become a listener by calling `leaveSeat`. All members in the room will receive an `onAnchorLeaveSeat` notification.

![](https://main.qcloudimg.com/raw/08f7bf725fa05e1d97a69aacdbd3986a.png)
After a speaker list operation, the order in which different notifications are sent is: callbacks > independent events such as `onAnchorEnterSeat`.
<dx-codeblock>
::: Swift Swift
// 1. The listener becomes a speaker
self.chatSalon.enterSeat { (code, message) in
    // 2. The callback is received
}

// 3. The listener receives a notification that someone became a speaker and can determine whether it is him/herself
func onAnchorEnterSeat(user: ChatSalonUserInfo) {
    // Handle the mic-on event
}
:::
</dx-codeblock>
:::
</dx-tabs>


[](id:model.step8)

### Step 8. Use signaling for invitations

If you want listeners and room owners to obtain each other’s consent before performing the above actions in your application, you can use signaling for invitation sending.

<dx-tabs>
::: Listener requesting to speak

1. A listener calls `sendInvitation`, passing in information including the anchor's `userId` and custom command words. The function will return an `inviteId`, which should be recorded.
2. The room owner receives an `onReceiveNewInvitation` notification, and a window pops up on the UI asking the room owner whether to approve the request.
3. The room owner approves the request, and calls `acceptInvitation` with the `inviteId` passed in.
4. The listener receives an `onInviteeAccepted` notification and calls `enterSeat` to become a speaker.

![](https://main.qcloudimg.com/raw/76f13e8118c49136fcfd99942e56a65e.png)
<dx-codeblock>
::: Swift Swift
// Listener
// 1. Call `sendInvitation` to request to speak
let inviteId = self.chatSalon.sendInvitation(cmd: "ENTER_SEAT", userID: ownerUserId, content: "1") { (code, message) in
    // Callback for the request sending result
}
// 2. Make the listener a speaker upon receiving approval from the listener
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chatSalon.enterSeat { (code, message) in
            // Callback for the result
        }
    }
}

// Room owner
// 1. Receive the request
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "ENTER_SEAT" {
        // 2. Approve the request
        self.chatSalon.acceptInvitation(identifier: identifier, callback: nil)
    }
}
:::
</dx-codeblock>
:::
::: Room owner inviting listener to speak

1. The room owner calls `sendInvitation`, passing in information including the listener's `userId` and custom command words. The function will return an `inviteId`, which should be recorded.
2. The listener receives an `onReceiveNewInvitation` notification, and a window pops up asking the listener whether to agree to speak.
3. The listener agrees, and calls `acceptInvitation` with the `inviteId` passed in.
4. The room owner receives an `onInviteeAccepted` notification and calls `pickSeat` to make the listener a speaker.

![](https://main.qcloudimg.com/raw/3193dd17c510ca5a6583747c0bde0114.png)

<dx-codeblock>
::: Swift Swift
// Room owner
// 1. Call `sendInvitation` to invite listener `123` to speak
let inviteId = self.chatSalon.sendInvitation(cmd: "PICK_SEAT", userID: ownerUserId, content: "2") { (code, message) in
    // Callback for the request sending result
}

// 2. Make the listener a speaker upon receiving approval from the listener
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.chatSalon.pickSeat(userID: ) { (code, message) in
            // Callback for the result
        }
    }
}

// Listener
// 1. Receive the request
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "PICK_SEAT" {
        // 2. Approve the request
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
  Custom messages are often used to transfer custom signals, e.g., giving and broadcasting likes.
  <dx-codeblock>
  ::: Swift Swift
  // For example, a sender can customize commands to distinguish on-screen comments and likes
  // For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes
  self.chatSalon.sendRoomCustomMsg(cmd: “CMD_DANMU”, message: "hello world", callback: nil)
  self.chatSalon.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)
  // Recipient: listen for custom messages
  func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: ChatSalonUserInfo) {
    if cmd == "CMD_DANMU" {
        // An on-screen comment is received
    }
    if cmd == "CMD_LIKE" {
        // A like is received
    }
  }
  :::
  </dx-codeblock>
