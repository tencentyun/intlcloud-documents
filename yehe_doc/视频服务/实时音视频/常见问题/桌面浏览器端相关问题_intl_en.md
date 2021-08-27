[](id:que1)
### What browsers support TRTC SDK for desktop browsers?	
TRTC SDK for desktop browsers is well supported by Chrome (desktop), Edge (desktop), and Safari (desktop and mobile), but poorly or not supported by other platforms such as browsers on Android. For more information, please see [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/35143).
You can visit [WebRTC Support Level Test](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) in a browser to test whether the environment fully supports WebRTC.

[](id:que2)
### Can TRTC SDK for desktop browsers communicate with TRTC for PC?
Yes. TRTC supports communication across all platforms.

[](id:que3)
### Native TRTC SDKs have an on-cloud stream mix API, but how can I implement the on-cloud stream mixing feature with TRTC SDK for desktop browsers?
Currently, there isn’t an on-cloud stream mix API for desktop browsers. You can call the [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997) API of CSS to mix streams.

[](id:que4)

### What should I do if the error "RtcError: no valid ice candidate found" occurs when I run TRTC SDK for desktop browsers?

It indicates that the SDK failed to punch holes via Session Traversal Utilities for NAT (STUN). Please check your firewall policy. TRTC SDK for desktop browsers uses the following ports and domain name for data transfer, which should be added to the allowlist of the firewall. After configuration, use the [official demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/official-demo/index.html) to check whether the configuration has taken effect.
 - TCP port: 8687
 - UDP ports: 8000, 8080, 8800, 843, 443, 16285
 - Domain name: qcloud.rtc.qq.com

[](id:que5)
### What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?
It indicates that TRTC SDK for desktop browsers failed to establish a media transport connection. Please check your firewall policy. The SDK uses the following ports and domain name for data transfer, which should be added to the allowlist of the firewall. After configuration, use the [official demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/official-demo/index.html) to check whether the configuration has taken effect.
 - TCP port: 8687
 - UDP ports: 8000, 8080, 8800, 843, 443, 16285
 - Domain name: qcloud.rtc.qq.com


