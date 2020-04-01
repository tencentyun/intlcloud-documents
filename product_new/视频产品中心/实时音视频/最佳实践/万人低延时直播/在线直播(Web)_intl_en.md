This document describes the scenario where the user enters a live room as viewer and then starts co-anchoring. The process of entering the room as anchor for live broadcasting is the same as the process of video call. For more information, please see [TRTC Video Call](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-01-basic-video-call.html).

## Step 1. Create a Client object

Create a [Client](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html) object through the [TRTC.createClient()](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createClient) method. The parameter settings are as follows:

- `mode`: interactive live video broadcasting mode, which is set to `live` here
- `sdkAppId`: the `sdkAppId` you applied for from Tencent Cloud
- `userId`: user ID
- `userSig`: user signature

```javascript
const client = TRTC.createClient({
  mode: 'live',
  sdkAppId,
  userId,
  userSig
});
```

## Step 2. Enter a live room as viewer

Call [Client.join()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#join) to enter an audio/video call room.
Parameters:

- `roomId`: room ID
- `role`: user role:
  - `anchor`: anchor. The anchor role has permission to publish the local stream and receive remote streams. The default value is the anchor role.
  - `audience`: viewer. The viewer role only has the permission to receive remote streams but not to publish the local stream. If the viewer wants to co-anchor with the anchor, they need to switch the role to `anchor` via [Client.switchRole()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#switchRole) and then publish the local stream.

```javascript
// Enter the room as a viewer
client
  .join({ roomId, role: 'audience' })
  .catch(error => {
    console.error('Failed to enter the room' + error);
  })
  .then(() => {
    console.log('Entered room successfully');
  });
```

## Step 3. View live broadcasting
1. The remote stream is obtained by listening on the `client.on('stream-added')` event. After receiving this event, use [Client.subscribe()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#subscribe) to subscribe to a remote audio/video stream.
>Please register the `client.on('stream-added')` event before calling [Client.join()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#join) to enter the room, so that you won't miss the notifications for remote user's room entry.
>
```javascript
client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('Remote stream added: ' + remoteStream.getId());
  // Subscribe to a remote stream
  client.subscribe(remoteStream);
});
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('Remote stream successfully subscribed to:' + remoteStream.getId());
  // Play back the remote stream
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
```
2. In the callback of remote stream subscription success, the [Stream.play()](https://trtc-1252463788.file.myqcloud.com/web/docs/Stream.html#play) method can be called to play back audio/video on a webpage. The `play` method accepts a `div` element ID as a parameter. The SDK will automatically create a corresponding audio/video tag under the `div` element and play back audio/video on it.

```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('Remote stream successfully subscribed to:' + remoteStream.getId());
  // Play back the remote stream
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
```

## Step 4. Co-anchor with the anchor

### Step 4.1. Switch roles

Use [Client.switchRole()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#switchRole) to switch to the `anchor` role.

```javascript
client
  .switchRole('anchor')
  .catch(error => {
    console.error('Failed to switch roles ' + error);
  })
  .then(() => {
    // Switched role successfully. Now, it is the anchor role
  });
```

### Step 4.2. Co-anchor

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
3. Play back the local stream when it is successfully initialized
```javascript
localStream
  .initialize()
  .catch(error => {
    console.error('Failed to initialize the local stream ' + error);
  })
  .then(() => {
    console.log('Local stream successfully initialized');
    localStream.play('local_stream');
  });
```
4. After the local stream is successfully initialized, call the [Client.publish()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#publish) method to publish it and start co-anchoring.
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

## Step 5. Exit the live room

Call the [Client.leave()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#leave) method to exit the live room when the live broadcasting ends, and the entire live broadcasting session will end.

```javascript
client.leave().catch(error => {
  console
    .error(error => {
      console.error('Failed to exit the room ' + error);
      // This error is unrecoverable and the page needs to be refreshed.
    })
    .then(() => {
      // Exited room successfully. `client.join` can be called again to enter the room again for a new call.
    });
});
```
