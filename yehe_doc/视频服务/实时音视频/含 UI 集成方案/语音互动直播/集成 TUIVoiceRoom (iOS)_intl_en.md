## Component Overview

`TUIVoiceRoom` is an open-source audio/video UI component. After integrating it into your project, you can make your application support the group audio chat scenario simply by writing a few lines of code. It also supports the [Android](https://intl.cloud.tencent.com/document/product/647/37286) platform. Its basic features are as shown below:

<table class="tablestyle">
<tbody><tr>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/a30e897eabbc6f9104bd41db246f33b1.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/857d3b1651cdf1126f1653e1541b3bba.png" width="250"></td>
<td><img src="https://qcloudimg.tencent-cloud.cn/raw/6ddb805c442974d202ef610db643fa39.png" width="250"></td>
</tr>
</tbody></table>


## Component Integration
### Step 1. Download and import the `TUIVoiceRoom` component

Create the `TUIVoiceRoom` folder at the same level as the `Podfile` in your Xcode project, copy [TXAppBasic](https://github.com/One-time/TUIVoiceRoom/tree/main/iOS/TXAppBasic), [Resources](https://github.com/One-time/TUIVoiceRoom/tree/main/iOS/Resources), [Source](https://github.com/One-time/TUIVoiceRoom/tree/main/iOS/Source), and [TUIVoiceRoom.podspec](https://github.com/One-time/TUIVoiceRoom/blob/main/iOS/TUIVoiceRoom.podspec) files from the [`iOS` directory in the GitHub repository](https://github.com/One-time/TUIVoiceRoom/tree/main/iOS) to the folder, and complete the following import operations:
- Open the project's `Podfile` and import `TUIVocieRoom.podspec` as follows:
```
# `path` is the path of `TXAppBasic.podspec` relative to the `Podfile`
pod 'TXAppBasic', :path => "TUIVoiceRoom/TXAppBasic/"
# `path` is the path of `TUIVoiceRoom.podspec` relative to the `Podfile`
pod 'TUIVoiceRoom', :path => "TUIVoiceRoom/", :subspecs => ["TRTC"]    
```
- Open Terminal, enter the directory of `Podfile`, and run `pod install`.
```
pod install
```

### Step 2. Configure permission requests and obfuscation rules
In `info.plist`, add `Privacy > Microphone Usage Description` to request mic access.

```plist
<key>NSMicrophoneUsageDescription</key>
<string>`TUIVoiceRoom` needs to access your mic to be able to shoot videos with audio.</string>
```

### Step 3. Initialize and log in to the component

```Swift
// Initialize
let mTRTCVoiceRoom = TRTCVoiceRoom.shared()
// Login
mTRTCVoiceRoom.login(sdkAppID: SDKAppID, userId: userId, userSig: userSig) { code, message in
    if code == 0 {
        // Logged in
    }
}
```
**Parameter description:**
- **SDKAppID**: **TRTC application ID**. If you haven't activated the TRTC service, log in to the [TRTC console](https://console.cloud.tencent.com/trtc/app), create a TRTC application, and click **Application Info**. The `SDKAppID` is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/435d5615e0c4075640bb05c49884360c.png)
- **Secretkey**: **TRTC application key**, which corresponds to `SDKAppID`. On the [Application Management](https://console.cloud.tencent.com/trtc/app) page in the TRTC console, the `SecretKey` is as shown below:
- **userId**: ID of the current user, which is a string that can contain only letters (a-z and A-Z), digits (0-9), hyphens (-), and underscores (_). We recommend that you keep it consistent with your user account system.
- **userSig**: Security protection signature calculated based on `SDKAppID`, `userId`, and `Secretkey`. You can click [here](https://console.cloud.tencent.com/trtc/usersigtool) to directly generate a debugging `userSig` online, or you can calculate it on your own by referring to the [demo project](https://github.com/tencentyun/TUIRoom/blob/main/Android/Debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java#L88). For more information, see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166).




### Step 4. Implement the audio chat room
1. **The room owner creates an audio chat room through [TRTCVoiceRoom#createRoom](https://intl.cloud.tencent.com/document/product/647/38171)**.
```Swift
// Initialize the audio chat room parameters
let roomParam = VoiceRoomParam()
roomParam.roomName = "Room name"
roomParam.needRequest = false // Whether your consent is required for listeners to speak
roomParam.coverUrl = "URL of room cover image"
roomParam.seatCount = 7 // Number of room seats. In this example, the number is 7. 6 seats are available after you take one.
roomParam.seatInfoList = []
// Initialize the seat information
for _ in 0..< param.seatCount {
    let seatInfo = VoiceRoomSeatInfo()
    param.seatInfoList.append(seatInfo)
}
// Create a room
mTRTCVoiceRoom.createRoom(roomID: yourRoomID, roomParam: roomParam) { (code, message) in
    if code == 0 {
        // Room created successfully
    }
}
```
2. **A listener enters the audio chat room through [TRTCVoiceRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/38171)**.
```Swift
// 1. A listener calls an API to enter the room
mTRTCVoiceRoom.enterRoom(roomID: roomID) { (code, message) in
    // Callback of the room entry result
    if code == 0 {
       // Entered room successfully
    }
}
```
3. ***A listener mics on through [TRTCVoiceRoom#enterSeat](https://intl.cloud.tencent.com/document/product/647/38171)**.
```Swift
// 1. A listener calls an API to mic on
let seatIndex = 2; // Seat index
mTRTCVoiceRoom.enterSeat(seatIndex: 2) { (code, message) in
    if code == 0 {
        // Mic turned on successfully
    }
}

// 2. The `onSeatListChange` callback is received, and the seat list is refreshed
@Override
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refreshed seat list
}
```
4. **The room owner makes a listener speaker through [TRTCVoiceRoom#pickSeat](https://intl.cloud.tencent.com/document/product/647/38171)**.
```Swift
// 1. The room owner invites a listener to speak
let seatIndex = 2; // Seat index
let userId = "123"; // ID of the user to speak
mTRTCVoiceRoom.pickSeat(seatIndex: 1, userId: "123") { (code, message) in
    if code == 0 {
    }
}

// 2. The `onSeatListChange` callback is received, and the seat list is refreshed
func onSeatListChange(seatInfoList: [VoiceRoomSeatInfo]) {
    // Refreshed seat list
}
```
5. **A listener requests to speak through [TRTCVoiceRoom#sendInvitation](https://intl.cloud.tencent.com/document/product/647/38171)**.
```Swift
// Listener
// 1. A listener calls an API to request to speak
let seatIndex = "1"; // Seat index
let userId = "123"; // User ID
let inviteId = mTRTCVoiceRoom.sendInvitation(cmd: "takeSeat", userId: ownerUserId, content: "1") { (code, message) in
    // Callback of the result
}

// 2. Place the user in the seat after the invitation is accepted
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.mTRTCVoiceRoom.enterSeat(seatIndex: ) { (code, message) in
            // Callback of the result
        }
    }
}

// Room owner
// 1. The room owner receives the request
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "takeSeat" {
        // 2. The room owner accepts the request
        self.mTRTCVoiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```
6. **The room owner invites a listener to speak through [TRTCVoiceRoom#sendInvitation](https://intl.cloud.tencent.com/document/product/647/38171)**.
```Swift
// Room owner
// 1. Call `sendInvitation` to invite user `123` to take seat 2
let inviteId = self.mTRTCVoiceRoom.sendInvitation(cmd: "pickSeat", userId: ownerUserId, content: "2") { (code, message) in
    // Callback of the result
}

// 2. Place the user in the seat after the invitation is accepted
func onInviteeAccepted(identifier: String, invitee: String) {
    if identifier == selfID {
        self.mTRTCVoiceRoom.pickSeat(seatIndex: ) { (code, message) in
            // Callback of the result
        }
    }
}

// Listener
// 1. The listener receives the invitation
func onReceiveNewInvitation(identifier: String, inviter: String, cmd: String, content: String) {
    if cmd == "pickSeat" {
        // 2. The listener accepts the invitation
        self.mTRTCVoiceRoom.acceptInvitation(identifier: identifier, callback: nil)
    }
}
```
7. **Implement text chat through [TRTCVoiceRoom#sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/38171)**.
```Swift
// Sender: Sends text messages
self.mTRTCVoiceRoom.sendRoomTextMsg(message: message) { (code, message) in
         
}

// Receiver: Listens for text messages
func onRecvRoomTextMsg(message: String, userInfo: VoiceRoomUserInfo) {
    // Handling of the messages received        
}
```
8. **Implement on-screen commenting through [TRTCVoiceRoom#sendRoomCustomMsg](https://intl.cloud.tencent.com/document/product/647/38171)**.
```Swift
// For example, a sender can customize commands to distinguish on-screen comments and likes.
// For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes.
self.mTRTCVoiceRoom.sendRoomCustomMsg(cmd: “CMD_DANMU”, message: "hello world", callback: nil)
self.mTRTCVoiceRoom.sendRoomCustomMsg(cmd: "CMD_LIKE", message: "", callback: nil)

// Receiver: Listens for custom messages
func onRecvRoomCustomMsg(cmd: String, message: String, userInfo: VoiceRoomUserInfo) {
    if cmd == "CMD_DANMU" {
        // An on-screen comment is received.
    }
    if cmd == "CMD_LIKE" {
        // A like is received
    }
}
```


## FAQs
If you have any requirements or feedback, contact colleenyu@tencent.com.
