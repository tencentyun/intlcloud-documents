## Supported Platforms

Proposed by Google, the WebRTC technology is well supported by Chrome (desktop), Edge (desktop), Firefox (desktop), and Safari (desktop and mobile), but poorly or not supported by other platforms such as browsers on Android.

- If your application scenario is mainly in the education sector, consider using [TRTC SDK for Electron](https://intl.cloud.tencent.com/document/product/647/35097), which supports two-channel big/small video images, with more flexible screen sharing schemes and better recovery capabilities on poor network connections.

<table>
<tr>
<th>OS</th>
<th width="22%">Browser</th><th>Minimum Browser<br>Version Requirement</th><th width="16%">Receive (Playback)</th><th width="16%">Send (Broadcast)</th><th>Screen Sharing</th><th>SDK Version Requirement</th>
</tr><tr>
<td rowspan="4">macOS</td>
<td>Safari (desktop)</td>
<td>11+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Safari 13+)</td>
<td>-</td>
</tr>
<tr>
<td>Chrome (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Chrome 72+)</td>
<td>-</td>
</tr>
<tr>
<td>Firefox (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Firefox 66+）</td>
<td>4.7.0+</td>
</tr>
<tr>
<td>Edge (desktop)</td>
<td>80+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>4.7.0+</td>
</tr>
<tr>
<td  rowspan="4">Windows</td>
<td>Chrome (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Chrome 72+)</td>
<td>-</td>
</tr>
<tr>
<td>QQ browser (desktop, WebKit core)</td>
<td>10.4+</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>Firefox (desktop)</td>
<td>56+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported (on Firefox 66+）</td>
<td>4.7.0+</td>
</tr>
<tr>
<td>Edge (desktop)</td>
<td>80+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
<td>4.7.0+</td>
</tr>
<tr>
<td>iOS 11.1.2+</td>
<td>Safari (mobile)</td>
<td>11+</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>WeChat embedded browser</td>
<td>-</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>WeChat embedded browser</td>
<td>WeChat 6.5+</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td  rowspan="4">Android</td>
<td>QQ browser (mobile)</td>
<td>-</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr><tr>
<td>UC browser (mobile)</td>
<td>-</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>WeChat embedded browser (TBS core)</td>
<td>-</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
<tr>
<td>WeChat embedded browser (XWEB core)</td>
<td>-</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
<td>-</td>
</tr>
</table>

## API Guide
The tutorials below offer detailed instructions on how to use different APIs.

| Feature                       | Sample Code                                                                                                      |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Basic audio/video call  | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-11-basic-video-call.html)               |
| Interactive live streaming | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-12-basic-live-video.html)                           |
| Switching cameras/mics | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-13-basic-switch-camera-mic.html)      |
| Setting local video attributes  | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-14-basic-set-video-profile.html)      |
| Dynamically enabling/disabling local audio/video | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-15-basic-dynamic-add-video.html) |
| Sharing screen | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html)   |
| Detecting volume | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-17-basic-detect-volume.html) |
| Custom capturing and playback rendering | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-20-advanced-customized-capture-rendering.html) |
| Specifying the maximum number of upstream users in a room | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-04-info-uplink-limits.html) |
| Adding music and audio effects | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-22-advanced-audio-mixer.html)                  |


## TRTC

>!This document applies to 4.x.x versions of TRTC SDK for desktop browsers.

TRTC is the main entry to [TRTC SDK for desktop browsers](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/index.html). You can use TRTC methods to create a client object (`Client`) and local audio/video stream object (`Stream`) for real-time communication, check a browser's compatibility and whether it supports screen sharing, as well as set log levels and upload logs.