[](id:que6)
### How do I implement the screenshot feature in TRTC SDK for desktop browsers?
Please see the [Stream.getVideoFrame()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#getVideoFrame) API.

[](id:que7)
### What do the errors `NotFoundError`, `NotAllowedError`, `NotReadableError`, `OverConstrainedError`, and `AbortError` found in the log of TRTC SDK for desktop browsers mean?


| Error               | Description | Suggested Solution |
| -------------------- | -------------------- | -------------------- |
| NotFoundError | The media (audio, video, or screen sharing) specified by the request parameter are not found. <br>This error occurs if, for example, the PC has no cameras but the browser is asked to obtain a video stream.   | Remind users to check devices such as cameras and mics before making a call. If a user does not have a camera and wants to make an audio call, use [TRTC.createStream({ audio: true, video: false })](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream) to make the SDK capture audio only. |
| NotAllowedError| The user has rejected the request of the current browser instance to access the camera/mic or share screens.| Remind the user that audio/video calls are not possible without camera/mic access. |
| NotReadableError  | The user has granted access to the requested device, but it is still inaccessible due to a hardware, browser, or webpage error.  | Handle the error according to the error message returned, and send this message to the user: “The camera/mic cannot be accessed. Please make sure that no other applications are requesting access and try again.”|
| OverConstrainedError | The `cameraId/microphoneId` value is invalid. | Make sure that a valid `cameraId/microphoneId` value is passed in.|
| AbortError| The device cannot be accessed due to an unknown reason. | - |


For more information, please see [initialize]((https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#initialize).


[](id:que8)
### Does TRTC SDK for desktop browsers support the dual-channel (big and small images) encoding mode as that enabled by `enableSmallVideoStream`?	
No, TRTC SDK for desktop browsers does not support the dual-channel encoding mode for now.

[](id:que9)
### How do I remove a camera from the camera list after the camera is disconnected in TRTC SDK for desktop browsers?
You can try calling [getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getCameras) to get the new device list. If there is still information of the disconnected camera, it indicates that the browser has not refreshed the list, so TRTC SDK for desktop browsers cannot get the new device list.

[](id:que10)
### How do I record audio-only streams in TRTC SDK for desktop browsers? Why does the recording fail after I enable auto relayed push and auto recording in the console?	
You need to set the `pureAudioPushMode` parameter of [createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient).

[](id:que11)
### Can TRTC SDK for desktop browsers get the current volume?
The [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioLevel) method can be used to get the current volume.

[](id:que12)
### Can I change the style of the screen sharing pop-up window in TRTC SDK for desktop browsers?	
No, because the style of the pop-up window is determined by the browser and cannot be changed at the webpage level.

[](id:que13)
### In TRTC SDK for desktop browsers, does the resolution set for pushed streams apply to all browsers?
Video resolutions may not match on different devices and browsers. In such cases, the browser will adjust the resolution automatically so that it is close to the value set in `setVideoProfile`. For more information, see [setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#setVideoProfile).

[](id:que14)
### How do I check whether TRTC SDK for desktop browsers can get the device (camera/mic) list?
1. Check whether the browser can access the devices:
Open the console with the browser and enter `navigator.mediaDevices.enumerateDevices()` to see if the device list can be obtained.
 - Normally, a promise containing an array of `MediaDeviceInfo` objects will be returned, each object corresponding to an available media device.
 - If the SDK fails to enumerate the devices, a rejected promise will be returned, indicating that the browser fails to detect any devices. You need to check the browser or devices.
2. If the device list can be obtained, enter `navigator.mediaDevices.getUserMedia({ audio: true, video: true })` to see if the `MediaStream` object can be returned. If it is not returned, it indicates that the browser failed to obtain any data. You need to check your browser configuration.

[](id:que15)
### What do I do with echo or noise in TRTC SDK for desktop browsers?
If other users hear echo or noise from a user using TRTC SDK for desktop browsers, it indicates that 3A (AEC, ANS, and AGC) processing is not working.
WebRTC provides a set of 3A algorithms, which you can control by enabling or disabling AEC, ANS, and AGC in `MediaTrackConstrains`. To fix the issues of echo, noise, and low volume, you can enable AEC, ANS, and AGC by setting `echoCancellation`, `noiseSuppression`, and `autoGainControl` to `true` when calling `createStream` of `localstream` in TRTC SDK for desktop browsers.
If any of the following occurs, it indicates that the browser is incompatible with the device used. Please check the device or replace it.
- The echo issue persists after `echoCancellation` is set to `true`.
- Background noise persists after `noiseSuppression` is set to `true`.
- The volume remains low after `autoGainControl` is set to `true`.

For more information, please see [MediaTrackConstraints](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaTrackConstraints).



[](id:que17)

### How do I capture the audio played back by the shared application on Windows?
You can call the [startSystemAudioLoopback](https://intl.cloud.tencent.com/document/product/647/35131) API to enable system audio capturing.

[](id:que18)
### How to implement the feature that allows anchors to invite audience to audio/video interaction in the conference mode on Windows?
You need to use another Tencent Cloud product, [IM](https://intl.cloud.tencent.com/document/product/1047/33996), to enable the feature.

This is how it works: A sends a custom message X (you can determine how the message is displayed) to B, and the calling page is triggered; B receives X and the called page is triggered; B uses [enterRoom](https://intl.cloud.tencent.com/document/product/647/35131) to enter the room and sends a custom message X1 to A; A receives X1 (you can determine whether to display the message) and uses `enterRoom` to enter the room. The messages are sent via IM.

[](id:que19)
### How do audience watch the video of co-anchors in a room?
In the live streaming modes, audience enter the room and get the `userid` of anchors via [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a) in `TRTCCloudDelegate` (users who are co-anchoring enter the room via [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f) and are also anchors for audience). They then call [startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a33a6e3765d6ca52d572224bc6e25dbcb) to display the video of the anchors.
For more information, please see [Live Streaming Mode > Windows](https://intl.cloud.tencent.com/document/product/647/35109).

[](id:que20)
### Can I listen for room exit by remote users on web?
Yes. You can use the [client.on('peer-leave')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html) event to receive notifications when a remote user exits the room.

