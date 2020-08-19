## Supported Platforms

Proposed by Google, the WebRTC technology is well supported by Chrome (desktop) and Safari (desktop and mobile) but poorly or not supported by other platforms (such as browsers on Android).
- For mobile devices, the [Mini Program](https://cloud.tencent.com/document/product/647/17018) solution is recommended, which is supported by both WeChat and Mobile QQ. This solution is implemented through native technologies of corresponding platforms to deliver excellent audio/video performance and specifically adapted to major mobile phone brands.
- If your application scenario is mainly in the education sector, the [Electron](https://intl.cloud.tencent.com/document/product/647/35097) solution is recommended for the teacher end, which is more stable and supports two-channel big/small video images, more flexible screen sharing schemes, and more powerful recovery capabilities on poor network connections.

| OS | Browser | Minimum Browser Version Requirement | Receipt (Playback) | Sending (Mic-on) | Screen Sharing |
|:-------:|:-------:|:-------:|:-------:|:-------:| :-------:|
| macOS  | Safari (desktop) |  11+ | Supported | Supported  | Not supported |
| macOS  | Chrome (desktop) |  56+ | Supported | Supported | Supported (on Chrome 72+) |
| Windows  | Chrome (desktop) |  56+ | Supported | Supported | Supported (on Chrome 72+) |
| Windows  | QQ Browser (desktop) |  10.4 | Supported | Supported | Not supported |
| iOS | Safari (mobile) | 11.1.2 | Supported | Supported | Not supported |
| iOS | WeChat embedded browser | 12.1.4 | Supported | Not supported | Not supported |
| Android | QQ Browser (mobile) | - | Not supported | Not supported | Not supported |
| Android | UC Browser (mobile) | - | Not supported | Not supported | Not supported |
| Android | WeChat embedded browser | - | Not supported | Not supported | Not supported |

## API Guide
For more information on how to use APIs, please see the guide below:

| Function                       | Sample Code Guide   |
|--------------|--------------------|
| Basic audio/video call  | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-01-basic-video-call.html)               |
| ILVB | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-02-live-video.html)                           |
| Switching camera/mic | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-03-advanced-switch-camera-mic.html)      |
| Setting local video attributes  | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-04-advanced-set-video-profile.html)      |
| Dynamically enabling/disabling local audio/video | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-05-advanced-dynamic-add-video.html) |
| Sharing screen | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-06-advanced-screencast.html)   |
| Detecting volume level | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-07-advanced-detect-volume.html) |
| Custom capturing and playback rendering | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-08-advanced-customized-capture-rendering.html) |
| Limiting the maximum number of upstream users in a room | [Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-09-advanced-uplink-limits.html) |


## TRTC

>!This document applies to TRTC SDK for Desktop Browser v4.x.x.

