This document describes how an anchor publishes audio/video streams. "Publishing" refers to turning on the mic and camera to make the audio heard and video seen by other users in the room.

![](https://qcloudimg.tencent-cloud.cn/raw/3f49218df6a0cc1a106f9a61c23fdb98.png)

You will encounter two types of objects while using the TRTC web SDK:
- Client object, which represents a local client. The [Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html) class provides APIs for room entry, local stream publishing, remote stream subscription, etc.
- Stream object, which represents an audio/video stream object. There are local stream objects ([LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html)) and remote stream objects ([RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html)). The `Stream` class provides APIs for stream-related actions, including audio/video playback control.

[](id:step1)
## Step 1. Enter a room
Create a client object and enter a room. For detailed directions, see [Entering a Room](https://intl.cloud.tencent.com/document/product/647/48424).


[](id:step2)
## Step 2. Create a local stream
Call [TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createStream) to create a local audio/video stream.

| Parameter | Description | Notes | Data Type | Example | Default Value |Remarks|
|---------|---------|---------|---------|---------|---------|---------|
| userId | The user ID. | This parameter is **required** and must be the same as the user ID you pass in when creating the client. | string | “denny” or “123321”| - |**Required**|
| audio | Whether to capture audio. | This parameter is **required**. It specifies whether to capture audio from the mic. | boolean | true |  - | **Required**|
| video | Whether to capture video. | This parameter is **required**. It specifies whether to capture video from the camera. | boolean | true |  - | **Required**|

For more information on the parameters, see [TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createStream). 

```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
```

Before publishing the local stream, call [LocalStream.initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize) to initialize the stream.
During initialization, the SDK will ask for permissions to use your camera and mic. When asked by the browser, allow the permissions.

In the callback for successful initialization, call [LocalStream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#play) to play the audio and video locally.

```javascript
// Using the Promise syntax
localStream
  .initialize()
  .then(() => {
    console.log('Initialized the local stream successfully');
    localStream.play('local_stream');
  })
  .catch(error => {
    console.error('Failed to initialize the local stream' + error);
  });

// We recommend you use the async/await syntax
try {
  await localStream.initialize();
  localStream.play('local_stream');
  console.log('Initialized the local stream successfully');
} catch (error) {
  console.error('Failed to initialize the local stream' + error);
}
```


[](id:step3)
## Step 3. Publish the local stream
After the local stream is initialized, call [Client.publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish) to publish it.
```javascript
// Using the Promise syntax
client
  .publish(localStream)
  .then(() => {
    console.log('Published the local stream successfully');
  })
  .catch(error => {
    console.error('Failed to publish local stream' + error);
  });

// We recommend you use the async/await syntax
try {
  await client.publish(localStream);
  console.log('Published the local stream successfully');
} catch (error) {
  console.error('Failed to publish the local stream' + error);
}
```

## Code for the entire process
```javascript
const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});
const localStream = TRTC.createStream({ userId, audio: true, video: true });

try {
  await client.join({ roomId });
  console.log('Entered the room successfully');
} catch (error) {
  console.error('Failed to enter the room. Please try again later.' + error);
}

try {
  await localStream.initialize();
  localStream.play('local_stream');
  console.log('Initialized the local stream successfully');
} catch (error) {
  console.error('Failed to initialize the local stream' + error);
}

try {
  await client.publish(localStream);
  console.log('Published the local stream successfully');
} catch (error) {
  console.error('Failed to publish the local stream' + error);
}
```
