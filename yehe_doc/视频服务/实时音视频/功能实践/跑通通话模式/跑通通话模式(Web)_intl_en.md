This document describes the basic workflow of the TRTC SDK for Web and how to implement the real-time audio/video call feature.

You will deal with two types of objects in your use of the TRTC SDK for web.
- Client object, which represents a local client. The [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html) class provides APIs for room entry, local stream publishing, remote stream subscription, etc.
- Stream object, which represents an audio/video stream object. There are local stream objects ([LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html)) and remote stream objects ([RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html)). The `Stream` class provides APIs for stream-related actions, including audio/video playback control.

Below are the APIs used in a basic audio/video call:
![](https://main.qcloudimg.com/raw/9f246e5a88e5a8176290eb6070a0ecb6.jpg)

## Step 1. Create a client object

Create a [client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html) object using [TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient). Set the parameters as follows:
- `mode`: TRTC mode, which should be set to `rtc`
- `sdkAppId`: the `sdkAppId` you obtain from Tencent Cloud
- `userId`: user ID
- `userSig`: user signature. For the calculation method, please see [UserSig](https://intl.cloud.tencent.com/document/product/647/35166)

```javascript
const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});
```

## Step 2. Enter a room

Call [Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join) to enter a room.
`roomId`: room ID

```javascript
client
  .join({ roomId })
  .catch(error => {
    console.error('Failed to enter room' + error);
  })
  .then(() => {
    console.log('Entered room successfully');
  });
```

## Step 3. Publish the local stream and subscribe to a remote stream

1. Call [TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream) to create a local audio/video stream.
 In the example below, the local stream is captured by the camera and mic. The parameters are as follows:
 - `userId`: ID of the user to whom the stream belongs
 - `audio`: whether to enable audio
 - `video`: whether to enable video

 ```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
 ```

2. Call [LocalStream.initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize) to initialize the local audio/video stream.
```javascript
localStream
  .initialize()
  .catch(error => {
    console.error('Failed to initialize local stream ' + error);
  })
  .then(() => {
    console.log('Local stream initialized');
  });
```

3. After the local stream is initialized, call [Client.publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish) to publish it.
```javascript
client
  .publish(localStream)
  .catch(error => {
    console.error('Failed to publish local stream ' + error);
  })
  .then(() => {
    console.log('Local stream published successfully');
  });
```

4. After receiving the [Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED) callback, which is used to listen for remote streams, call [Client.subscribe()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe) to subscribe to the stream.
>?
>- To ensure that you are notified when a remote user enters the room, please register the [Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED) callback before you call [Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join) to enter the room.
>- For other events such as the exit of a remote user, please see the [API documentation](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html).
```javascript
client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('New remote stream: ' + remoteStream.getId());
  // Subscribe to the remote stream
  client.subscribe(remoteStream);
});
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('Subscribed to remote stream successfully:' + remoteStream.getId());
  // Play the remote stream
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
```

5. In the callback that indicates successful initialization of the local stream or subscription to a remote stream, call [Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#play) to play the stream on a webpage. The `play` method allows a parameter that is a div element ID. The SDK will create an audio/video tag in the div element and play the stream on it.
 - Play the local stream after successful initialization
```javascript
localStream
  .initialize()
  .catch(error => {
    console.error('Failed to initialize local stream ' + error);
  })
  .then(() => {
    console.log('Local stream successfully initialized');
    localStream.play('local_stream');
  });
```
 - Play a remote stream after successful subscription
```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('Subscribed to remote stream successfully:' + remoteStream.getId());
  // Play the remote stream
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
```

## Step 4. Exit the room

Call [Client.leave()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave) to exit the room, and the call session ends.

```javascript
client
.leave()
.then(() => {
  // Exited room. You can call `client.join` to start a new call.
})
.catch(error => {
  console.error('Failed to exit room ' + error);
  // The error is unrecoverable. Please refresh the page.
});
```

>! The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.
