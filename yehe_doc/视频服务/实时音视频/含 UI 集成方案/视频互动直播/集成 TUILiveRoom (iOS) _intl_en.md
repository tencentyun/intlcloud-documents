## Component Overview

`TUILiveRoom` is an open-source audio/video UI component. After integrating it into your project, you can make your application support the interactive video live streaming scenario simply by writing a few lines of code. It also supports [Android](https://intl.cloud.tencent.com/document/product/647/36061) and [Flutter](https://intl.cloud.tencent.com/document/product/647/41944) platforms. Its basic features are as shown below:

<table>
<tr>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/34337da1f6427b9a834f6562eba5c663.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/52eb1656b5a892e6da65f49a1d503735.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/70c9e1e7290592f8c7892b236fb1061e.jpg"/></td>
<td><img width="260" height="561" src="https://qcloudimg.tencent-cloud.cn/raw/ed8c3666aa03951c6d0d9cfe2dccc495.jpg"/></td>
</tr>
</table>


## Component Integration

### Step 1. Download and import the `TUILiveRoom` component
Create the `TUILiveRoom` folder at the same level as the `Podfile` in your Xcode project, copy the [TXAppBasic](https://github.com/One-time/TUILiveRoom/tree/main/iOS/TXAppBasic), [TCBeautyKit](https://github.com/One-time/TUILiveRoom/tree/main/iOS/TCBeautyKit), [Resources](https://github.com/One-time/TUILiveRoom/tree/main/iOS/Resources), [Source](https://github.com/One-time/TUILiveRoom/tree/main/iOS/Source) and [TUIVoiceRoom.podspec](https://github.com/One-time/TUILiveRoom/blob/main/iOS/TUILiveRoom.podspec) files from the [`iOS` directory in the GitHub repository](https://github.com/One-time/TUILiveRoom/tree/main/iOS) to the folder, and complete the following import operations:
- Open the project's `Podfile` and import `TUILiveRoom.podspec` as follows:
```
# :path => "Points to the relative path of the directory of `TXAppBasic.podspec`"
pod 'TXAppBasic', :path => "TUILiveRoom/TXAppBasic/"

# :path => "Points to the relative path of the directory of `TCBeautyKit.podspec`"
pod 'TCBeautyKit', :path => "TUILiveRoom/TCBeautyKit/"

# :path => "Points to the relative path of the directory of `TUILiveRoom.podspec`"
pod 'TUILiveRoom', :path => "TUILiveRoom/", :subspecs => ["TRTC"]
```
- Open Terminal, enter the directory of `Podfile`, and run `pod install`.
```
pod install
```

### Step 2. Configure permission requests and obfuscation rules
Add `Privacy > Microphone Usage Description` (mic access request) and `Privacy > Camera Usage Description` (camera access request) to the `info.plist` file in sequence.

```plist
<key>NSMicrophoneUsageDescription</key>
<string>`TUILiveRoom` needs to access your mic to be able to shoot videos with audio.</string>
<key>NSCameraUsageDescription</key>
<string>`TUILiveRoom` needs to access your camera to be able to shoot videos with images.</string>
```

### Step 3. Initialize and log in to the component
```Swift
 let mTRTCLiveRoom = TRTCLiveRoom()
 // useCDNFirst: `true` means that the audience watches live streams over CDNs, and `false` means that the audience watches live streams in the low latency mode.
 //CDNPlayDomain: The playback domain name for CDN live streaming
 let config = TRTCLiveRoomConfig(useCDNFirst: useCDNFirst, cdnPlayDomain: yourCDNPlayDomain)
 mTRTCLiveRoom.login(SDKAPPID, userID, userSig, config) { (code, error) in
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

### Step 4. Implement an interactive video live room
1. **The anchor starts streaming through [TRTCLiveRoom#createRoom](https://intl.cloud.tencent.com/document/product/647/37332)**.
```Swift
// 1. Set your username and profile photo as an anchor
 mTRTCLiveRoom.setSelfProfile(name: "A", avatarURL: "faceUrl", callback: nil)

 // 2. Enable camera preview and set beauty filters before streaming
 let view = UIView()
 parentView.add(view)
 mTRTCLiveRoom.startCameraPreview(frontCamera: true, view: view, callback: nil)
 mTRTCLiveRoom.getBeautyManager().setBeautyStyle(.nature)
 mTRTCLiveRoom.getBeautyManager().setBeautyLevel(6)

 // 3. Create a room
 let param = TRTCCreateRoomParam(roomName: "Test room", coverUrl: "")
 mTRTCLiveRoom.createRoom(roomID: 123456789, roomParam: param) { [weak self] (code, error) in
  if code == 0 {
    // 4. Start streaming and publish the streams to CDNs
    self?.mTRTCLiveRoom.startPublish(streamID: mSelfUserId + "_stream", callback: nil)
  }
}
```
2. **Audience watches through [TRTCLiveRoom#enterRoom](https://intl.cloud.tencent.com/document/product/647/37332)**.
```Swift
// 1. Get the room list from the backend. Suppose it is `roomList`
 var roomList: [UInt32] = GetRoomList()

 // 2. Call `getRoomInfos` to get the details of the room
 mTRTCLiveRoom.getRoomInfos(roomIDs: roomList, callback: { (code, msg, list) in
    if code == 0 {
      // After getting the room information, you can display on the anchor list page the anchor's nickname, profile photo, and other information
    }
 })

 // 3. Select a `roomid` and enter the room
 mTRTCLiveRoom.enterRoom(roomID: roomID, callback: callback)

 // 4. After receiving the notification about the anchor’s entry, start playback
 public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
   // 5. Play the anchor's video
   mTRTCLiveRoom.startPlay(userID: userID, view: renderView, callback: nil) 
 }
```
3. **Audience member and the anchor co-anchor together through [TRTCLiveRoom#requestJoinAnchor](https://intl.cloud.tencent.com/document/product/647/37332)**.
```Swift
// Audience:
  // 1. The audience member sends a co-anchoring request
  mTRTCLiveRoom.requestJoinAnchor(reason: mSelfUserId + "requested to co-anchor", responseCallback: { [weak self] (agreed, reason) in 
      // 4. The request is accepted by the anchor
       if agreed {
        // 5. The audience member turns on the camera and starts pushing streams
        self?.mTRTCLiveRoom.startCameraPreview(frontCamera: true, view: localView, callback: nil)
        self?.mTRTCLiveRoom.startPublish(streamID: streamID, callback: nil)
       }        
  }, callback: callback)

  // Anchor:
  // 2. The anchor receives the co-anchoring request
  public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestJoinAnchor user: TRTCLiveUserInfo, reason: String?, timeout: Double) {
    // 3. The anchor accepts the co-anchoring request
    mTRTCLiveRoom.responseJoinAnchor(userID: userID, agree: true, reason: "agreed to co-anchor")
  }

  // 6. The anchor receives a notification that the co-anchoring audience member has turned on the mic
  public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
    // 7. The anchor plays the audience member’s video
    mTRTCLiveRoom.startPlay(userID: userID, view: view, callback: nil)
  }
