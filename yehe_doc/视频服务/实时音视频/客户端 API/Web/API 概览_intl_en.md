## Supported Platforms

The TRTC web SDK is based on WebRTC and can be used on mainstream desktop and mobile browsers. For details about browser support, see the table below.
If your browser (for example, WebView) is not in the list, you can run a [TRTC Web SDK Support Level Test](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) in the browser to test whether it fully supports WebRTC.

<table>
<thead>
<tr>
<th>OS</th>
<th>Browser</th>
<th>Minimum Browser<br>Version Requirements</th>
<th>SDK Version Requirements</th>
<th>Receive (Playback)</th>
<th>Send (Publish)</th>
<th width=19%>Share Screen</th>
</tr>
</thead>
<tr>
<td rowspan="11">Windows</td>
<td>Chrome (desktop)</td>
<td>56+</td>
<td>N/A</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported on Chrome 72+</td>
</tr>
<tr>
<td>QQ Browser (desktop, WebKit core)</td>
<td>10.4+</td>
<td>N/A</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Firefox (desktop)</td>
<td>56+</td>
<td>4.7.0+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported on Firefox 66+</td>
</tr>
<tr>
<td>Edge (desktop)</td>
<td>80+</td>
<td>4.7.0+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Sogou Browser (desktop, WebKit core)</td>
<td>11+</td>
<td>4.7.0+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Sogou Browser (Trident core) </td>
<td>N/A</td>
<td>N/A</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Opera (desktop)</td>
<td>46+</td>
<td>4.7.0+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported on Opera 60+</td>
</tr>
<tr>
<td>360 Secure Browser (Blink core)</td>
<td>13+</td>
<td>4.7.0+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>360 Secure Browser (Trident core)</td>
<td>N/A</td>
<td>N/A</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>WeChat built-in browser (desktop)</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>WeCom built-in browser (desktop)</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td rowspan="7">macOS</td>
<td>Safari (desktop)</td>
<td>11+</td>
<td>N/A</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported on Safari 13+</td>
</tr>
<tr>
<td>Chrome (desktop)</td>
<td>56+</td>
<td>N/A</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported on Chrome 72+</td>
</tr>
<tr>
<td>Firefox (desktop)</td>
<td>56+</td>
<td>4.7.0+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported on Firefox 66+. <a href="#attention3">(Note[3])</a></td>
</tr>
<tr>
<td>Edge (desktop)</td>
<td>80+</td>
<td>4.7.0+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported</td>
</tr>
<tr>
<td>Opera (desktop)</td>
<td>46+</td>
<td>4.7.0+</td>
<td>Supported</td>
<td>Supported</td>
<td>Supported on Opera 60+</td>
</tr>
<tr>
<td>WeChat built-in browser (desktop)</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>WeCom built-in browser (desktop)</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td rowspan="6">Android</td>
<td>WeChat built-in browser (TBS core)</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>WeChat built-in browser (XWEB core)</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>WeCom built-in browser</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>Chrome (mobile)</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>QQ Browser (mobile)</td>
<td>N/A</td>
<td>N/A</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>UC Browser (mobile)</td>
<td>N/A</td>
<td>N/A</td>
<td>Not supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>WeChat built-in browser</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>WeChat built-in browser</td>
<td>WeChat 6.5+</td>
<td>N/A</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>iOS</td>
<td>WeCom built-in browser</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>iOS 11.1.2+</td>
<td>Safari (mobile)</td>
<td>11+</td>
<td>N/A</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>Chrome (mobile)</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Not supported</td>
<td>Not supported</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>Chrome (mobile)</td>
<td>N/A</td>
<td>N/A</td>
<td>Supported</td>
<td>Supported</td>
<td>Not supported</td>
</tr>
</table>

