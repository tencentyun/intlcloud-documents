This document describes the basic workflow of the Tencent Cloud TRTC SDK for Desktop Browser and how to implement a real-time audio/video call feature.

In the TRTC SDK for Desktop Browser, the following terms are often used:
- Client object, which represents a local client. The [Client](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html) class method provides features such as entering a call room, publishing a local stream, and subscribing to a remote stream.
- Stream object, which represents an audio/video stream object, including local audio/video stream object [LocalStream](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html) and remote audio/video stream object [RemoteStream](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html). The `Stream` class method mainly provides the behaviors of audio/video stream objects, including audio/video playback control.

The API call process of basic audio/video calls is as shown below:
![](https://main.qcloudimg.com/raw/9f246e5a88e5a8176290eb6070a0ecb6.jpg)

## Step 1. Create a Client object

Create a [Client](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html) object through the [TRTC.createClient()](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createClient) method. The parameter settings are as follows:
- `mode`: TRTC call mode, which is set to `rtc` here
- `sdkAppId`: the `sdkAppId` you applied for from Tencent Cloud
- `userId`: user ID
- `userSig`: user signature. For the calculation method, please see [How to Calculate UserSig](https://intl.cloud.tencent.com/document/product/647/35166)

```javascript
const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});
```

## Step 2. Enter an audio/video call room

Call [Client.join()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#join) to enter an audio/video call room.
`roomId` parameter: room ID

```javascript
client
  .join({ roomId })
  .catch(error => {
    console.error('Failed to enter the room' + error);
  })
  .then(() => {
    console.log('Entered room successfully');
  });
```

## Step 3. Publish the local stream and subscribe to a remote stream

1. Use the [TRTC.createStream()](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createStream) method to create a local audio/video stream.
 In the following example, the audio/video stream is captured from the camera and mic. The parameter settings are as follows:
 - `userId`: ID of the user to whom the local stream belongs
 - `audio`: whether to enable audio
 - `video`: whether to enable video

 ```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
 ```

2. Call [LocalStream.initialize()](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize) to initialize the local audio/video stream.
```javascript
localStream
  .initialize()
  .catch(error => {
    console.error('Failed to initialize the local stream ' + error);
  })
  .then(() => {
    console.log('Initialized local stream successfully');
  });
```

3. After the local stream is successfully initialized, call the [Client.publish()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#publish) method to publish it.
```javascript
client
  .publish(localStream)
  .catch(error => {
    console.error('Failed to publish the local stream ' + error);
  })
  .then(() => {
    console.log('Published local stream successfully');
  });
```

4. The remote stream is obtained by listening on the [Client.on('stream-added')](https://trtc-1252463788.file.myqcloud.com/web/docs/module-Event.html#.STREAM_ADDED) event. After receiving this event, use [Client.subscribe()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#subscribe) to subscribe to a remote audio/video stream.

>?
>- Before you use [Client.join()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#join) to enter a room, please use [Client.on('stream-added')](https://trtc-1252463788.file.myqcloud.com/web/docs/module-Event.html#.STREAM_ADDED) to register an event to ensure that you can receive the notification when a remote user enters the room.
>- For more information about remote stream exiting the room or other events, please see [Event](https://trtc-1252463788.file.myqcloud.com/web/docs/module-Event.html).

```javascript
client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('Remote stream added: ' + remoteStream.getId());
  // Subscribe to a remote stream
  client.subscribe(remoteStream);
});
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('Subscribed to remote stream successfully:' + remoteStream.getId());
  // Play back the remote stream
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
```

5. In the callback of local stream initialization success or remote stream subscription success, the [Stream.play()](https://trtc-1252463788.file.myqcloud.com/web/docs/Stream.html#play) method can be called to play back audio/video on a webpage. The `play` method accepts a `div` element ID as a parameter. The SDK will automatically create a corresponding audio/video tag under the `div` element and play back audio/video on it.
 - Play back the local stream when it is successfully initialized
```javascript
localStream
  .initialize()
  .catch(error => {
    console.error('Failed to initialize the local stream ' + error);
  })
  .then(() => {
    console.log('Initialized local stream successfully');
    localStream.play('local_stream');
  });
```
 - Play back the remote stream when it is successfully subscribed to
```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('Subscribed to remote stream successfully:' + remoteStream.getId());
  // Play back the remote stream
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
```

## Step 4. Exit the audio/video call room

Call the [Client.leave()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#leave) method to exit the audio/video call room when the call ends, and the entire audio/video call session will end.

```javascript
client
.leave()
.then(() => {
  // Exited room successfully. `client.join` can be called again to enter the room again for a new call.
})
.catch(error => {
  console.error('Failed to exit the room ' + error);
  // This error is unrecoverable and the page needs to be refreshed.
});
```
