[](id:base)
## Basics

[](id:b1)
### What is TRTCCalling?
TRTCCalling is an RTC solution based on TRTC and TIM. It supports one-to-one and group audio/video calls and allows quick integration.
![](https://main.qcloudimg.com/raw/db70b140c138ba8c4aff32f679332ac3.png)      

[](id:b2)
### Does TRTCCalling support string-type `roomID`?
`roomID` can be a string, but it must be a numeric string.


[](id:environment)
## Environment

[](id:e1)
### What browsers does the TRTC SDK for web support?
For details about browser support, please see [Browsers Supported](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html).
If your browser is not listed in the above document, you can open [the TRTC compatibility check page](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) with the browser to test whether it fully supports WebRTC.

[](id:e2)
### How do I test my current network quality?
Please see [Network Quality Check Before Calls](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-24-advanced-network-quality.html) for detailed directions.

[](id:e3)
### I can run the IM H5 demo successfully locally, but when it is deployed to the server and accessed via an IP address, I can’t make audio/video calls. What should I do?

-**Background**: After running the IM H5 demo locally, the user can send messages and make audio/video calls using localhost. When the project is deployed to the server and accessed via an IP address, text messages can be sent and received, the server responds to console requests properly, and the console reports no errors, but the user fails to make audio/video calls and cannot obtain video.
-**Cause**: IM uses the TRTCCalling SDK for audio/video calls, but the user uses HTTP for access.
-**Solution**: Make sure the TRTCCalling SDK is accessed via HTTPS or localhost.


[](id:Integrated)
## Integration

[](id:i1)
### Why can’t I receive the `NO_RESP` event in the online demo of TRTCCalling?
-**Cause**: The `NO_RESP` event is triggered only when two conditions are met at the same time: the call invitation times out and the callee is not online.
-**Solution**: You will receive the event when both conditions are met.

[](id:i2)
### What should I do if I can’t hear the audio of remote users when accessing TRTCCalling using WeChat’s built-in browser on iOS?
- Cause: This problem is caused by the browser’s autoplay policy.
- Solution: We have addressed this problem in v1.0.0. Please update TRTCCalling to v1.0.0 or a later version.

[](id:i3)
### What should I do if the error “uncaught (in promise) TypeError: cannot read property 'stop' of null” occurs when I call `hangup()` of TRTCCalling?
-**Cause**: The user calls `hangup()` multiple times in a callback, which causes the API to be triggered again before it is executed.
- **Solution**: You only need to call `hangup()` once. The subsequent operations are performed within TRTCCalling. You only need to pay attention to operations related to your business.

[](id:i3)
### On Chrome 90, `trtccalling.js` prompts “Unsupported TRTCClient. Your browser is not compatible with the application”. What should I do?
-**Cause**: Your IM version is too old. It does not have a compatibility check mechanism.
-**Solution**: Update IM.

[](id:4)
### What should I do if the error “TypeError: Cannot read property 'getVideoTracks' of null” occurs when I make a call?

-**Cause**: The error occurs because the callee has not granted the camera/mic access when answering the call.
-**Solution**: Call device-related APIs (such as `startRemoteView` and `startLocalView`) asynchronously, or update TRTCCalling to v1.0.0.

[](id:i5)
### What should I do if the error “TSignaling._onMessageReceived unknown bussinessID=undefined” occurs in an application (`sdkAppid`) that imports TRTCCalling via script?
-**Details**: If the same application (`sdkAppid`) imports TRTCCalling both via script on two clients, the two clients can communicate with each other. However, if the application imports TRTCCalling via script on one client and npm on the other, or if the other client’s application imports the TRTC SDK for Android/iOS, the two clients cannot communicate with each other.
- **Cause**: `bussinessId=undefined` indicates that the TSignaling version is too old. The signaling feature in old TSignaling versions is flawed.
-**Solution**: Update TSignaling and make sure that **the file name of TSignaling is `tsignaling-js` during import.**


[](id:i6)
### What should I do if the error “Uncaught (in promise) Error: You can call `createCustomMessage` only when the SDK is ready” occurs?

-**Cause**: The SDK is not initialized as required.
-**Solution**: Update TRTCCalling to v1.0.0 and call the API after receiving the `SDK_READY` callback.


[](id:i7)
### What should I do if the error “Uncaught (in promise) RTCError: duplicated play() call observed, please stop() firstly &lt;INVALID_OPERATION 0x1001&gt;” occurs?
-**Cause**: This error occurs if you call the `startRemoteView` API during an audio call.
-**Solution**: Do not call `startRemoteView` during an audio call.

[](id:i8)
### What should I do if the error “Uncaught (in promise) Error: inviteID is invalid or invitation has been processed” occurs?
-**Details**: Client A, which uses TRTCCalling for web, calls client B, which uses a native application. Client B answers the call, and client A hangs up before the local camera is started and local preview is displayed. Client B remains on the call page, and the error `Uncaught (in promise) Error: inviteID is invalid or invitation has been processed` is prompted.
-**Cause**: A user can enter a TRTC room without granting access to audio/video devices, but if the user hangs up, a user in a native application will not be notified.
-**Solution**: TRTCCalling 1.0.0 requests camera/mic access beforehand and does not allow users to enter a room before they grant the access. We recommend you update TRTCCalling to v1.0.0 or a later version.

[](id:i9)
### After a call is made, log is printed at the callee side (which indicates that the call invitation is received), but why is the `handleNewInvitationReceived` callback not received?

-**Cause**: The TRTCCalling version is v0.6.0 or earlier, or the TSignaling version is v0.3.0 or earlier.
-**Solution**: Update TRTCCalling and TSignaling to the latest version.