>!
>- Due to H.264 copyright restrictions, H.264 encoding, which is required for stream publishing, is unavailable for Chrome versions earlier than v88 on Huawei devices. If you want to use the TRTC web SDK to publish streams on Chrome or Chrome WebView-based browsers on Huawei devices, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) to enable VP8 encoding/decoding.
>- Firefox for macOS performs poorly in terms of screen sharing, and no solution has been found yet. We recommend you use Chrome or Safari instead.[](id:attention3)
>- If you want to add support for dual-channel encoding on web, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- For service stability and better online support, we recommend you to keep your SDK updated to the latest version. For notes on version updates, see [Update Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html).

## URL Protocol Support
Because of the security policies of browsers, when you use WebRTC, there are requirements on the protocol used for access. For details, see the table below.

| Scenario     | Protocol             | Receive (Playback) | Send (Publish) | Share Screen | Remarks |
|----------|:-----------------|:---------|----------|--------|----------|
| Production     | HTTPS        | Supported         | Supported         | Supported     | **Recommended** |
| Production     | HTTP         | Supported         | Not supported       | Not supported   |      |
| Local development | http://localhost | Supported         | Supported         | Supported     | **Recommended** |
| Local development | http://127.0.0.1 | Supported         | Supported         | Supported     |      |
| Local development | http://[local IP address]  | Supported         | Not supported       | Not supported   |      |
| Local development | file:///         | Supported         | Supported         | Supported     |      |

## API Guide
For details about the initialization process and the use of APIs, see the tutorials below:

| Feature                       | Sample Code   |
|--------------------------|----------------------|
| Audio/Video call  | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-11-basic-video-call.html)               |
| Interactive live streaming           | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-12-basic-live-video.html)    |
| Switching cameras/mics | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html)      |
| Setting local video attributes           | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-14-basic-set-video-profile.html)    |
| Disabling/Enabling local audio/video | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-15-basic-dynamic-add-video.html)    |
| Screen sharing                   | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html)                   |
| Measuring volume       | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-17-basic-detect-volume.html)        |
| Custom capturing and rendering | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-20-advanced-customized-capture-rendering.html) |
| Limit on the number of upstream users in a room | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-04-info-uplink-limits.html) |
| Adding background music and audio effects | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-22-advanced-audio-mixer.html)                  |
| Environment and device check before calls| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-23-advanced-support-detection.html) |
| Network quality check before calls| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html) |
| Device change check| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-25-advanced-device-change.html)|
| Publishing to CDN| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-26-advanced-publish-cdn-stream.html) |
| Enabling dual-stream mode| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-27-advanced-small-stream.html) |
| Enabling beauty filters| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-28-advanced-beauty.html) |
| Enabling watermarking| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-29-advance-water-mark.html) |
| Enabling cross-room communication| [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-30-advanced-cross-room-link.html) |
| Implementing On-Cloud MixTranscoding               | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-31-advanced-mix-transcode.html)  |
| Implementing on-cloud recording               | [Tutorial](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-32-advanced-cloud-record.html)   |

