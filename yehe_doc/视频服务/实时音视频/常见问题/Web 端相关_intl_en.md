## 1. Basics
[](id:b1)
### What browsers does the TRTC SDK for web support?
For details about browser support, please see [Browsers Supported](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html).
If your browser is not listed in the above document, you can open [the TRTC compatibility check page](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) with the browser to test whether it fully supports WebRTC.

[](id:b2)
### How do I test my audio/video devices before making a call?
Please see [Environment and Device Check Before Calls](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html) for directions.

[](id:que3)
### How do I test my current network quality?
Please see [Network Quality Check Before Calls](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-24-advanced-network-quality.html) for detailed directions.

[](id:b3)
### Does the SDK support stream mixing, relayed push, dual-channel mode, or beauty filters?
You can refer to [startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode), [Publishing to CDN](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-26-advanced-publish-cdn-stream.html), [Enabling Dual-Channel Mode](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-27-advanced-small-stream.html), and [Enabling Beauty Filters](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html) to enable the advanced features.

## 2. Publishing and Playback
[](id:p1)
### What do the errors `NotFoundError`, `NotAllowedError`, `NotReadableError`, `OverConstrainedError`, and `AbortError` found in the logs of the TRTC SDK for web mean?
| Error               | Description | Suggested Solution |
| -------------------- | -------------------- | -------------------- |
| NotFoundError | The media (audio, video, or screen sharing) specified by the request parameter are not found. This error occurs if, for example, the PC has no cameras but the browser is asked to obtain a video stream. | Remind users to check devices such as cameras and mics before making a call. If a user does not have a camera and wants to make an audio call, use [TRTC.createStream({ audio: true, video: false})](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream) to make the SDK capture audio only. |
| NotAllowedError| The user has rejected the request of the current browser instance to access the camera/mic or share screens.| Remind the user that audio/video calls are not possible without camera/mic access. |
| NotReadableError  | The user has granted access to the requested device, but it is still inaccessible due to a hardware, browser, or webpage error. | Handle the error according to the error message returned, and send this message to the user: “The camera/mic cannot be accessed. Please make sure that no other applications are requesting access and try again.”|
| OverConstrainedError | The `cameraId`/`microphoneId` value is invalid. | Make sure that a valid `cameraId`/`microphoneId` value is passed in.|
| AbortError| The device cannot be accessed due to an unknown reason. | - |

