> The following FAQs are applicable for TRTC Web SDK version 3.x.x.

### How can I determine if the current browser supports WebRTC?
Use WebRTCAPI.fn.detectRTC to check if WebRTC is supported. If false is returned, the business end will provide an error message page to guide you to use the supported environment. In special cases, you can also handle it in the following ways:
- Open the [Ability Testing page](https://www.qcloudtrtc.com/webrtc-samples/abilitytest/index.html) to test it.
- [Submit a ticket](https://console.cloud.tencent.com/workorder/category) to seek our help.

### What should I do if howling (feedback) occurs?
A muted attribute for local video/audio is already set up in the Demo (Web), which sets the local video stream to play on mute. If this is not set, the sound of the local video stream will be used as the audio input source again, causing the problem of “howling” or “feedback.”

```html
	<video muted autoplay playsinline></video>

	<audio muted autoplay playsinline></audio>
```

> The problem of “howling” or “feedback” could also occur when using two mobile devices (Android or iOS) for close-range testing. Just mute both the capture and the playback of one of the devices.

### What should I do if it takes a long time to hear the audio?
If you are using an audio-only scenario, then use the audio tag instead of video when loading the audio stream.

### What should I do when Android WeChat/Mobile QQ cannot be used normally?
Use the [testing tool](http://debugx5.qq.com/) to confirm whether TBS is successfully installed/upgraded. If it was not a success, then reinstall TBS.

### Why does it indicate on set remote sdp failed (as shown below)?
![](https://main.qcloudimg.com/raw/45f5395173438ebb5894d45197828ac5.png)
The closeLocalMedia parameter in the webrtcapi instantiation method indicates whether the automatic push is turned off. When the parameter is set as false (the default value), then this problem will occur when actively calling startWebRTC.

### How should I troubleshoot it when the phone’s battery consumption is abnormally high?
Video requires encoding/decoding, which in itself uses up a great deal of power. If the page does not have push/watch but the battery consumption is still abnormally high, you can check whether the video’s srcObject was reset during interrupted streaming callback.

```javascript
    `videoElement.srcObject = null`
```

### What should I do if “SecurityError” occurs?
This exception indicates that audio/video cannot be correctly obtained.
WebRTC must be enabled in the page of HTTPS or localhost, otherwise the audio/video device cannot be obtained.

### What does “NotAllowedError” mean?
This exception indicates that the user rejects the request to obtain the audio/video device.

### What should I do if “OverConstrainedError” occurs?
This exception indicates that the specified requirements cannot be met by the device. This is an object of the `OverconstrainedError` type and has a constraint attribute that contains constraint pairs that cannot be satisfied. If multiple tabs are enabled for push at a time, make sure the resolution to be collected is consistent.

### What does “NotFoundError” mean?
This exception indicates that a media type that matches the request parameters cannot be found.

### Why does “NotReadableError” occur when the user has authorization?
Even if the user has been authorized to use an appropriate device, it cannot be accessed due to a hardware, browser, or web page error on the operating system.

### What makes “AbortError” occur?
Even if both the user and the operating system have been granted the access to the device hardware and no `NotReadableError` type problem caused by hardware occurs, the device still cannot be used due to some problems, which thereby causes the Abort Error to occur.

### What kind of situation causes “TypeError” to occur?
The constraints objects are not set or set to false.

### What should I do when there is no sound?
The browser uses the default sound output device. It is recommended that you adjust the sound output device and disable devices other than the amplifier to determine if it works normally.

### What should I do if I am unable to make a video call in the Electron development environment?
If you are using Electron and are unable to make a video call after submitting it to the Mac App Store, please add `com.apple.securite.network.server` to the entitlements.plist file.

### How do you prevent a black screen caused by dom tree redrawing?
If you are using react/vue/angular, the relationship between video and stream is controlled by JS. If data changes cause page changes, you need to rebind the video with the stream, or else a black screen will occur.

### What is the cause of a black screen in iOS?
- If you are using react/vue/angular, a video created dynamically cannot be automatically played in a browser.
- If you are using viewer mode and not implementing push, iOS does not allow auto playback of videos with sound, and remote video streams cannot be played automatically. You need to bind the remote streams to the video tag and add video.play() in the onRemoteStreamUpdate event handling function.


### Why are there still data packets even when the mic is turned off or muted?
There will still be mute packets after the mic is turned off or muted.

### Why are there still data packets even when the camera is turned off?
There will still be black screen packets after the camera is turned off.

