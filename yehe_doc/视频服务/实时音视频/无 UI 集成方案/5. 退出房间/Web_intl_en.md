This document describes how to exit the current TRTC room and in which cases a user is forced to exit the room.
![](https://qcloudimg.tencent-cloud.cn/raw/ea39f08a98dc41195ae63a6ecae803b8.png)

You will encounter two types of objects while using the TRTC web SDK:
- Client object, which represents a local client. The [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html) class provides APIs for room entry, local stream publishing, remote stream subscription, etc.
- Stream object, which represents an audio/video stream object. There are local stream objects ([LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html)) and remote stream objects ([RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html)). The `Stream` class provides APIs for stream-related actions, including audio/video playback control.

[](id:step1)
## Step 1. Enter a room
Create a client object and enter a room. For detailed directions, see [Entering a Room](https://intl.cloud.tencent.com/document/product/647/48424).

[](id:step2)
## Step 2. Exit the room

Call [Client.leave()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#leave) to exit the room, and the call session ends.

```javascript
await client.leave(); 
```

[](id:step3)
## Step 3. Forced to exit the room
In the following cases, a user will receive the [CLIENT_BANNED](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CLIENT_BANNED) callback, which indicates that they were forced to exit the room.

```javascript
client.on('client-banned', error => {
  console.error('client-banned observed: ' + error.message);
  // client-banned observed: client was banned because of duplicated userId joining the room.
  // client-banned observed: client was banned because of you got banned by account admin
});
```

- **Case 1: A user with the same user ID entered the room.**
If there are two anchors with the same user ID in the room, the user who entered the room first will be removed from the room.
Suppose user A entered a room first, and user B entered the same room with the same user ID. User A would be removed from the room.
Having two users with the same ID in the same room may cause errors and is not allowed.

- **Case 2: A server-side API is called to remove the user or close the room.**
You call [RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) | [RemoveUserByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39630) to remove a user from a TRTC room. The user will receive the [CLIENT_BANNED](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CLIENT_BANNED) callback. If you call [DismissRoom](https://intl.cloud.tencent.com/document/product/647/34269) | [DismissRoomByStrRoomId](https://intl.cloud.tencent.com/document/product/647/39631) to close a TRTC room, all users in the room will receive the [CLIENT_BANNED](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CLIENT_BANNED) callback.