For more information, please see [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#initialize).

[](id:p2)
### Why am I unable to publish or play streams on some mobile browsers?
For details about browser support, please see [Browsers Supported](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html).
If your browser is not listed in the above document, you can open [the TRTC compatibility check page](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) with the browser to test whether it fully supports WebRTC.

[](id:p3)
### In the TRTC SDK for web, are resolution settings for stream publishing applicable to all browsers?
The resolution set may be unattainable due to device and browser restrictions, in which case the browser will adjust the resolution to make it as close as possible to the target. For details, please see [setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#setVideoProfile).

[](id:p4)
### Can I modify the style of screen sharing in the TRTC SDK for web?
No. The style of screen sharing is controlled by browsers and cannot be modified.

[](id:p5)
### Does the TRTC SDK for web support stream mixing?
Yes, it does. For details, please see [startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode).

[](id:p6)
### In the TRTC SDK for web, how do I remove a camera from the camera list after it is disconnected?
You can call [TRTC.getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getCameras) to see if you can get the new device list. If there is still information of the disconnected camera, it indicates that the browser has not refreshed the list and the SDK cannot get the new device list.

[](id:p7)
### Why am I unable to publish streams from WeChat’s built-in browser on iOS?
To learn whether the built-in browser of WeChat for iOS supports publishing or playback, please see [Browsers Supported](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html).

## 3. Playback
[](id:v1)
### Why is there video but no audio during a call?
- It may be because of the browser’s autoplay policy, which causes the “PLAY_NOT_ALLOWED” error. To solve the problem, display a window on the UI and, in the callback for the window’s clicking event, call `Stream.resume()` to resume audio playback. For details, please see [Suggested Solutions for Autoplay Restrictions](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html).
- This problem may also be caused by an unknown error. Check the `audioLevel` and `audioEnergy` of the sender and recipient in the dashboard.

[](id:v2)
### What should I do if video is not displayed during a call?
Check whether the webpage has obtained any data. If data can be sent and received successfully, check whether the correct `mediaStream` object is assigned to the `srcObject` property of `<video>`. Video will not be displayed if `srcObject` is incorrect.

[](id:v3)
### What should I do if there is echo or noise during a call or the volume of a call is small?
These issues are common if the call participants are close to each other. Please ensure a certain distance between call participants when testing. If a non-web client hears echo or noise from a web client, it indicates that 3A is not working on the web end.
If you use the browser’s built-in API [getUserMedia](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia) for custom capturing, you need to enable 3A manually using the parameters below:
- `echoCancellation`: echo cancellation
- `noiseSuppression`: noise suppression
- `autoGainControl`: automatic gain control. 

If you use the [TRTC.createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createStream) API for capturing, you don’t need to set the 3A parameters manually. The TRTC SDK enables 3A by default.

## 4. Others
[](id:o1)
### What should I do if the error "RtcError: no valid ice candidate found" occurs when I run the TRTC SDK for web?
It indicates that the TRTC SDK for web failed to punch a hole via Session Traversal Utilities for NAT (STUN). Please check your firewall configuration. The ports and domain name listed in the document below must be added to the allowlist of your firewall as the SDK uses them for data transfer. After configuration, use the [official demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-rtc.html) to check whether the configuration has taken effect.

For details, please see [Dealing with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).

[](id:o2)
### What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?
It indicates that TRTC SDK for web failed to establish a media transport connection. Please check your firewall configuration. The ports and domain name listed in the document below must be added to the allowlist of your firewall as the SDK uses them for data transfer. After configuration, use the [official demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-rtc.html) to check whether the configuration has taken effect.

For details, please see [Dealing with Firewall Restrictions](https://intl.cloud.tencent.com/document/product/647/35164).


[](id:o3)
### Does the TRTC SDK for web support getting the current volume?
You can use [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioLevel) to get the current volume. For details, please see [Detecting Volume](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-17-basic-detect-volume.html).

[](id:o4)
### What triggers the `Client.on(‘client-banned’)` event?
Calling the RESTful API [RemoveUser](https://intl.cloud.tencent.com/document/product/647/34268) will trigger the event. Note that repeated login causes a business logic error and should be avoided logically, but it will not trigger the `Client.on(‘client-banned’)` event. If you want to manage forced logout in a room, please use the IM SDK for web.

[](id:o5)
### Can I listen for room exit by remote users in the TRTC SDK for web?
Yes. You can use the [client.on('peer-leave')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html) event to receive notifications when a remote user exits the room.

[](id:o6)
### Is data synced between the TRTC SDKs for web and PC?
Yes. TRTC supports communication across all platforms.

[](id:o7)
### How do I take a screenshot in the TRTC SDK for web?
You can use the [Stream.getVideoFrame()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#getVideoFrame) API to take a screenshot.

[](id:o8)
### How do I record audio-only streams in the TRTC SDK for web? Why does the recording fail after I enable auto relayed push and auto recording in the console?
You need to set the `pureAudioPushMode` parameter of [createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient).

[](id:o9)
### What should I do with `Client.on(‘error’)`?
It indicates that the SDK encountered an unrecoverable error. You can refresh the page or call `Client.leave` to leave the room and then call `Client.join` to try again.

[](id:o10)
### Does the TRTC SDK for web or WeChat Mini Program support custom stream ID?
The TRTC SDK for web has supported custom stream ID since v4.3.8. You can update your SDK to use the feature. The TRTC SDK for Mini Program does not support custom stream ID currently.

[](id:011)
### How do I capture system audio during screen sharing in the TRTC SDK for web?
Please see [Capturing System Audio During Screen Sharing](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html#h2-6) for detailed directions.
Currently, system audio capturing is supported on Chrome M74+ only. On Chrome for Windows and Chrome OS, you can capture the audio of the entire system, while on Chrome for Linux and macOS, you can capture only the audio of Chrome tabs. Other Chrome versions, OS, and browsers do not support system audio capturing.

[](id:012)
### How do I switch the camera/mic in the TRTC SDK for web?
You can first get the system’s cameras and mics and call [switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#switchDevice) to switch the camera/mic. For detailed directions, please see [Switching Cameras/Mics](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-13-basic-switch-camera-mic.html).
