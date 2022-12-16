# Upgrading to TUICallKit

`TUICallKit` is Tencent Cloud’s new audio/video call component that comes with UI elements. As an upgraded version of `TRTCCalling`, `TUICallKit` offers features including group calls and AI noise canceling, supports cross-platform calls, and delivers greater reliability. Before you upgrade to `TUICallKit`, please understand the following:
- Calls between `TRTCCalling` and `TUICallKit` are supported. Just make sure you use the same `SDKAppID`.
- `TUICallKit` relies on the audio/video call capability of Tencent Cloud Instant Messaging (IM). You can activate a 60-day free trial of the capability in the [IM console](https://console.cloud.tencent.com/im): Select the target application to enter the **Basic Configuration** page, find **Tencent Real-Time Communication** in the bottom right, and click **Try now**. If you are officially launching your application, please [purchase the capability](https://buy.cloud.tencent.com/avc).

<img width="568" alt="image" src="https://qcloudimg.tencent-cloud.cn/raw/796e49d9f55174aacb62bb8eb848feaf.png">

## Overview

`TUICallKit` is designed and optimized based on the needs of existing users of `TRTCCalling`. You can upgrade to `TUICallKit` with just a few steps. The process takes approximately 20 minutes.
You can choose either of two upgrade methods:
1. Upgrading to the open-source component [TUICallKit Vue3 UI](https://github.com/tencentyun/TUICallKit/tree/main/Web) (recommended): With just a few lines of code changes, you can equip your application with the capability to make audio/video calls, with support for offline call push.
2. Upgrading to the [TUICallEngine SDK](https://www.npmjs.com/package/tuicall-engine-webrtc): You can migrate directly from `TRTCCalling` to the SDK and retain your existing UI layer.
Below are the detailed directions:

## Upgrading to `TUICallKit Vue3 UI`

`TUICallKit Vue3 UI` is an open-source component that comes with UI elements. It can reduce your development time by as much as 90% and allows you to quickly launch an audio/video call application.
- To try the features of the component, see [TUICallKit basic demo](https://github.com/tencentyun/TUICallKit/blob/main/Web/demos/basic/README.md).
- If you want to quickly integrate the component’s features into your project, see [Integration (TUICallKit)](https://www.tencentcloud.com/document/product/647/50993).
- If you want to modify the UI, see [UI Customization (TUICallKit)](https://www.tencentcloud.com/document/product/647/50997).

## Upgrading to TUICallEngine 1.x (no UI)

This section shows you how to upgrade from `TRTCCalling 1.x` to `TUICallEngine 1.x`.

### 1. Update the SDK dependencies

Install the TUICallEngine SDK and update other dependencies to the latest version.

```bash
yarn add tuicall-engine-webrtc # Install TUICallEngine 
yarn add tim-js-sdk@latest trtc-js-sdk@latest tsignaling@latest # Update the dependencies to the latest version
yarn remove trtc-calling-js # Remove TRTCCalling
# If you haven’t installed Yarn, execute "npm install -g yarn" first.
# If you want to continue using npm to manage the dependencies, replace "yarn add" with "npm install" and replace "yarn remove" with "npm uninstall".
```
### 2. Change the SDK import method and instance creation method

You can no longer build your project after performing the above steps. To address the conflicts, you also need to do the following:
1. Change the import method
```javascript
// The old SDK
import TRTCCalling from 'trtc-calling-js';

// The new SDK
import { TUICallEngine } from "tuicall-engine-webrtc";
```

2. Change the instance creation method. For details about the API, see `createInstance()`. Below is an example:

```javascript
// The old SDK
new TRTCCalling({ SDKAppID });

// The new SDK
TUICallEngine.createInstance({ SDKAppID });
// TUICallEngine.destroyInstance(); // Call this API to terminate the instance
```

### 3. Replace the listener constant

The listener constant has changed from `TRTCCalling.EVENT` to `TUICallEvent`. The latter can be imported from `tuicall-engine-webrtc`.
We recommend you use the editor to replace it in bulk.

```javascript
// The old SDK
trtcCalling.on(TRTCCalling.EVNET.ERROR, this.handleError);
trtcCalling.on(TRTCCalling.EVNET.INVITED, this.handleNewInvitationReceived);
trtcCalling.on(TRTCCalling.EVNET.USER_ACCEPT, this.handleUserAccept);
...(Other events)

// The new SDK
import { TUICallEvent } from "tuicall-engine-webrtc";
tuiCallEngine.on(TUICallEvent.ERROR, this.handleError); // “tuiCallEngine” is the new instance name. You can also continue to use “trtcCalling”.
tuiCallEngine.on(TUICallEvent.INVITED, this.handleNewInvitationReceived);
tuiCallEngine.on(TUICallEvent.USER_ACCEPT, this.handleUserAccept);
...(Other events)

```

### 4. Replace the call type constant

If you never used the call type constant before, skip this.
The call type constant has changed from `TRTCCalling.CALL_TYPE` to `TUICallType`. The latter can be imported from `tuicall-engine-webrtc`.
We recommend you use the editor to replace it in bulk.
```javascript
// The old SDK
this.TRTCCalling.CALL_TYPE.AUDIO_CALL // Audio call
this.TRTCCalling.CALL_TYPE.VIDEO_CALL // Video call

// The new SDK
import { TUICallType } from "tuicall-engine-webrtc";
TUICallType.AUDIO_CALL // Audio call
TUICallType.VIDEO_CALL // Video call
```

### 5. Other important API changes

| Description | Old (TRTCCalling) | New (TUICallEngine) | Remarks |
| --- | --- | --- | --- |
| Changes the call type. | trtcCalling.switchToAudioCall() | tuiCallEngine.[switchCallMediaType()](https://www.tencentcloud.com/document/product/647/51016#switchcallmediatype) | The API name changed. The parameter specifies the call type to change to. |
| Gets the mic list. | trtcCalling.getMicrophones() | [tuiCallEngine.getDeviceList()](https://www.tencentcloud.com/document/product/647/51016#getdevicelist) | The two APIs are merged into one. The parameter specifies the type of devices to return. |
| Gets the camera list. | trtcCalling.getCameras() | [tuiCallEngine.getDeviceList()](https://www.tencentcloud.com/document/product/647/51016#getdevicelist) | The two APIs are merged into one. The parameter specifies the type of devices to return. |
| Turns on/off the mic | trtcCalling.setMicMute() | [tuiCallEngine.closeMicrophone()](https://www.tencentcloud.com/document/product/647/51016#closemicrophone) | The API is split into two APIs.|
| Turns on/off the mic | trtcCalling.setMicMute() | [tuiCallEngine.openMicrophone()](https://www.tencentcloud.com/document/product/647/51016#openmicrophone) | The API is split into two APIs.|
| Sets the username and profile photo. | - | [tuiCallEngine.setSelfInfo()](https://www.tencentcloud.com/document/product/647/51016#setselfinfo) | This API is used to set the username and profile photo. |
| Enables/Disables AI noise canceling | - | [tuiCallEngine.enableAIVoice()](https://www.tencentcloud.com/document/product/647/51016#c9ace016-0cfa-441e-a7c7-7fd1c8c55a51) | This is supported since v4.12.1. For details, see the document about AI noise canceling. |


### 6. Others

- `TUICallKit` relies on the audio/video call capability of IM. If you encounter the error "The package you purchased does not support this ability.", you can go to the IM console, click the target application to enter the **Basic Configuration** page, find **Tencent Real-Time Communication** in the bottom right, and click **Try now** to activate a 60-day free trial of the capability. If you are officially launching your application, please go to the purchase page to purchase the capability.
- After performing the above steps, you will be able to use the TUICallEngine SDK. For other questions about API calls, please refer to the API documentation.
