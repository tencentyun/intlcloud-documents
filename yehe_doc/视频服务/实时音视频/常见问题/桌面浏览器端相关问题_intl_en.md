### Which browsers support the SDK for desktop browser?	
It is well supported by Chrome (desktop) and Safari (desktop and mobile) but poorly or not supported by other platforms (such as browsers on Android). For more information, please see [Supported Platforms](https://intl.cloud.tencent.com/document/product/647/35143).
You can open the [WebRTC capability test](https://www.qcloudtrtc.com/webrtc-samples/abilitytest/index.html) page in your browser to check whether WebRTC is fully supported.

### Does TRTC work in the same way across desktop browsers, WeChat Mini Program, and PC?
Yes. TRTC supports interconnection across all platforms.

### The native TRTC SDK has an on-cloud stream mix API. How is on-cloud stream mix implemented by the TRTC SDK for desktop browser or WeChat Mini Program?
Currently, there are no client APIs for desktop browser and WeChat Mini Program. You can directly call the [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997) API of LVB to mix streams.

### What should I do if the error "RtcError: no valid ice candidate found" occurs during I run the SDK for desktop browser?

It indicates that the TRTC SDK for desktop browser failed with regard to Session Traversal Utilities for NAT (STUN). Please check your firewall policy. The SDK uses the following ports for data transfer, which should be added to the allowlist of the firewall. After configuring these ports, please use the [official demo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html) to check whether the ports work.
 - TCP port: 8687
 - UDP ports: 8000, 8800, 843, 443
 - Domain name: qcloud.rtc.qq.com

### What should I do if the client error "RtcError: ICE/DTLS Transport connection failed" or "RtcError: DTLS Transport connection timeout" occurs?
It indicates that the TRTC SDK for desktop browser failed to build a media transfer channel. Please check your firewall policy. The SDK uses the following ports for data transfer, which should be added to the allowlist of the firewall. After configuring these ports, please use the [official demo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html) to check whether the ports work.
 - TCP port: 8687
 - UDP ports: 8000, 8800, 843, 443
 - Domain name: qcloud.rtc.qq.com


### How is the screencapturing feature of TRTC for desktop browser implemented?
The `HTMLVideoElement.takeSnapshot` in the `HTMLVideoElement` instance is used for screencapturing.
``` 
/*
 * params:
 *   DeviceObject device
 * return:
 *   null
 */
    var video = document.getElementById(""video"")
    video.takeSnapshot(function(data){
        var img = document.createElement('img');
        img.src = data;
        $(""#some_div_id"").append( img );
    });
```

### What do the errors `NotFoundError`, `NotAllowedError`, `NotReadableError`, `OverConstrainedError`, and `AbortError` found in the log of the SDK for desktop browser mean?


| Error | Description | Suggested Solution |
|---------|---------|---------|
| NotFoundError | No media types (including audio, video, and screen sharing) that meet the request parameters are found. <br>For example, this error will occur if the PC has no camera but the browser is requested to get a video stream. | Remind the user to check the required devices such as camera or mic before making a call. If there are no cameras and it is required to make a voice call, specify to capture the mic only in [TRTC.createStream({ audio: true, video: false })](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.250015174.1562552652.1542703643#.createStream). |
| NotAllowedError| The user has rejected the request to access audio, video, or screen sharing made by the current browser instance.| Inform the user that it is impossible to make video or voice calls without camera/mic access. |
| NotReadableError| The user has granted access to the required device, but it is inaccessible due to an error in a certain hardware device on the operating system, browser, or webpage. | Process in response to the error reported by the browser and inform the user that "The camera/mic is temporarily inaccessible. Please make sure that no other applications are requesting access to the camera/mic and try again". |
| OverConstrainedError| The value of the `cameraId`/`microphoneId` parameter is invalid. | Make sure that the value of the `cameraId`/`microphoneId` parameter is correct and valid. |
| AbortError| The device cannot be used for an unknown reason. | - |


For more information, please see [initialize()](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?#initialize).


### Does the SDK for desktop browser support dual-channel encoding mode with big and small images similar to enableSmallVideoStream?	
No. It is unsupported currently.

### How do I clear the data in the camera list if the camera is removed during the use of the SDK for desktop browser?
You can try calling [getCameras](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.48566118.1562552652.1542703643#.getCameras) to get the new device list. If there is still information of the removed camera, it indicates that the browser has not refreshed the list, and the SDK for desktop browser cannot get the new device list.

### How does the SDK for desktop browser record pure audio push? Why can't I enable auto-relay and auto-recording in the console?	
You need to set the `pureAudioPushMode` parameter of [createClient](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.212323796.1562552652.1542703643#.createClient).

### Can the SDK for desktop browser get the current volume level?
The [getAudioLevel](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?_ga=1.215278807.1562552652.1542703643#getAudioLevel) method can be used to get current volume level.

### Can I change the style of the screen sharing pop-up window of the SDK for desktop browser?	
No, as it is controlled by the browser and thus cannot be modified.

### Does the resolution of push set by the SDK for desktop browser by using width and height apply to all browsers?
Due to the restrictions of the device and browser, the video resolution may not be able to match exactly. In this case, the browser will automatically adjust the resolution to make it close to the resolution corresponding to `Profile`. For more information, please see [setVideoProfile](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?#setVideoProfile).

### How do I check whether the SDK for desktop browser can get the device (camera/microphone) list properly?
1. Check whether the browser can use the devices properly:
Open the console directly on the page and enter `navigator.mediaDevices.enumerateDevices()` to check whether the device list can be obtained.
 - If the device list is obtained, a `Promise` will be returned, where there is an array of `MediaDeviceInfo` objects and each object in the array corresponds to an available media device.
 - If the enumeration fails, the `Promise` will return `rejected`, indicating that the browser has not recognized the device, and you need to check the browser or device.
2. If the device list can be obtained, enter `navigator.mediaDevices.getUserMedia({ audio: true, video: true })` to check whether the `MediaStream` object can be returned properly. If it is not returned, the browser has not obtained the data, and you need to check the browser configuration.

### What should I do if the SDK for desktop browser encounters an echo or noise issue?
If you hear an echo or noise from the SDK for desktop browser on other devices, it indicates that 3A processing has not taken effect.
The WebRTC standard provides a set of 3A algorithms which allows you to control 3A processing by enabling or disabling AEC, ANS, and AGC in `MediaTrackConstrains` of `audio`. If you encounter issues such as echo, noise, and low volume level, you can control echo cancellation, noise suppression, and volume gain by controlling the `echoCancellation`, `noiseSuppression`, and `autoGainControl` attributes respectively during `createStream` in the `localstream` of the SDK for desktop browser.
If any of the following circumstances occurs, it indicates that the browser is not compatible with the hardware device, and we recommend you replace or check the device.
- The echo issue persists when `echoCancellation` is set to `true`.
- The background noise persists when `noiseSuppression` is set to `true`.
- The volume is still low when `autoGainControl` is set to `true`.

For more information, please see [MediaTrackConstraints](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaTrackConstraints).

### What should I do if the screen goes black when the SDK for desktop browser is used on a phone?
Currently, WebRTC is not well supported by iOS and Android. The WeChat Mini Program scheme is recommended.
