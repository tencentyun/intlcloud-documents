## 1. Basics

### What browsers does the TRTC web SDK support?

For details about browser support, see [Browsers Supported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html). If your browser is not listed in the document, you can open [the TRTC compatibility check page](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) with the browser to test whether it fully supports WebRTC.

### How do I test my current network quality?

See [Network Quality Check Before Calls](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html).

### The SDK worked fine when I tested it locally, but after I deployed it online, why couldn’t I make any audio/video calls. What’s wrong?

To ensure data security and protect users’ privacy, browsers allow access to the mic and camera only in secure environments, for example, when `https`, `localhost`, or `file://` is used for access. Because HTTP is not secure, browsers block access to media devices when HTTP is used.

If you can use the SDK in a local development environment but cannot capture data from the camera or mic after deploying it to the web, check whether your webpage is deployed using HTTP. If so, use HTTPS instead and make sure you have a valid HTTPS certificate.

For more information, see [Domain Name and Protocol Support](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html#h2-2).

### What should I do if the “is not included in the current tim&#39;s package” error occurs?

**Cause**:

The version of your TIM dependency is too old.

If it’s not a version issue, then it may be because you haven’t purchased a TRTC package for your application or the feature used is not supported by the package you purchased.

**Solution**:

Update your TIM dependency to v2.21.2 or later.

Purchase a TRTC package.


## 2. Integration

### What should I do if the error “uncaught (in promise) TypeError: cannot read property 'stop' of null” occurs when I call `tuiCallEngine.handup()`?

**Cause**: `hangup()` is called multiple times in a callback, which causes the API to be triggered again before it is executed.

**Solution**: You only need to call `hangup()` once. The subsequent operations are performed within the component. You only need to pay attention to operations related to your business.

### What should I do if the error “TypeError: Cannot read property 'getVideoTracks' of null” occurs when I make a call?

**Cause**: The error occurs if the callee does not grant the camera/mic access before answering a call.

**Solution**: Call device-related APIs (such as `startRemoteView` and `startLocalView`) asynchronously, or update the component to the latest version.

### What should I do if the error “TSignaling._onMessageReceived unknown bussinessID=undefined” occurs in an application (`SDKAppID`) that imports the component via script?

**Details**: If the same application (`SDKAppID`) imports the component both via script on two clients, the two clients can communicate with each other. However, if the application imports the component via script on one client and using npm on the other, or if the other client’s application imports the TRTC Android/iOS SDK, the two clients cannot communicate with each other, and the above error will occur.

**Cause**: `bussinessId=undefined` indicates that the `TSignaling` version is too old. The signaling feature in old versions of `TSignaling` is flawed.

**Solution**: Update `TSignaling` and make sure **its filename is `tsignaling-js` during import.**

### What should I do if the error “Uncaught ( in promise ) RTCError: duplicated play() call observed, please stop() firstly <INVALID_OPERATION 0x1001>” occurs?

**Cause**: This error occurs if you call the `startRemoteView` API during an audio call.

**Solution**: Do not call `startRemoteView` during an audio call.

### What should I do if the error “TRTCCalling.call - failed to access the user’s device” occurs?

**Cause**: The component is not granted camera/mic permission or the camera/mic does not exist.

**Solution**:

Run the [TRTC support level test](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html).

Check in [Chrome Settings](chrome://settings/content) whether your Chrome has granted camera/mic permission to the website using the component.

### Does the `TUICallEngine` web component support receiving offline messages?

No, it does not support receiving offline messages.

However, it supports pushing offline messages. You can set the message to push using the [offlinePushInfo](https://www.tencentcloud.com/document/product/647) parameter of `call` or `groupCall`.

### What should I do if the error “TRTCClient.getMediaDevicesAuth - failed to get user video steam - NotReadableError: Could not start video source” occurs?

**Cause**: The system did not grant the browser camera permission.

**Solution**: Grant the browser camera permission in system settings.