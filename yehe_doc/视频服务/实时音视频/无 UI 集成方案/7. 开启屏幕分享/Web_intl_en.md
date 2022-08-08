For a list of the browsers that support screen sharing, see [Browsers Supported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html). You can also use the [TRTC.isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.isScreenShareSupported) API to check whether your current browser supports screen sharing.
This document describes how to implement the screen sharing feature in the TRTC web SDK.

> !
>- The TRTC web SDK does not support publishing substreams, and screen sharing streams are published as primary streams. Therefore, if a remote screen sharing stream is from a browser, the [RemoteStream.getType()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getType) API will return `main`. We recommend you set `userId` in such a way that you can tell from the ID it’s a screen sharing stream from a browser.
>- The TRTC SDKs for native applications (iOS, Android, macOS, Windows, etc.) support publishing substreams, and screen sharing streams are published as substreams. Therefore, if a remote screen sharing stream is from a native application, the [RemoteStream.getType()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getType) API will return `auxiliary`.

## Creating and Publishing a Screen Sharing Stream

[](id:step1)
### Step 1. Create a screen sharing stream
A screen sharing stream includes an audio track and a video track, and an audio track includes mic audio and system audio.
```javascript
// We recommend you add the prefix `share` to the `userId` of the object to indicate that it is used for screen sharing.
const userId = 'share_userId';
const roomId = 'roomId';

// Good:
// Capture only the screen
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// Capture audio from the mic and video from the screen
const shareStream = TRTC.createStream({ audio: true, screen: true, userId });
// Capture system audio and the screen
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });

// Bad:
const shareStream = TRTC.createStream({ camera: true, screen: true });
// or
const shareStream = TRTC.createStream({ camera: true, screenAudio: true });

```

>! 
>- You cannot set both `audio` and `screenAudio` to `true`, nor can you set both `camera` and `screenAudio` to `true`. For more information about `screenAudio`, see "Capturing System Audio During Screen Sharing" below.
>- You cannot set both `camera` and `screen` to `true`.