>? 
>- Learn more about the features of the TRTC web SDK [here](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-10-basic-get-started-with-demo.html).
>- For FAQs, see [Web](https://intl.cloud.tencent.com/document/product/647/37340).

## API Details
### TRTC

>! This document applies to 4.x.x versions of the TRTC web SDK.

`TRTC` is the main entry to the [TRTC web SDK](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/index.html). You can use `TRTC` APIs to create a client object (`Client`) and local audio/video stream object (`Stream`) for real-time communication, check a browser's compatibility and whether it supports screen sharing, as well as set the log output level and enable/disable log upload.

| API                          | Description                |
|----------------------------|-----------------------|
| [VERSION](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.VERSION)                                 | Version of the TRTC web SDK                                                                                                                                 |
| [checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.checkSystemRequirements) | Checks whether a browser is compatible with the TRTC web SDK. If not, ask users to download the latest version of Chrome. |
| [isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.isScreenShareSupported) | Checks whether a browser supports screen sharing. Call this API before creating a screen sharing stream.                                                                  |
| [isSmallStreamSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#isSmallStreamSupported)    | Checks whether a browser supports the dual-stream mode. Call this API before you enable the dual-stream mode.     |
| [getDevices](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getDevices)                           | Gets the list of media input/output devices.                                                                                                                                    |
| [getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getCameras)                           | Gets the list of cameras.                                                                                                                                          |
| [getMicrophones](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getMicrophones)                   | Gets the list of mics.                                                                                                                                          |
| [getSpeakers](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getSpeakers)                         | Gets the list of speakers.                                                                                                                                          |
| [createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient)    | Creates a client object, which can enter a room, publish streams, subscribe to streams, and perform other actions.          |
| [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createStream) | Creates a local `Stream` object, which uses the [publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish) API to publish the local audio/video stream. |

### TRTC.Logger

`TRTC.Logger` provides APIs for log settings, including [log output level](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.LogLevel) setting and log upload enabling/disabling.

| API                                             | Description                                                         |
| ---------------------------------- | ------------------ |
| [setLogLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.setLogLevel) | Sets the log output level. |
| [enableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.enableUploadLog) | Enables log upload.     |
| [disableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.disableUploadLog) | Disables log upload. |

### Client

A client object (`Client`) is created through [createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient) and represents an audio/video call.

| API      | Description                         |
|----------------------------|---------------------|
| [setProxyServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setProxyServer)           | Sets proxy servers. You can use this API if you deploy proxy servers, e.g., Nginx + Coturn, by yourself.                                                                                                      |
| [setTurnServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setTurnServer) | Sets TURN servers. This API is used together with [setProxyServer()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setProxyServer). You can use it if you deploy proxy and TURN servers by yourself. |
| [join](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#join)                               | Enters a room. This starts an audio/video call. If the room does not exist, the system will create the room automatically.                                                                                |
| [leave](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#leave)                             | Exits a room. This ends an audio/video call.      |
| [publish](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish) | Publishes the local audio/video stream. You should call this API only after you call [join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#join) to enter a room. You can publish only one local stream per audio/video call.                    |
| [unpublish](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#unpublish)                     | Stops publishing the local stream.     |
| [subscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#subscribe)                     | Subscribes to a remote stream.        |
| [unsubscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#unsubscribe)                 | Unsubscribes from a remote stream.     |
| [switchRole](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#switchRole)               | Switches user roles. This API works only in interactive live streaming scenarios (`live`).          |
| [sendSEIMessage](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#sendSEIMessage) |  Sends an SEI message. |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#on)           | Listens for client object events.         |
| [off](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#off)               | Stops listening for client object events.            |
| [getRemoteMutedState](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteMutedState) | Gets the audio/video status of remote users in a room.           |
| [getTransportStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getTransportStats)       | Gets data transfer statistics.    |
| [getLocalAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getLocalAudioStats) | Gets the audio statistics of the published local stream. This API can be used only after [publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish) is called.         |
| [getLocalVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getLocalVideoStats) | Gets the video statistics of the published local stream. This API can be used only after [publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish) is called.           |
| [getRemoteAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteAudioStats) | Gets the audio statistics of all remote streams.        |
| [getRemoteVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteVideoStats) | Gets the video statistics of all remote streams.       |
| [startPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startPublishCDNStream)             | Publishes the stream of the current client to CDN.              |
| [stopPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopPublishCDNStream)               | Stops publishing the stream of the current client to CDN.  |
| [startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startMixTranscode)       | Starts On-Cloud MixTranscoding. This API works only after stream publishing.           |
| [stopMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopMixTranscode)         | Stops On-Cloud MixTranscoding. This API works only after successful local stream publishing (`publish`) and stream mixing ([startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startMixTranscode)). |
| [enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableAudioVolumeEvaluation) | Enables/Disables the volume callback.            |
| [enableSmallStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableSmallStream)       | Enables the dual-stream mode for publishing.              |
| [disableSmallStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#disableSmallStream)     | Disables the dual-stream mode for publishing.              |
| [setSmallStreamProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setSmallStreamProfile)             | Sets parameters for the low-quality stream.     |
| [setRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopPublishCDNStream)           | Switches between the low-quality stream and high-quality stream of a remote user. This API works only if a remote user enables the dual-stream mode.            |

### LocalStream

A local audio/video stream is created through [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createStream). `LocalStream` is a subclass of [Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html).

| API                          | Description                         |
|--------------------------|--------------------------|
| [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)                   | Initializes a local audio/video stream object.                                                                                                                                                                 |
| [setAudioProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioProfile) | Sets audio parameters. This API works only if it is called before [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize). |
| [setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setVideoProfile) | Sets video parameters. This API works only if it is called before [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize). |
| [setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setScreenProfile) | Sets screen sharing parameters. This API works only if it is called before [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize). |
| [setVideoContentHint](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setVideoContentHint) | Sets video content hint, mainly in order to improve the video encoding quality in different scenarios. This method must be called before [initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize) is called. |
| [switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#switchDevice)               | Switches media input devices.                                                                                                                                                                       |
| [addTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#addTrack)                       | Adds an audio or video track to the local stream.                                                                                                                                                                     |
| [removeTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#removeTrack)                 | Removes the video track of the local stream.                                                                                                                                                                           |
| [replaceTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#replaceTrack)               | Replaces the audio or video track of the local stream.                                                                                                                                                                     |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#play)                               | Starts playing the local audio/video stream.                                                                                                                                                                         |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#stop)                               | Stops playing the local audio/video stream.                                                                                                                                                                       |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#resume)                           | Resumes playing the local audio/video stream.                                                                                                                                                                         |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#close)                   | Closes the local audio/video stream.                                                                                     |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#muteAudio)                     | Disables the audio track of the local stream.                                                                                                                                                                           |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#muteVideo)                     | Disables the video track of the local stream.                                                                                                                                                                           |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#unmuteAudio)                 | Enables the audio track of the local stream.                                                                                                                                                                           |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#unmuteVideo)                 | Enables the video track of the local stream.                                                                                                                                                                           |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getId)                   | Gets the stream ID.                                                                          |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getUserId)                     | Gets the ID of the user to whom the stream belongs.                                                                                                                                                                  |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioOutput)           | Sets the audio output device.                                                                                                                                                                       |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getAudioLevel)             | Gets the current volume. This API works only if there is audio data in the local stream or a remote stream.                                                                                                                               |
| [setAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioCaptureVolume) | Sets the mic capturing volume.|
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#hasAudio)                       | Queries whether there is an audio track.                                                                                                                                                                       |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#hasVideo)                       | Queries whether there is a video track.                                                                                                                                                                       |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getAudioTrack)             | Gets the audio track of the local stream.                                                                                                                                                                           |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getVideoTrack)             | Gets the video track of the local stream.                                                                                                                                                                           |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getVideoFrame)             | Gets the current video frame.                                                                                                                                                                         |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#on) | Listens for stream events. |
| [off](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#off)   | Stops listening for stream events. |



### RemoteStream

A remote audio/video stream is obtained via the [Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_ADDED) callback. `RemoteStream` is a subclass of [Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html).

| API                          | Description           |
|-----------------|-----------|
| [getType](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getType) | Gets the remote stream type. This method is mainly used to determine whether a remote stream is an audio/video primary stream or a video substream (which is usually a screen sharing stream). |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#play)                               | Starts playing an audio/video stream.                                                                                                                                                                         |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#stop)                               | Stops playing an audio/video stream.                                                                                                                                                                       |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#resume)                 | Resumes playing an audio/video stream.                                                                                   |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#close)                   | Closes an audio/video stream.                                                                                     |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#muteAudio)           | Disables the audio track of a stream.                                                                                     |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#muteVideo)           | Disables the video track of a stream.                                                                                     |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#unmuteAudio)       | Enables the audio track of a stream.                                                                                     |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#unmuteVideo)       | Enables the video track of a stream.                                                                                     |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getId)                   | Gets the stream ID.                                                                          |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getUserId)           | Gets the ID of the user to whom a stream belongs.                                                                            |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#setAudioOutput) | Sets the audio output device.                                                                                 |
| [setAudioVolume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#setAudioVolume) | Sets the playback volume.                                                                                 |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getAudioLevel) | Gets the current volume. This API works only if there is audio data in the local stream or a remote stream.                                         |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#hasAudio)             | Queries whether there is an audio track.                                                                                 |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#hasVideo)             | Queries whether there is a video track.                                                                                 |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getAudioTrack)   | Gets the audio track of a stream.                                                                                     |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getVideoTrack)   | Gets the video track of a stream.                                                                                     |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getVideoFrame)   | Gets the current video frame.                                                                                   |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#on) | Listens for stream events. |
| [off](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#off)         | Stops listening for stream events.        |


### RtcError

`RtcError` is the error object.

| API      | Description                         |
|-----------------------|-----------|
| [getCode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RtcError.html#getCode) | Gets the error code. |

### ClientEvent
Client events, which are also the values of `eventName` in the `client.on('eventName')` callback.

| API                          | Description           |
| ---------- | ---------- |
| [stream-added](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_ADDED) | There was a new remote stream. This callback is triggered after a remote user starts publishing.             |
| [stream-removed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_REMOVED) | A remote stream was removed. This callback is triggered after a remote user stops publishing.         |
| [stream-updated](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_UPDATED) | A remote stream was updated. This callback is triggered after a remote user adds, removes, or replaces an audio or video track. |
| [stream-subscribed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_SUBSCRIBED) | A remote stream was subscribed to. This callback is triggered after the local user calls `subscribe()` to successfully subscribe to a remote stream.    |
| [connection-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CONNECTION_STATE_CHANGED) | The connection status between the local client and Tencent Cloud changed.       |
| [peer-join](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.PEER_JOIN) | A remote user entered the room.      |
| [peer-leave](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.PEER_LEAVE) | A remote user left the room.      |
| [mute-audio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.MUTE_AUDIO) | A remote user disabled their audio track. This callback is triggered after a remote user disables their audio track.         |
| [mute-video](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.MUTE_VIDEO) | A remote user disabled their video track. This callback is triggered after a remote user disables their video track.         |
| [unmute-audio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.UNMUTE_AUDIO) | A remote user enabled their audio track. This callback is triggered after a remote user enables their audio track.         |
| [unmute-video](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.UNMUTE_VIDEO) | A remote user enabled their video track. This callback is triggered after a remote user enables their video track.         |
| [client-banned](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CLIENT_BANNED) | A user was removed from the room for one of the following reasons:<ul style="margin:0"><li/>A user with the same username entered the room. **Note**: Avoid repeated room entry with the same username because it will cause an error. <li/>The account admin called a server-side API to remove the user from the room.</ul> |
| [network-quality](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.NETWORK_QUALITY) | Callback of statistics on the quality of upstream and downstream data transfer. This callback is triggered every two seconds after room entry. |
| [audio-volume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.AUDIO_VOLUME) | Callback of user volumes.<br>After you call the [enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableAudioVolumeEvaluation) API to enable this callback, the SDK will return the volume of each user in the room at a regular interval. |
| [sei-message](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.SEI_MESSAGE) | An SEI message was received. |
| [error](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.ERROR) | Error event. This callback is triggered if an unrecoverable error occurs. For details, see [Error Codes](https://intl.cloud.tencent.com/document/product/647/41665). |

### StreamEvent
Stream events.

| API      | Description                         |
| ------------- | ------------- |
| [player-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.PLAYER_STATE_CHANGED)         | The status of the audio/video player changed.               |
| [screen-sharing-stopped](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.SCREEN_SHARING_STOPPED)     | Local screen sharing stopped. This event is valid only for the local stream.  |
| [connection-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.CONNECTION_STATE_CHANGED) | The connection status of the stream changed. Listen for this event in `stream-added` and cancel listening for this event in `stream-removed`. |
| [error](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.ERROR) | Error event. This callback is triggered if an unrecoverable error occurs. For details, see [Error Codes](https://intl.cloud.tencent.com/document/product/647/41665). |


## Contact Us

If you have any questions, please email us at colleenyu@tencent.com.