TRTC is the main entry of [TRTC SDK for Desktop Browser](https://trtc-1252463788.file.myqcloud.com/web/docs/index.html). You can use TRTC methods to create a client object (`Client`) and local audio/video stream object (`Stream`) for real-time audio/video communication. In addition, the TRTC methods can check the browser's compatibility and support for screen sharing, set log levels, and upload logs.

| API | Description |
| --- | --- |
| [VERSION](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.VERSION) | TRTC SDK for Desktop Browser version number. |
| [checkSystemRequirements](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.checkSystemRequirements) | Checks whether the browser is compatible with the TRTC SDK for Desktop Browser; if not, we recommend you guide the user to download or use the latest Chrome version. |
| [isScreenShareSupported](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.isScreenShareSupported) | Checks whether the browser supports screen sharing. Before creating a screen sharing stream, please call this method to check whether the current browser supports screen sharing. |
| [getDevices](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.getDevices) | Returns the list of media input/output devices. |
| [getCameras](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.getCameras) | Returns the list of cameras. |
| [getMicrophones](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.getMicrophones) | Returns the list of mics. |
| [getSpeakers](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.getSpeakers) | Returns the list of speakers. |
| [createClient](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createClient) | Creates real-time audio/video call client object, which is called only once in each call. |
| [createStream](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createStream) | Creates local `Stream` object, which publishes the local audio/video stream by using the [publish()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#publish) method. |

## TRTC.Logger

TRTC.Logger provides log setting methods for operations such as setting [log output level](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.Logger.html#.LogLevel) and enabling/disabling log upload.

| API | Description |
| --- | --- |
| [setLogLevel](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.Logger.html#.setLogLevel) | Sets log output level. |
| [enableUploadLog](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.Logger.html#.enableUploadLog) | Enables log upload. |
| [disableUploadLog](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.Logger.html#.disableUploadLog) | Disables log upload. |

## Client

The audio/video call client object `Client` is created through [createClient()](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createClient) and represents an audio/video call.

| API | Description |
| --- | --- |
| [setProxyServer](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#setProxyServer) | Sets proxy server. This method is suitable for scenarios where you deploy the proxy server by yourself, e.g., deployment with Ngnix and coturn. |
| [setTurnServer](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#setTurnServer) | Sets TURN server. This method can be used together with [setProxyServer()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#setProxyServer) and is suitable for you to deploy the proxy server and TURN-based transfer. |
| [join](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#join) | Enters room, i.e., starting audio/video call. If the room does not exist, the system will automatically create a new room. |
| [leave](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#leave) | Exits current room, i.e., ending the current audio/video call. |
| [publish](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#publish) | Publishes local audio/video stream. This method must be called after the [join()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#join) method is called to enter a room. Only one local stream can be published in one audio/video call. |
| [unpublish](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#unpublish) | Unpublishes local stream. |
| [subscribe](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#subscribe) | Subscribes to remote stream. |
| [unsubscribe](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#unsubscribe) | Unsubscribes from remote stream. |
| [switchRole](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#switchRole) | Switches user role. This method takes effect only in ILVB mode (`live`). |
| [on](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#on) | Listens on client object events. |
| [getRemoteMutedState](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#getRemoteMutedState)| Gets the list of audio/video mute status of remote users in the current room. |
| [getLocalAudioStats](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#getLocalAudioStats) | Gets the audio statistics of currently published local streams. This method must be called after [publish()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#publish) is called. |
| [getLocalVideoStats](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#getLocalVideoStats) | Gets the video statistics of currently published local streams. This method must be called after [publish()](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#publish) is called. |
| [getRemoteAudioStats](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#getRemoteAudioStats) | Gets the audio statistics of all current remote streams. |
| [getRemoteVideoStats](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#getRemoteVideoStats) | Gets the video statistics of all current remote streams. |

## LocalStream

LocalStream, i.e., local audio/video stream, is created through [createStream](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createStream) and is a subclass of [Stream](https://trtc-1252463788.file.myqcloud.com/web/docs/Stream.html).

| API | Description |
| --- | --- |
| [initialize](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize) | Initializes local audio/video stream object. |
| [setAudioProfile](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#setAudioProfile) | Sets audio profile. This method must be called before [initialize()](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize) is called. |
| [setVideoProfile](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#setVideoProfile) | Sets video profile. This method must be called before [initialize()](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize) is called. |
| [setScreenProfile](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#setScreenProfile) | Sets screen sharing profile. This method must be called before [initialize()](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize) is called. |
| [setVideoContentHint](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#setVideoContentHint) | Sets video content hint, mainly in order to improve the video encoding quality in different scenarios. This method must be called before [initialize()](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#initialize) is called. |
| [switchDevice](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#switchDevice) | Switches media input device. |
| [addTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#addTrack) | Adds audio or video track. |
| [removeTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#removeTrack) | Removes video track. |
| [replaceTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#replaceTrack) | Changes audio or video track. |
| [play](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#play) | Starts audio/video stream. |
| [stop](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#stop) | Stops audio/video stream. |
| [resume](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#resume) | Resumes audio/video stream. |
| [close](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#close) | Closes audio/video stream. |
| [muteAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#muteAudio) | Disables audio track. |
| [muteVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#muteVideo) | Disables video track. |
| [unmuteAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#unmuteAudio) | Enables audio track. |
| [unmuteVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#unmuteVideo) | Enables video track. |
| [getId](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getId) | Gets unique Stream ID. |
| [getUserId](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getUserId) | Gets the ID of the user to whom the stream belongs. |
| [setAudioOutput](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#setAudioOutput) | Sets audio output device. |
| [getAudioLevel](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getAudioLevel) | Gets current volume level. This method takes effect only if there is audio data in the local or remote stream. |
| [hasAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#hasAudio) | Specifies whether there is an audio track. |
| [hasVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#hasVideo) | Specifies whether there is a video track. |
| [getAudioTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getAudioTrack) | Gets audio track. |
| [getVideoTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getVideoTrack) | Gets video track. |
| [getVideoFrame](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#getVideoFrame) | Gets current video frame. |
| [on](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#on) | Listens on `Stream` events. |



## RemoteStream

Remote audio/video stream, which is obtained by listening on the [Client.on('stream-added')](https://trtc-1252463788.file.myqcloud.com/web/docs/module-Event.html#.STREAM_ADDED) event and is a subclass of `[Stream]()`.

| API | Description |
| --- | --- |
| [getType](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getType) | Gets remote stream type. This method is mainly used to determine whether a remote stream is a primary audio/video stream or secondary video stream (which is usually a screen sharing stream). |
| [play](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#play) | Starts audio/video stream. |
| [stop](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#stop) | Stops audio/video stream. |
| [resume](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#resume) | Resumes audio/video stream. |
| [close](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#close) | Closes audio/video stream. |
| [muteAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#muteAudio) | Disables audio track. |
| [muteVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#muteVideo) | Disables video track. |
| [unmuteAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#unmuteAudio) | Enables audio track. |
| [unmuteVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#unmuteVideo) | Enables video track. |
| [getId](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getId) | Gets unique Stream ID. |
| [getUserId](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getUserId) | Gets the ID of the user to whom the stream belongs. |
| [setAudioOutput](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#setAudioOutput) | Sets audio output device. |
| [setAudioVolume](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#setAudioVolume) | Sets playback volume level. |
| [getAudioLevel](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getAudioLevel) | Gets current volume level. This method takes effect only if there is audio data in the local or remote stream. |
| [hasAudio](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#hasAudio) | Specifies whether there is an audio track. |
| [hasVideo](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#hasVideo) | Specifies whether there is a video track. |
| [getAudioTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getAudioTrack) | Gets audio track. |
| [getVideoTrack](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getVideoTrack) | Gets video track. |
| [getVideoFrame](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#getVideoFrame) | Gets current video frame. |
| [on](https://trtc-1252463788.file.myqcloud.com/web/docs/RemoteStream.html#on) | Listens on `Stream` events. |


## RtcError

`RtcError` error object.

| API | Description |
| --- | --- |
| [getCode](https://trtc-1252463788.file.myqcloud.com/web/docs/RtcError.html#getCode) | Gets error code. |