[](id:step2)
### Step 2. Initialize the screen sharing stream
During initialization, the browser will ask the user’s permission to share the screen. If the user denies the permission or if the browser is not granted the permission by the system, the `NotReadableError` or `NotAllowedError` error will be returned. In such cases, you need to ask the user to change the browser or system settings to grant the screen sharing permission and then initialize the screen sharing stream again.
>! For Safari, you need to initialize the screen sharing stream in an onclick callback. For details, see [FAQs](#que).

```javascript
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
        // The user denies the permission or cancels screen sharing.
      }
      return;
    default:
      // An unknown error occurred during the initialization of the screen sharing stream. Ask the user to try again.
      return;
  }
}
```

[](id:step3)
### Step 3. Create a client object for screen sharing
We recommend you add the prefix `share` to the `userId` of the object to indicate that it is used for screen sharing.

```javascript
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

```
[](id:step4)
### Step 4. Publish the screen sharing stream
Use the client object created in step 1 to publish the stream. If it is successful, remote users will receive the stream.
```javascript
try {
  await shareClient.publish(shareStream);
} catch (error) {
  // ShareClient failed to publish local stream
}
```

### Code for the entire process
```javascript
// We recommend you add the prefix `share` to the `userId` of the object to indicate that it is used for screen sharing.
const userId = 'share_userId';
const roomId = 'roomId';
// Capture only the screen
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// Capture audio from the mic and video from the screen
// const shareStream = TRTC.createStream({ audio: true, screen: true, userId });
// Capture system audio and the screen
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
        // The user denies the permission or cancels screen sharing.
      }
      return;
    default:
      // An unknown error occurred during the initialization of the screen sharing stream. Ask the user to try again.
      return;
  }
}
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
try {
  await shareClient.publish(shareStream);
} catch (error) {
  // ShareClient failed to publish local stream
}
```

## Configuring Screen Sharing Parameters
Screen sharing parameters include resolution, frame rate, and bitrate, which you can set by calling the [setScreenProfile()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setScreenProfile) API. Each profile value corresponds to a set of resolution, frame rate, and bitrate. The default value is `1080p`.

```javascript
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// For SetScreenProfile() to work, you must call it before you call initialize().
shareStream.setScreenProfile('1080p');
await shareStream.initialize();
```

You can also specify a custom value for the resolution, frame rate, and bitrate.

```javascript
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });
// For SetScreenProfile() to work, you must call it before you call initialize().
shareStream.setScreenProfile({ width: 1920, height: 1080, frameRate: 5, bitrate: 1600 /* kbps */});
await shareStream.initialize();
```
Recommended screen sharing settings:

| Profile | Resolution (W x H) | Frame Rate (fps) | Bitrate (Kbps) |
|:--------|:----------------|:----------|:------------|
| 480p    | 640 x 480         | 5           | 900         |
| 480p_2  | 640 x 480         | 30          | 1000        |
| 720p    | 1280 x 720        | 5           | 1200        |
| 720p_2  | 1280 x 720        | 30          | 3000        |
| 1080p   | 1920 x 1080       | 5           | 1600        |
| 1080p_2 | 1920 x 1080       | 30          | 4000        |

>! Setting the parameters too high may cause unexpected results. We recommend you use the above settings.

## Stopping Screen Sharing

```javascript
// The screen sharing client stops publishing the stream.
await shareClient.unpublish(shareStream);
// Close the screen sharing stream.
shareStream.close();
// Leave the room.
await shareClient.leave();

// The above three steps are optional. You can determine what code to use according to the actual situation. Normally, you need to add code to determine whether the user has entered the room and whether the stream has been published. For more code samples, see the [demo source code](https://github.com/LiteAVSDK/TRTC_Web/blob/main/base-js/js/share-client.js).
```

A user may also stop screen sharing by clicking a built-in button in the browser, so it’s necessary to listen for the screen sharing stopping event and, if the event occurs, take the necessary action.
<img src="https://qcloudimg.tencent-cloud.cn/raw/bb9d93106c1d22f819e905ea3196d866.png" width="600px">

```javascript
// Listen for the screen sharing stopping event.
shareStream.on('screen-sharing-stopped', event => {
  // Stop publishing the screen sharing stream.
  await shareClient.unpublish(shareStream);
  // Close the screen sharing stream.
  shareStream.close();
  // Leave the room.
  await shareClient.leave();
});
```

## Publishing Both Camera and Screen Sharing Streams
A client can publish only one video track and one audio track. Therefore, to publish both the camera and screen sharing streams, you need to create two clients.
Below is an example:
- **client**: Publish the camera stream and subscribe to all remote streams except that of `shareClient`.
- **shareClient**: Publish the screen sharing stream and subscribe to no remote streams.

>! 
>- You need to disable automatic subscription for `shareClient` so that it does not subscribe to remote streams. For details, see the [API document](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createClient).
>- For `client`, you need to unsubscribe from the stream of `shareClient`.

Sample code:
```javascript
const client = TRTC.createClient({ mode: 'rtc', sdkAppId, userId, userSig });
// Set autoSubscribe to false to disable automatic subscription for shareClient.
const shareClient = TRTC.createClient({ mode: 'rtc', sdkAppId, `share_${userId}`, userSig, autoSubscribe: false,});

// Unsubscribe from the stream of shareClient.
client.on('stream-added', event => {
  const remoteStream = event.stream;
  const remoteUserId = remoteStream.getUserId();
  if (remoteUserId === `share_${userId}`) {
    // Unsubscribe from the screen sharing stream.
    client.unsubscribe(remoteStream);
  } else {
    // Subscribe to other remote streams.
    client.subscribe(remoteStream);
  }
});

await client.join({ roomId });
await shareClient.join({ roomId });

const localStream = TRTC.createStream({ audio: true, video: true, userId }); 
const shareStream = TRTC.createStream({ audio: false, screen: true, userId });

// The code for initialization and publishing is omitted. You can add the code based on your needs.

```

## Capturing System Audio During Screen Sharing

**System audio capturing is supported only on Chrome M74 and later versions. On Chrome for Windows and Chrome OS, you can capture the audio of the entire system, while on Chrome for Linux and macOS, you can only capture the audio of Chrome tabs. Other Chrome versions, OS, and browsers do not support system audio capturing.**

```javascript
// Set `screenAudio` to true when creating the screen sharing stream. Don’t set `audio` to true because you cannot capture mic and system audio at the same time.
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });
await shareStream.initialize();
...
```

In the pop-up window, select **Share audio**, and the stream published will contain system audio.



## FAQs
1. **What should I do if the error `getDisplayMedia must be called from a user gesture handler` occurs on Safari?**
With Safari, you can call the screen capturing API `getDisplayMedia` only within one second of the callback for an onclick event. For details, see [this WebKit Bugzilla page](https://bugs.webkit.org/show_bug.cgi?id=198040).
```javascript
// Good
async function onClick() {
  // We recommend you capture the stream first.
  const screenStream = TRTC.createStream({ screen: true });
  await screenStream.initialize();
  await client.join({ roomId: 123123 });
}

// Bad
async function onClick() {
  await client.join({ roomId: 123123 });
  // If it takes longer than one second for the client to enter the room, capturing will fail.
  const screenStream = TRTC.createStream({ screen: true });
  await screenStream.initialize();
}
```

2. **On Chrome for macOS, I have allowed the browser to record the screen, but screen sharing [failed](https://bugs.chromium.org/p/chromium/issues/detail?id=1306876) with the error "NotAllowedError: Permission denied by system" or "NotReadableError: Could not start video source". What should I do?**
Go to **Settings > Security & Privacy**, click **Privacy > Screen Recording**, unselect Chrome and then select it again, and restart Chrome.

3. [WebRTC Known Issues and Solutions](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-02-info-webrtc-issues.html#h2-9)

4. [Electron uses TRTC Web SDK for screen sharing](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-33-advanced-electron-screen-share.html)

5. **How do I tell whether the user is sharing a screen, a window, or a Chrome tab?**
```javascript
// After the screen is captured successfully
const shareStream = TRTC.createStream({ screenAudio: true, screen: true, userId });
await shareStream.initialize();

// Use `displaySurface` to get the content shared
const { displaySurface } = shareStream.getVideoTrack().getSettings();
// `monitor` indicates the entire screen, `window` indicates an application window, and `browser` indicates a Chrome tab
```
For details, see [displaySurface](https://developer.mozilla.org/en-US/docs/Web/API/MediaTrackSettings/displaySurface).