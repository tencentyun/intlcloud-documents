This document describes how to enter a room as audience and start co-anchoring. The process of entering a room and publishing streams as an anchor in live streaming scenarios is the same as that in call scenarios. Please see [Real-Time Audio/Video Call](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-11-basic-video-call.html).

## Example
You can click [Demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-live.html) to try out the audio/video features, or log in to [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Web/base-react-next/src/pages/basic-live) to get the sample code related to this document.

## Step 1. Create a client object 

Create a [client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html) object using [TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient). Set the parameters as follows:

- `mode`: TRTC mode, which should be set to `live`
- `sdkAppId`: the `sdkAppId` you obtain from Tencent Cloud
- `userId`: user ID
- `userSig`: user signature

<dx-codeblock>
::: javascript javascript
const client = TRTC.createClient({
  mode: 'live',
  sdkAppId,
  userId,
  userSig
});
:::
</dx-codeblock>

## Step 2. Enter a room as audience

Call [Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join) to enter a TRTC room. Below are the request parameters:

- `roomId`: room ID
- `role`: role
  - `anchor` (default): users in the role of “anchor” can publish local streams and play remote streams.
  - `audience`. Users in the role of “audience” can play remote streams but cannot publish local streams. To co-anchor and publish local streams, audience must switch the role to `anchor` using [Client.switchRole()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole).

<dx-codeblock>
::: javascript javascript
// Enter a room as audience
client
  .join({ roomId, role: 'audience' })
  .then(() => {
    console.log('Entered room successfully');
  })
  .catch(error => {
    console.error('Failed to enter room' + error);
  });
:::
</dx-codeblock>

## Step 3. Play a live stream
1. After receiving `client.on('stream-added')`, which is used to listen for remote streams, call [Client.subscribe()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe) to subscribe to the remote stream.
>?To ensure that you are notified when a remote user enters the room, please subscribe to the `client.on('stream-added')` callback before you call [Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join) to enter the room.

<dx-codeblock>
::: javascript javascript
client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('New remote stream:' + remoteStream.getId());
  // Subscribe to the remote stream
  client.subscribe(remoteStream);
});
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('Subscribed to remote stream successfully:' + remoteStream.getId());
  // Play the remote stream
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
:::
</dx-codeblock>
2. In the callback that indicates successful subscription to a remote stream, call [Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#play) to play the stream on a webpage. The `play` method allows a parameter that is a div element ID. The SDK will create an audio/video tag in the div element and play the stream on it.
<dx-codeblock>
::: javascript javascript
client.on('stream-subscribed', event => {
    const remoteStream = event.stream;
    console.log('Subscribed to remote stream successfully:' + remoteStream.getId());
    // Play the remote stream
    remoteStream.play('remote_stream-' + remoteStream.getId());
});
:::
</dx-codeblock>

## Step 4. Co-anchor

### Step 4.1. Switch roles

Call [Client.switchRole()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole) to switch the role to `anchor`.
<dx-codeblock>
::: javascript javascript
client
  .switchRole('anchor')
  .then(() => {
    // Role switched to “anchor” successfully
  })
  .catch(error => {
    console.error('Failed to switch role' + error);
  });
:::
</dx-codeblock>

### Step 4.2. Co-anchor

1. Call [TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream) to create a local audio/video stream. In the example below, the audio/video stream is captured by the camera and mic. The parameters include:
 - `userId`: ID of the user to whom the local stream belongs
 - `audio`: whether to enable audio
 - `video`: whether to enable video

 ```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
 ```

2. Call [LocalStream.initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize) to initialize the local audio/video stream.
<dx-codeblock>
::: javascript javascript
localStream
    .initialize()
    .then(() => {
    console.log('Local stream initialized successfully');
    })
    .catch(error => {
    console.error('Failed to initialize local stream' + error);
    });
:::
</dx-codeblock>
3. Play the local stream after it is initialized
<dx-codeblock>
::: javascript javascript
localStream
    .initialize()
    .then(() => {
    console.log('Local stream initialized successfully');
    localStream.play('local_stream');
    })
    .catch(error => {
    console.error('Failed to initialize local stream' + error);
    });
:::
</dx-codeblock>
4. Call [Client.publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish) to publish the local stream and start co-anchoring.
<dx-codeblock>
::: javascript javascript
client
    .publish(localStream)
    .then(() => {
    console.log('Local stream published successfully');
    })
    .catch(error => {
    console.error('Failed to publish local stream' + error);
    });
:::
</dx-codeblock>

## Step 5. Exit the room

Call [Client.leave()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave) to exit the room. The live streaming session ends.
<dx-codeblock>
::: javascript javascript
client
  .leave()
  .then(() => {
    // Exited room successfully
  })
  .catch(error => {
    console.error('Failed to leave room' + error);
  });
:::
</dx-codeblock>

>! The value of `appScene` must be the same on each client. Inconsistent `appScene` may cause unexpected problems.