| API                                                                                                              | Description                                                                                                                                                          |
| ---------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [VERSION](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.VERSION)                                 | Gets the version number of TRTC SDK for desktop browsers.                                                                                                                                  |
| [checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.checkSystemRequirements) | Checks whether a browser supports TRTC SDK for desktop browsers; if not, ask users to download the latest version of Chrome.                                  |
| [isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.isScreenShareSupported) | Checks whether the browser supports screen sharing. Call this method before creating a screen sharing stream.                                                                  |
| [getDevices](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getDevices)                           | Returns the list of media input/output devices.                                                                                                                                    |
| [getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getCameras)                           | Returns the list of cameras.                                                                                                                                          |
| [getMicrophones](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getMicrophones)                   | Returns the list of mics.                                                                                                                                          |
| [getSpeakers](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getSpeakers)                         | Returns the list of speakers.                                                                                                                                          |
| [createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)                       | Creates a client object for real-time audio/video calls. This method needs to be called only once for each call.                                                                                              |
| [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream) | Creates a local `Stream` object, which uses the [`publish()`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish) method to publish local audio/video stream. |

## TRTC.Logger

TRTC.Logger provides methods for log settings such as [log output level](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.LogLevel) setting and log upload enabling/disabling.

| API                                                                                                       | Description               |
| --------------------------------------------------------------------------------------------------------- | ------------------ |
| [setLogLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.setLogLevel) | Sets the log output level. |
| [enableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.enableUploadLog) | Enables log upload.     |
| [disableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.disableUploadLog) | Disables log upload. |

## Client

The audio/video call client object `Client` is created through [`createClient()`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient) and represents an audio/video call.

