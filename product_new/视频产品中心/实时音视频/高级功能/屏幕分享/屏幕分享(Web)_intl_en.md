This document mainly describes how to use screen sharing.
>! Screen sharing only supports using Chrome M72+.

## Creating and Publishing a Screen Sharing Stream

```
//Creating a screen sharing stream
const localStream = TRTC.createStream({ audio: false, screen: true });
//Listening to a screen sharing stop event
localStream.on('screen-sharing-stopped', event => {
  console.log('screen sharing was stopped');
});

//Initializing a screen sharing stream
localStream.initialize().then(() => {
  console.log('screencast stream init success');
  //Publishing a screen sharing stream
  client.publish(localStream).then(() => {
    console.log('screen casting');
  });
});
```

## Screen Sharing Attributes

The screen sharing attributes include resolution, frame rate, and bitrate. An attributes profile can be specified using {@link LocalStream#setScreenProfile setScreenProfile()}. Each profile has a corresponding resolution, frame rate, and bitrate. Custom resolution, frame rate, and bitrate can also be used. Screen sharing uses the '1080p' profile by default.

- Specifying an attributes profile:
```
const localStream = TRTC.createStream({ audio: false, screen: true });
localStream.setScreenProfile('1080p');
localStream.initialize().then(() => {
  // screencast stream init success
});
```

- Using custom resolution, frame rate, and bitrate:
```
const localStream = TRTC.createStream({ audio: false, screen: true });
localStream.setScreenProfile({ width: 1920, height: 1080, frameRate: 5, bitrate: 1600 /* kbps */});
localStream.initialize().then(() => {
  // screencast stream init success
});
```

List of recommended screen sharing attributes:

| Profile | Resolution (W x H) | Frame Rate (fps) | Bitrate (Kbps) |
| :------ | :---------------- | :---------- | :---------- |
| 480p    | 640 x 480         | 5           | 900         |
| 480p_2  | 640 x 480         | 30          | 1000        |
| 720p    | 1280 x 720        | 5           | 1200        |
| 720p_2  | 1280 x 720        | 30          | 3000        |
| 1080p   | 1920 x 1080       | 5           | 1600        |
| 1080p_2 | 1920 x 1080       | 30          | 4000        |



## Simultaneously Pushing Camera Video and Screen Sharing

One {@link Client Client} can only push one channel of audio and one channel of video at one time. If you wish to simultaneously push camera video and screen sharing, we recommend that you create another independent client to be responsible for pushing screen sharing only.

```
//Using an independent user ID to push screen sharing
const shareId = 'share-userId';
const shareClient = TRTC.createClient({ mode: 'videoCall', sdkAppId, userId: shareId, userSig });

//Specifying that this shareClient does not receive any remote streams by default (it is only responsible for sending the screen sharing stream)
shareClient.setDefaultMuteRemoteStreams(true);
shareClient.join().then(() => {
  console.log('shareClient join success');
  //Creating a screen sharing stream
  const localStream = TRTC.createStream({ audio: false, screen: true });
  localStream.initialize().then(() => {
    // screencast stream init success
    shareClient.publish(localStream).then(() => {
      console.log('screen casting');
    });
  });
});

//Specifying that subscribed shareID remote stream is canceled in main client
client.on('stream-added', event => {
  const remoteStream = event.stream;
  const remoteUserId = remoteStream.getUserId();
  if (remoteUserId === shareId) {
    //Canceling subscription to one’s own screen sharing stream
    client.unsubscribe(remoteStream);
  } else {
    //Subscribing to other general remote stream
    client.subscribe(remoteStream);
  }
});
```
