This document describes how to enable the screen sharing feature.
>! Screen sharing is only supported on Chrome M72+.

## Creating and Publishing Screen Sharing Stream

<dx-codeblock>
::: Screen sharing stream 
//Create a screen sharing stream
const localStream = TRTC.createStream({ audio: false, screen: true });
//Listen for the screen sharing stopping event
localStream.on('screen-sharing-stopped', event => {
  console.log('screen sharing was stopped');
});

//Initialize the screen sharing stream
localStream.initialize().then(() => {
  console.log('screencast stream init success');
  //Publish the screen sharing stream
  client.publish(localStream).then(() => {
    console.log('screen casting');
  });
});
:::
</dx-codeblock>

## Screen Sharing Attributes

Screen sharing attributes include resolution, frame rate, and bitrate. You can use {@link LocalStream#setScreenProfile setScreenProfile()} to specify a profile. Each profile corresponds to a set of resolution, frame rate, and bitrate. You can also specify custom values for resolution, frame rate, and bitrate. The SDK uses the '1080p' profile for screen sharing by default.

- Specifying a profile:
<dx-codeblock>
::: Profile 
const localStream = TRTC.createStream({ audio: false, screen: true });
localStream.setScreenProfile('1080p');
localStream.initialize().then(() => {
		// screencast stream init success
});
:::
</dx-codeblock>
- Specifying custom values for resolution, frame rate, and bitrate:
<dx-codeblock>
::: Custom resolution 
const localStream = TRTC.createStream({ audio: false, screen: true });
localStream.setScreenProfile({ width: 1920, height: 1080, frameRate: 5, bitrate: 1600 /* kbps */});
localStream.initialize().then(() => {
		// screencast stream init success
});
:::
</dx-codeblock>

Recommended settings for screen sharing attributes:

| Profile | Resolution (W × H) | Frame Rate (fps) | Bitrate (Kbps) |
| :------ | :---------------- | :---------- | :---------- |
| 480p    | 640 × 480         | 5           | 900         |
| 480p_2  | 640 × 480         | 30          | 1000        |
| 720p    | 1280 × 720        | 5           | 1200        |
| 720p_2  | 1280 × 720        | 30          | 3000        |
| 1080p   | 1920 × 1080       | 5           | 1600        |
| 1080p_2 | 1920 × 1080       | 30          | 4000        |



## Publishing Both Camera and Screen Sharing Streams

Each {@link Client Client} can publish at most 1 audio track and 1 video track at a time. To publish both the camera and screen sharing streams, you are advised to create a dedicated client for screen sharing.


<dx-codeblock>
::: client 
//Use a separate user ID to publish the screen sharing stream
const shareId = 'share-userId';
const shareClient = TRTC.createClient({ mode: 'rtc', sdkAppId, userId, shareId, userSig });

//Unsubscribe from all remote streams for `shareClient` (The client only publishes the screen sharing stream.)
shareClient.on('stream-added', event => {
  const remoteStream = event.stream;
  shareClient.unsubscribe(remoteStream);
});
shareClient.join({ roomId }).then(() => {
  console.log('shareClient join success');
  //Create a screen sharing stream
  const localStream = TRTC.createStream({ audio: false, screen: true });
  localStream.initialize().then(() => {
    // screencast stream init success
    shareClient.publish(localStream).then(() => {
      console.log('screen casting');
    });
  });
});

//Unsubscribe from the stream of `shareId` for the main client
client.on('stream-added', event => {
  const remoteStream = event.stream;
  const remoteUserId = remoteStream.getUserId();
  if (remoteUserId === shareId) {
    //Unsubscribe from the screen sharing stream
    client.unsubscribe(remoteStream);
  } else {
    //Subscribe to other remote streams
    client.subscribe(remoteStream);
  }
});
:::
</dx-codeblock>