```
4. **Anchors compete through [TRTCLiveRoom#requestRoomPK](https://intl.cloud.tencent.com/document/product/647/37332)**.
```Swift
// Anchor A:
// Create room 12345
mTRTCLiveRoom.createRoom(roomID: 12345, roomParam: param, callback: nil)

// 1. Send a competition request to anchor B
mTRTCLiveRoom.requestRoomPK(roomID: 54321, userID: "B", responseCallback: { (agree, reason) in
  // 5. Receive a callback of whether the request is accepted by anchor B
  if agree {
  }       
}, callback: callback)

// Anchor A receives the callback of anchor B’s entry
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
  // 6. After receiving the notification of anchor B’s entry, anchor A plays anchor B's video image
  mTRTCLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}

// Anchor B:
// Create room 54321
mTRTCLiveRoom.createRoom(roomID: 54321, roomParam: param, callback: nil)

// 2. Receive anchor A’s request
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRequestRoomPK user: TRTCLiveUserInfo, timeout: Double) {
  // 3. Accept anchor A's request
  mTRTCLiveRoom.responseRoomPK(userID: userID, agree: true, reason: reason)
}

public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onAnchorEnter userID: String) {
  // 4. Receive a notification about anchor A’s entry and play anchor A's video
  mTRTCLiveRoom.startPlay(userID: userID, view: view, callback: callback)
}
```
5. **Implement text chat through [TRTCLiveRoom#sendRoomTextMsg](https://intl.cloud.tencent.com/document/product/647/37332)**.
```Swift
// Sender: Sends text messages
mTRTCLiveRoom.sendRoomTextMsg(message: "Hello Word!", callback: callback)
// Receiver: Listens for text messages
mTRTCLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRecvRoomTextMsg message: String, fromUser user: TRTCLiveUserInfo) {
  debugPrint("Received a text message from \(user.userName): \(message)")
}
```
6. **Implement on-screen commenting through [TRTCLiveRoom#sendRoomCustomMsg](https://intl.cloud.tencent.com/document/product/647/37332)**.
```Swift
// Sender: Customize CMD to distinguish on-screen comments and likes
// For example, use "CMD_DANMU" to indicate on-screen comments and "CMD_LIKE" to indicate likes.
mTRTCLiveRoom.sendRoomCustomMsg(command: "CMD_DANMU", message: "Hello world", callback: nil)
mTRTCLiveRoom.sendRoomCustomMsg(command: "CMD_LIKE", message: "", callback: nil)
// Receiver: Listens for custom messages
mTRTCLiveRoom.delegate = self
public func trtcLiveRoom(_ trtcLiveRoom: TRTCLiveRoom, onRecvRoomCustomMsg command: String, message: String, fromUser user: TRTCLiveUserInfo) {
  if "CMD_DANMU" == command {
    // An on-screen comment is received
    debugPrint("Received an on-screen comment from \(user.userName): \(message)")
  } else if "CMD_LIKE" == command {
    // A like is received
    debugPrint("\(user.userName) liked you.")
  }
}
```


## FAQs
If you have any requirements or feedback, contact colleenyu@tencent.com.