| API                                                                                                       | Description                                                                                                                                                                            |
| --------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [setProxyServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#setProxyServer)           | Sets proxy servers. This method is suitable where you deploy proxy servers, e.g., Nginx + Coturn, by yourself.                                                                                                      |
| [setTurnServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#setTurnServer) | Sets TURN servers. This method is used along with [`setProxyServer()`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#setProxyServer) and is suitable where you deploy proxy and TURN servers by yourself. |
| [join](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)                               | Enters a room, which starts an audio/video call. If the room does not exist, the system will create one.                                                                                |
| [leave](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave)                             | Exits the current room, which ends the current audio/video call.                                                                                                                                |
| [publish](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish) | Publishes local audio/video stream. This method can be called only after room entry using the [`join()`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join) method. Only one local stream can be published in one audio/video call.                    |
| [unpublish](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#unpublish)                     | Unpublishes local stream.                                                                                                                                                                |
| [subscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe)                     | Subscribes to a remote stream.                                                                                                                                                                    |
| [unsubscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#unsubscribe)                 | Unsubscribes from a remote stream.                                                                                                                                                                |
| [switchRole](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole)                   | Switches user roles. This method works only in the interactive live streaming mode (`live`).                                                                                                                                  |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#on)                                   | Listens for client object events.                                                                                                                                                            |
| [getRemoteMutedState](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteMutedState) | Gets the list of the audio/video mute status of remote users in the current room.                                                                                                                                    |
| [getLocalAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getLocalAudioStats) | Gets audio statistics of published local streams. This method can be used only after [`publish()`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish) is called.                                   |
| [getLocalVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getLocalVideoStats) | Gets video statistics of published local streams. This method can be used only after [`publish()`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish) is called.                                   |
| [getRemoteAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteAudioStats) | Gets audio statistics of all current remote streams.                                                                                                                                              |
| [getRemoteVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteVideoStats) | Gets video statistics of all current remote streams.                                                                                                                                              |

## LocalStream

LocalStream (local audio/video stream) is created through [`createStream`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream) and is a subclass of [Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html).

| API                                                                                                            | Description                                                                                                                                                                                     |
| -------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)                   | Initializes local audio/video stream objects.                                                                                                                                                                 |
| [setAudioProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setAudioProfile) | Sets audio profiles. This method can be used only before [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize) is called. |
| [setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setVideoProfile) | Sets video profiles. This method can be used only before [`initialize()`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize) is called. |
| [setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setScreenProfile) | Sets screen sharing profiles. This method can be used only before [`initialize()`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize) is called. |
| [setVideoContentHint](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setVideoContentHint) | Sets video content hints, mainly in order to improve the video encoding quality in different scenarios. This method can be used only after [`initialize()`](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize) is called. |
| [switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#switchDevice)               | Switches media input devices.                                                                                                                                                                       |
| [addTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#addTrack)                       | Adds an audio or video track.                                                                                                                                                                     |
| [removeTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#removeTrack)                 | Removes the video track.                                                                                                                                                                           |
| [replaceTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#replaceTrack)               | Replaces audio or video track.                                                                                                                                                                     |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#play)                               | Starts playing audio/video stream.                                                                                                                                                                         |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#stop)                               | Stops playing audio/video stream.                                                                                                                                                                       |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#resume)                           | Resumes playing audio/video stream.                                                                                                                                                                         |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#close)                             | Closes audio/video stream.                                                                                                                                                                           |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#muteAudio)                     | Disables the audio track.                                                                                                                                                                           |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#muteVideo)                     | Disables the video track.                                                                                                                                                                           |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#unmuteAudio)                 | Enables the audio track.                                                                                                                                                                           |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#unmuteVideo)                 | Enables the video track.                                                                                                                                                                           |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getId)                             | Gets the unique stream ID.                                                                                                                                                                |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getUserId)                     | Gets the ID of the user to whom the stream belongs.                                                                                                                                                                  |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setAudioOutput)           | Sets the audio output device.                                                                                                                                                                       |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioLevel)             | Gets the current audio level. This method works only if there is audio data in local or remote stream.                                                                                                                               |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#hasAudio)                       | Specifies whether there is an audio track.                                                                                                                                                                       |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#hasVideo)                       | Specifies whether there is a video track.                                                                                                                                                                       |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioTrack)             | Gets the audio track.                                                                                                                                                                           |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getVideoTrack)             | Gets the video track.                                                                                                                                                                           |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getVideoFrame)             | Gets the current video frame.                                                                                                                                                                         |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#on)                                   | Listens for stream events.                                                                                                                                                                       |



## RemoteStream

Remote audio/video stream, which is obtained by listening for the [Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED) event and is a subclass of `[Stream]()`.

| API                                                                                                   | Description                                                                                               |
| ----------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| [getType](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getType) | Gets the remote stream type. This method is mainly used to determine whether a remote stream is a primary audio/video stream or secondary video stream (which is usually a screen sharing stream). |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#play)                     | Starts playing audio/video stream.                                                                                   |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#stop)                     | Stops playing audio/video stream.                                                                                 |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#resume)                 | Resumes playing audio/video stream.                                                                                   |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#close)                   | Closes audio/video stream.                                                                                     |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#muteAudio)           | Disables the audio track.                                                                                     |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#muteVideo)           | Disables the video track.                                                                                     |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#unmuteAudio)       | Enables the audio track.                                                                                     |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#unmuteVideo)       | Enables the video track.                                                                                     |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getId)                   | Gets the unique stream ID.                                                                          |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getUserId)           | Gets the ID of the user to whom the stream belongs.                                                                            |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#setAudioOutput) | Sets the audio output device.                                                                                 |
| [setAudioVolume](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#setAudioVolume) | Sets the audio level.                                                                                 |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getAudioLevel) | Gets the current audio level. This method works only if there is audio data in local or remote stream.                                         |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#hasAudio)             | Specifies whether there is an audio track.                                                                                 |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#hasVideo)             | Specifies whether there is a video track.                                                                                 |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getAudioTrack)   | Gets the audio track.                                                                                     |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getVideoTrack)   | Gets the video track.                                                                                     |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#getVideoFrame)   | Gets the current video frame.                                                                                   |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html#on)                         | Listens for stream events.                                                                                 |


## RtcError

`RtcError` object.

| API                                                                                 | Description         |
| ----------------------------------------------------------------------------------- | ------------ |
| [getCode](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RtcError.html#getCode) | Gets the error code. |


