This document describes how to set the image quality for a video call or live streaming session. You can set the properties according to your requirements for video quality and smoothness to deliver better user experience.
Video properties include resolution, frame rate, and bitrate.

## Directions

You can call `{@link LocalStream#setVideoProfile setVideoProfile()}` to set video properties.

- Using a predefined profile, which corresponds to a set of recommended resolution, frame rate, and bitrate
```
const localStream = TRTC.createStream({ userId, audio: true, video: true });
// Set the profile to 480p
localStream.setVideoProfile('480p');

localStream.initialize().then(() => {
  console.log('local stream init success');
  localStream.play('local_stream');
});
```

- Specifying a custom resolution, frame rate, and bitrate
```
const localStream = TRTC.createStream({ userId, audio: true, video: true });
// Specify a value for the resolution, frame rate, and bitrate
localStream.setVideoProfile({ width: 640, height: 480, frameRate: 15, bitrate: 900 /* kpbs */});

localStream.initialize().then(() => {
  console.log('local stream init success');
  localStream.play('local_stream');
});
```

> !
>- In v4.8.4 and later versions, you can call `{@link LocalStream#setVideoProfile setVideoProfile()}` to change the video settings in real time during a call. For details, see the description of the API.
>- In versions earlier than v4.8.4, You must call `{@link LocalStream#setVideoProfile setVideoProfile()}` before you call `{@link LocalStream#initialize initialize()}` to initialize the local stream. You cannot change video settings during a call.

## Video Profiles

| Profile | Resolution (W x H) | Frame Rate (fps) | Bitrate (Kbps) |
| :----------- | :---------------- | :---------- | :----------- |
| 120p         | 160 x 120         | 15          | 200          |
| 180p         | 320 x 180         | 15          | 350          |
| 240p         | 320 x 240         | 15          | 400          |
| 360p         | 640 x 360         | 15          | 800          |
| 480p         | 640 x 480         | 15          | 900          |
| 720p         | 1280 x 720        | 15          | 1500         |
| 1080p   | 1920 x 1080       | 15           | 2000        |
| 1440p        | 2560 x 1440       | 30          | 4860         |
| 4K           | 3840 x 2160       | 30          | 9000         |

The target resolution of a profile may be unattainable due to device and browser restrictions, in which case the browser will adjust the resolution to make it as close as possible to the target.
