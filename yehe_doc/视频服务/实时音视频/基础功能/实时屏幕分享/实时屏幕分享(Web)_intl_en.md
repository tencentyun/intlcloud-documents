For a list of the browsers that support screen sharing, see [Browsers Supported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html). You can also use the [TRTC.isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.isScreenShareSupported) API to check whether your current browser supports screen sharing.
This document describes how to implement the screen sharing feature in the TRTC SDK for web.

> !
>- The TRTC SDK for web does not support publishing substreams, and screen sharing streams are published as primary streams. Therefore, if a remote screen sharing stream is from a browser, the [RemoteStream.getType()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getType) API will return `main`. We recommend you set `userId` in such a way that you can tell from the ID that a user is sharing the screen from a browser.
>- The TRTC SDKs for native applications (iOS, Android, macOS, Windows, etc.) support publishing substreams, and screen sharing streams are published as substreams. Therefore, if a remote screen sharing stream is from a native application, the [RemoteStream.getType()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getType) API will return `auxiliary`.

## Creating and Publishing a Screen Sharing Stream
>! Follow the steps below to create a screen sharing stream and publish it.

### Step 1. Create a client object for screen sharing
We recommend you add the prefix `share` to the `userId` of the object to indicate that it is used for screen sharing.

<dx-codeblock>
:::javascript
const shareClient = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId, // Example: ‘share_teacher’
  userSig
});
// The client object enters the room.
try {
  await shareClient.join({ roomId });
  // ShareClient join room success
} catch (error) {
  // ShareClient join room failed
}

:::
</dx-codeblock>

### Step 2. Create a screen sharing stream
A screen sharing stream includes an audio track and a video track, and an audio track includes mic audio and system audio.
<dx-codeblock>
:::javascript
// Good practices:
// Capture only video
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// Capture mic audio and video
const shareStream = TRTC.createStream({ audio: true, screen: true, userId });
// Capture system audio and video
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });

// Bad practices:
const shareStream = TRTC.createStream({ camera: true, screen: true });
// or
const shareStream = TRTC.createStream({ camera: true, screenAudio: true });

:::
</dx-codeblock>

>! 
>- You cannot set both `audio` and `screenAudio` to `true`, nor can you set both `camera` and `screenAudio` to `true`. For more information about `screenAudio`, see "Capturing System Audio During Screen Sharing" below.
>- You cannot set both `camera` and `screen` to `true`.

### Step 3. Initialize the screen sharing stream
During initialization, the browser will ask the user’s permission to share the screen. If the user denies the permission or if the browser is not granted the permission by the system, the `NotReadableError` or `NotAllowedError` error will be returned. In such cases, you need to instruct the user to change the browser settings or grant the screen sharing permission.
<dx-codeblock>
:::javascript
try {
  await shareStream.initialize();
} catch (error) {
  // If the initialization of the screen sharing stream fails, notify the user and stop performing subsequent steps including room entry and stream publishing.
  switch (error.name) {
    case 'NotReadableError':
      // Ask the user to check if the system has allowed the browser to record the screen.
      return;
    case 'NotAllowedError':
      if (error.message.includes('Permission denied by system')) {
        // Ask the user to check if the system has allowed the browser to record the screen.
      } else {
        // The user denied the permission or canceled screen sharing.
      }
      return;
    default:
      // An unknown error occurred during the initialization of the screen sharing stream. Ask the user to try again.
      return;
  }
}
:::
</dx-codeblock>

### Step 4. Publish the screen sharing stream
Use the client object created in step 1 to publish the stream. If it is successful, remote users will receive the stream.
<dx-codeblock>
:::javascript
try {
  await shareClient.publish(shareStream);
} catch (error) {
  // ShareClient failed to publish local stream
}
:::
</dx-codeblock>

### Code
<dx-codeblock>
:::javascript
const shareClient = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId, // Example: ‘share_teacher’
  userSig
});
// The client object enters the room.
try {
  await shareClient.join({ roomId });
  // ShareClient join room success
} catch (error) {
  // ShareClient join room failed
}
// Capture only video
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// Capture mic audio and video
// const shareStream = TRTC.createStream({ audio: true, screen: true, userId });
// Capture system audio and video
// const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });
try {
  await shareStream.initialize();
} catch (error) {
  // If the initialization of the screen sharing stream fails, notify the user and stop performing subsequent steps including room entry and stream publishing.
  switch (error.name) {
    case 'NotReadableError':
      // Ask the user to check if the system has allowed the browser to record the screen.
      return;
    case 'NotAllowedError':
      if (error.message.includes('Permission denied by system')) {
        // Ask the user to check if the system has allowed the browser to record the screen.
      } else {
        // The user denied the permission or canceled screen sharing.
      }
      return;
    default:
      // An unknown error occurred during the initialization of the screen sharing stream. Ask the user to try again.
      return;
  }
}
try {
  await shareClient.publish(shareStream);
} catch (error) {
  // ShareClient failed to publish local stream
}
:::
</dx-codeblock>

