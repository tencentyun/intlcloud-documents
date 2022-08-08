This document describes how to subscribe to the audio/video streams of another user (remote user) in the room, i.e., how to play back the audio/video of a remote user.
![](https://qcloudimg.tencent-cloud.cn/raw/c8ae41656c97fe546b9c4b0b857b0746.png)

You will encounter two types of objects while using the TRTC web SDK:
- Client object, which represents a local client. The [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html) class provides APIs for room entry, local stream publishing, remote stream subscription, etc.
- Stream object, which represents an audio/video stream object. There are local stream objects ([LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html)) and remote stream objects ([RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html)). The `Stream` class provides APIs for stream-related actions, including audio/video playback control.

## Step 1. Create a client object
Create a client object. For detailed directions, see [Entering a Room](https://cloud.tencent.com/document/product/647/74636#step1).

You can specify the subscription mode when creating a client. TRTC offers two subscription modes:
 - Automatic subscription: Upon receiving the `stream-added` notification, the SDK will start receiving and decoding the remote stream. This is the default mode of the SDK.
 - Manual subscription: A screen sharing client only publishes streams and does not receive streams. Therefore, for screen sharing clients, use the manual subscription mode.

```javascript
const client = TRTC.createClient({
  ...,
  autoSubscribe: false // The default value is `true` (automatic subscription)
});
```

## Step 2. Listen for new remote streams and subscribe
You can use [Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED) to listen for new remote streams. After receiving the notification, you can call [Client.subscribe()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#subscribe) to subscribe to the stream.

```javascript
client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('New remote stream:' + remoteStream.getId());
  // Subscribe to the remote stream
  client.subscribe(remoteStream);
});
```
>!
>- In order to receive notifications about all available streams in a room, make sure you register [Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED) before room entry.
>- For other events such as the exit of a remote user, see the [API documentation](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html).


## Step 3. Listen for successful subscription and play the stream
In the callback that indicates successful subscription to a remote stream, call [Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html#play) to play the stream. Pass in a div element ID or HTMLDivElement object to the API, and the SDK will create an audio/video tag in the element and play the stream.

For more information on the parameters of the `play` API, see [Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html#play). 

```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('Subscribed to the remote stream successfully:' + remoteStream.getId());
  // Play the remote stream
  remoteStream.play('remote-stream-' + remoteStream.getId());
});
```
Due to the [autoplay policy](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-21-advanced-auto-play-policy.html) of browsers, when you call `play`, a `PLAY_NOT_ALLOWED` error may occur. In such cases, the SDK will show a pop-up window to users. After obtaining the users’ permission, the SDK will call an API to resume the playback.

You can also implement your own user interaction logic and, after users’ clicking/tapping event, call [Stream.resume()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html#resume) to resume playback. In such cases, you need to set the `enableAutoPlayDialog` parameter of [TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createClient) to `false`.

```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('Subscribed to the remote stream successfully:' + remoteStream.getId());
  // Listen for the 0x4043 error of `remoteStream`
  remoteStream.on('error', error => {
    const errorCode = error.getCode();
    if (errorCode === 0x4043) {
      // If the `PLAY_NOT_ALLOWED` error occurs, display a window on the UI and, after users’ clicking/tapping event, call `stream.resume` to resume playback.
      // remoteStream.resume()
    }
  });
  // Play the remote stream
  remoteStream.play('remote-stream-' + remoteStream.getId());
});
```

## Step 4. Enter a room
Call `Client.join()` to enter a room. For detailed directions, see [Entering a Room](https://cloud.tencent.com/document/product/647/74636#step2).

## Code for the entire process

```javascript

const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});

client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('New remote stream:' + remoteStream.getId());
  // Subscribe to the remote stream
  client.subscribe(remoteStream);
});

client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('Subscribed to the remote stream successfully:' + remoteStream.getId());
  // Listen for the 0x4043 error of `remoteStream`
  remoteStream.on('error', error => {
    const errorCode = error.getCode();
    if (errorCode === 0x4043) {
      // If the `PLAY_NOT_ALLOWED` error occurs, display a window on the UI and, after users’ clicking/tapping event, call `stream.resume` to resume playback.
      // remoteStream.resume()
    }
  });
  // Play the remote stream
  remoteStream.play('remote-stream-' + remoteStream.getId());
});

try {
  await client.join({ roomId });
  console.log('Entered the room successfully');
} catch (error) {
  console.error('Failed to enter the room. Please try again later.' + error);
}
```