## Configuring Screen Sharing Parameters
Screen sharing parameters include resolution, frame rate, and bitrate, which you can set using the [setScreenProfile()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setScreenProfile) API. Each profile value corresponds to a set of resolution, frame rate, and bitrate. The default value is `1080p`.

<dx-codeblock>
:::javascript
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// For SetScreenProfile() to work, you must call it before you call initialize().
shareStream.setScreenProfile('1080p');
await shareStream.initialize();
:::
</dx-codeblock>

You can also specify a custom value for the resolution, frame rate, and bitrate.

<dx-codeblock>
:::javascript
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// For SetScreenProfile() to work, you must call it before you call initialize().
shareStream.setScreenProfile({ width: 1920, height: 1080, frameRate: 5, bitrate: 1600 /* kbps */});
await shareStream.initialize();
:::
</dx-codeblock>
Recommended screen sharing settings:

| Profile | Resolution (W × H) | Frame Rate (fps) | Bitrate (Kbps) |
|:--------|:----------------|:----------|:------------|
| 480p    | 640 × 480         | 5           | 900         |
| 480p_2  | 640 × 480         | 30          | 1000        |
| 720p    | 1280 × 720        | 5           | 1200        |
| 720p_2  | 1280 × 720        | 30          | 3000        |
| 1080p   | 1920 × 1080       | 5           | 1600        |
| 1080p_2 | 1920 × 1080       | 30          | 4000        |

>! Setting the parameters too high may cause unexpected results. We recommend you use the above settings.

## Stopping Screen Sharing

<dx-codeblock>
:::javascript
// The screen sharing client stops publishing the stream.
await shareClient.unpublish(shareStream);
// Close the screen sharing stream.
shareStream.close();
// The screen sharing client leaves the room.
await shareClient.leave();

// The above three steps are optional. You can determine what code to use according to the actual situation. Normally, you need to add code to determine whether the user has entered the room and whether the stream has been published. For more code samples, see the [demo source code](https://github.com/LiteAVSDK/TRTC_Web/blob/main/base-js/js/share-client.js).
:::
</dx-codeblock>

A user may also stop screen sharing by clicking a built-in button in the browser, so it’s necessary to listen for the screen sharing stopping event and, if the event occurs, take the necessary action.


<dx-codeblock>
:::javascript
// Listen for the screen sharing stopping event.
shareStream.on('screen-sharing-stopped', event => {
  // The screen sharing client stops publishing.
  await shareClient.unpublish(shareStream);
  // Close the screen sharing stream.
  shareStream.close();
  // The screen sharing client leaves the room.
  await shareClient.leave();
});
:::
</dx-codeblock>

## Publishing Both Camera and Screen Sharing Streams
A client can publish only one video track and one audio track. Therefore, to publish both the camera and screen sharing streams, you need to create two clients.
Below is an example:
- **client**: Publish the camera stream and subscribe to all remote streams except that of `shareClient`.
- **shareClient**: Publish the screen sharing stream and subscribe to no remote streams.

>! 
>- You need to disable automatic subscription for `shareClient` so that it does not subscribe to remote streams. For details, see the [API document](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createClient).
>- For `client`, you need to unsubscribe from the stream of `shareClient`.

Sample code:
<dx-codeblock>
:::javascript
const client = TRTC.createClient({ mode: 'rtc', sdkAppId, userId, userSig });
// Disable automatic subscription for shareClient: autoSubscribe: false
const shareClient = TRTC.createClient({ mode: 'rtc', sdkAppId, `share_${userId}`, userSig, autoSubscribe: false,});

// Unsubscribe from the stream of shareClient.
client.on('stream-added', event => {
  const remoteStream = event.stream;
  const remoteUserId = remoteStream.getUserId();
  if (remoteUserId === `share_${userId}`) {
    //Unsubscribe from the screen sharing stream.
    client.unsubscribe(remoteStream);
  } else {
    //Subscribe to other remote streams.
    client.subscribe(remoteStream);
  }
});

await client.join({ roomId });
await shareClient.join({ roomId });

const localStream = TRTC.createStream({ audio: true, video: true, userId }); 
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });

// The code for initialization and publishing is omitted. You can add the code based on your needs.

:::
</dx-codeblock>

## Capturing System Audio During Screen Sharing

**System audio capturing is supported only on Chrome M74 and later versions. On Chrome for Windows and Chrome OS, you can capture the audio of the entire system, while on Chrome for Linux and macOS, you can only capture the audio of Chrome tabs. Other Chrome versions, OS, and browsers do not support system audio capturing.**

<dx-codeblock>
:::javascript
// Set screenAudio to true when creating the screen sharing stream. Don’t set audio to true as you cannot capture mic and system audio at the same time.
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });
await shareStream.initialize();
...
:::
</dx-codeblock>

In the pop-up window, select **Share audio**, and the stream published will contain system audio.
