## Overview

Because it is difficult for users to detect device problems during a call, we recommend checking the browser and testing devices such as cameras and mics before starting a video call.

## Browser Check

Before calling the communication capabilities of the SDK, we recommend you use the `{@link TRTC.checkSystemRequirements checkSystemRequirements()}` API to check whether the SDK supports the user’s browser. If the browser is not supported, please recommend the user to use a supported browser based on his or her device type. 

```javascript
TRTC.checkSystemRequirements().then(checkResult => {
  if (checkResult.result) {
    // Check whether room entry is supported
    if (checkResult.isH264DecodeSupported) {
    	// Check whether stream pull is supported
    }
    if (checkResult.isH264EncodeSupported) {
    	// Check whether stream push is supported
    }
  }
})
```

⚠️ If the user’s current browser is supported by the SDK, but the check result returned by `TRTC.checkSystemRequirements` is `false`, it may be due to one of the following reasons:

1. The link does not meet one of the following:
- `localhost` domain (Firefox supports access to `localhost` and local IPs)
- Domain with HTTPS enabled
- Local file opened over the `file:///` protocol

2. After the Firefox browser is installed, the H.264 codec needs to be loaded dynamically; therefore, the check result will be `false` temporarily. Please wait for a while and try again or use another recommended browser to open the link.


### Known Use Limits for Different Browsers

**Firefox**
- Firefox supports only the frame rate of 30 fps. If you need to set the frame rate, use a different browser supported by the SDK.

**QQ Browser**
- The `NotFoundError` error may be thrown when `localStream.initialize()` is called in a `localhost` environment on certain Windows devices with normal cameras and mics.


## Audio/Video Device Test

To ensure that users can have a good user experience with the TRTC SDK, we recommend you check the user's device and network conditions and provide troubleshooting suggestions before the user enters a TRTC room.

You can integrate the device and network check features by referring to the following methods:

- [`rtc-detect` Library](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html#h2-4)
- [React Component for Device Check](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html#h2-5)
- [TRTC Capability Check Page](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html#h2-6)

## `rtc-detect` Library

You can use [rtc-detect](https://www.npmjs.com/package/rtc-detect) to check whether the current environment is supported by the TRTC SDK and view the details of the current environment.

### Installation

```shell
npm install rtc-detect
```

### Usage

```javascript
import RTCDetect from 'rtc-detect';
// Initialize the detection module
const detect = new RTCDetect();
// Get the detection result of the current environment
const result = await detect.getReportAsync();
// `result` contains the current environment system information, API support, codec support, and device information
console.log('result is: ' + result);
```

### API

#### (async) isTRTCSupported()

This API is used to check whether the current environment supports TRTC.

```javascript
const detect = new RTCDetect();
const data = await detect.isTRTCSupported();

if (data.result) {
  console.log('current browser supports TRTC.')
} else {
  console.log(`current browser does not support TRTC, reason: ${data.reason}.`)
}
```

#### getSystem()

This API is used to get the current system environment parameters.

| Item                   | Type   | Description                     |
| ---------------------- | ------ | ------------------------------- |
| UA                     | string | The browser user-agent.                    |
| OS                     | string | The OS of the current device.              |
| browser                | object | The current browser information in the format of `{ name, version }`. |
| displayResolution      | object | The current resolution in the format of `{ width, height }`.    |
| getHardwareConcurrency | number | The number of CPU cores of the current device.             |

```javascript
const detect = new RTCDetect();
const result = detect.getSystem();
```

#### getAPISupported()

This API is used to get the API support of the current environment.

| Item                              | Type    | Description                                           |
| --------------------------------- | ------- | ----------------------------------------------------- |
| isUserMediaSupported              | boolean | Whether the user media data stream can be obtained                           |
| isWebRTCSupported                 | boolean | Whether WebRTC is supported                                       |
| isWebSocketSupported              | boolean | Whether WebSocket is supported                                    |
| isWebAudioSupported               | boolean | Whether WebAudio is supported                                     |
| isScreenCaptureAPISupported       | boolean | Whether the screen stream can be obtained                                  |
| isCanvasCapturingSupported        | boolean | Whether the data stream can be obtained from the canvas                         |
| isVideoCapturingSupported         | boolean | Whether the data stream can be obtained from the video                          |
| isRTPSenderReplaceTracksSupported | boolean | Whether renegotiation with `peerConnection` can be skipped when `track` is replaced    |
| isApplyConstraintsSupported       | boolean | Whether the camera resolution can be changed without calling `getUserMedia` again|

```javascript
const detect = new RTCDetect();
const result = detect.getAPISupported();
```

#### (async) getDevicesAsync()

This API is used to get the available devices in the current environment.

| Item                    | Type                | Description                                        |
|-------------------------|---------------------|----------------------------------------------------|
| hasWebCamPermissions    | boolean | Whether the user camera data can be obtained                           |
| hasMicrophonePermission | boolean | Whether the user mic data can be obtained                           |
| cameras                 | array<CameraItem>   | List of user cameras, including their resolutions, maximum width, maximum height, and maximum frame rate (for certain browsers only) supported for video streams |
| microphones             | array<DeviceItem>   | List of mics used by users                                         |
| speakers                | array<DeviceItem>   | List of speakers used by users                                        |

**CameraItem**

| Item       | Type    | Description                                                          |
|------------|---------|----------------------------------------------------------------------|
| deviceId   | string  | The device ID, which is usually unique and can be used to identify devices. |
| groupId    | string  | The group ID. If two devices belong to the same physical device, they have the same group ID. |
| kind       | string  | The camera device type: 'videoinput'.                                                 |
| label      | string  | A tag which describes the device.                                                          |
| resolution | object  | The maximum resolution width, height, and frame rate supported by the camera {maxWidth: 1280, maxHeight: 720, maxFrameRate: 30}. |

**DeviceItem**

| Item     | Type     | Description                          |
|----------|----------|--------------------------------------|
| deviceId   | string  | The device ID, which is usually unique and can be used to identify devices. |
| groupId    | string  | The group ID. If two devices belong to the same physical device, they have the same group ID. |
| kind     | string   | The device type, such as 'audioinput' and 'audiooutput'. |
| label      | string  | A tag which describes the device.                                                            |

```javascript
const detect = new RTCDetect();
const result = await detect.getDevicesAsync();
```

#### (async) getCodecAsync()

This API is used to get the codec support of the current environment.

| Item                  | Type    | Description        |
| --------------------- | ------- | ------------------ |
| isH264EncodeSupported | boolean | Whether H.264 encoding is supported |
| isH264DecodeSupported | boolean | Whether H.264 decoding is supported |
| isVp8EncodeSupported  | boolean | Whether VP8 encoding is supported  |
| isVp8DecodeSupported  | boolean | Whether VP8 decoding is supported  |
If encoding is supported, audio/video can be published. If decoding is supported, audio/video can be pulled for playback.

```javascript
const detect = new RTCDetect();
const result = await detect.getCodecAsync();
```

#### (async) getReportAsync()

This API is used to get the detection report of the current environment.

| Item            | Type   | Description                       |
| --------------- | ------ | --------------------------------- |
| system          | object | Same as the returned value of `getSystem()`       |
| APISupported    | object | Same as the returned value of `getAPISupported()` |
| codecsSupported | object | Same as the returned value of `getCodecAsync()`   |
| devices         | object | Same as the returned value of `getDevicesAsync()` |

```javascript
const detect = new RTCDetect();
const result = await detect.getReportAsync();
```

#### (async) isHardWareAccelerationEnabled()

This API is used to check whether hardware acceleration is enabled on the Chrome browser.

> !
> The implementation of this API depends on the native WebRTC API. We recommend you call this API for check after calling `isTRTCSupported`. The check can take up to 30 seconds as tested below:
>   1. If hardware acceleration is enabled, this API will take about 2 seconds on Windows and 10 seconds on macOS.
>   2. If hardware acceleration is disabled, this API will take about 30 seconds on both Windows and macOS.


```javascript
const detect = new RTCDetect();
const data = await detect.isTRTCSupported();

if (data.result) {
  const result = await detect.isHardWareAccelerationEnabled();
  console.log(`is hardware acceleration enabled: ${result}`);
} else {
  console.log(`current browser does not support TRTC, reason: ${data.reason}.`)
}
```


## React Component for Device Check

### Device check UI component features

1. Device connection and check logic processing

2. Network check logic processing

3. Optional network check tab

4. Support for Chinese and English

### Device check UI component links

For more information on how to use the component's npm package, see [rtc-device-detector-react](https://www.npmjs.com/package/rtc-device-detector-react).

For more information on how to debug the component's source code, see [github/rtc-device-detector](https://github.com/FTTC/rtc-device-detector).

For more information on how to import the component, see [WebRTC API Example](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/index.html).

### Device check UI component page

<img src="https://qcloudimg.tencent-cloud.cn/raw/d4868199e58d757c56a6e69fd58f93a9.png" alt="img" style="zoom:52%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/a7f8aab8091da5b8147d68c493271521.png" alt="img" style="zoom:62%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/e87cc19b7f8bf90bc23a9dce9e00d5dc.png" alt="img" style="zoom:87%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/9ff35e633d69acffac15ebe27cb6c9cc.png" alt="img" style="zoom:77%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/d4227a2d69cf209a57f395918831873b.png" alt="img" style="zoom:62%;" />
<img src="https://qcloudimg.tencent-cloud.cn/raw/4ca749ec2d4fc52728c2a478a6067d83.png" alt="img" style="zoom:87%;" />

### Device and network check logic

#### 1) Device connection

 The purpose of device connection is to check whether the user’s device has a camera, mic, and speaker and is connected to the network. If a camera and mic exist, the system will try to get the audio/video streams and will prompt the user to grant permission to access their camera and mic.

+ Check whether the device has a camera, mic, and speaker

  ```javascript
  import TRTC from 'trtc-js-sdk';
  
  const cameraList = await TRTC.getCameras();
  const micList = await TRTC.getMicrophones();
  const speakerList = await TRTC.getSpeakers();
  const hasCameraDevice = cameraList.length > 0;
  const hasMicrophoneDevice = micList.length > 0;
  const hasSpeakerDevice = speakerList.length > 0;
  ```

+ Get the camera and mic access permissions

  ```javascript
  navigator.mediaDevices
    .getUserMedia({ video: hasCameraDevice, audio: hasMicrophoneDevice })
    .then((stream) => {
    	// The audio/video streams are successfully obtained
      // ...
    	// Release the camera and mic
     	stream.getTracks().forEach(track => track.stop());
    })
    .catch((error) => {
      // Failed to get the audio/video streams
    });
  ```

+ Check whether the device is connected to the network

  ```javascript
  export function isOnline() {
    const url = 'https://web.sdk.qcloud.com/trtc/webrtc/assets/trtc-logo.png';
    return new Promise((resolve) => {
      try {
        const xhr = new XMLHttpRequest();
        xhr.onload = function () {
          resolve(true);
        };
        xhr.onerror = function () {
          resolve(false);
        };
        xhr.open('GET', url, true);
        xhr.send();
      } catch (err) {
        // console.log(err);
      }
    });
  }
  const isOnline = await isOnline();
  ```



#### 2) Camera check

​	Camera check is to render the video stream captured by the selected camera to help the user determine whether the camera can be used normally.

+ Get the camera list. The first device in the list is used by default

  ```javascript
  import TRTC from 'trtc-js-sdk';
  
  let cameraList = await TRTC.getCameras();
  let cameraId = cameraList[0].deviceId;
  ```

+ Initialize the video stream and play it back in the `dom` element whose ID is `camera-video`

  ```javascript
  const localStream = TRTC.createStream({
    video: true,
    audio: false,
    cameraId,
  });
  await localStream.initialize();
  localStream.play('camera-video');
  ```

+ Update the stream after the user switches the camera

  ```javascript
  localStream.switchDevice('video', cameraId);
  ```

+ Listen on device plugging/unplugging

  ```javascript
  navigator.mediaDevices.addEventListener('devicechange', async () => {
    cameraList = await TRTC.getCameras();
      cameraId = cameraList[0].deviceId; 
    localStream.switchDevice('video', cameraId);
  })
  ```

+ Release the camera after the check is completed

  ```javascript
  localStream.close();
  ```



#### 3) Mic check

Mic check is to render the volume of the audio stream captured by the selected mic to help the user determine whether the mic can be used normally.

+ Get the mic list. The first device in the list is used by default

  ```javascript
  import TRTC from 'trtc-js-sdk';
  
  let microphoneList = await TRTC.getMicrophones();
  let microphoneId = microphoneList[0].deviceId;
  ```

+ Initialize the audio stream and play it back in the `dom` element whose ID is `audio-container`

  ```javascript
  const localStream = TRTC.createStream({
    video: false,
    audio: true,
    microphoneId,
  });
  await localStream.initialize();
  localStream.play('audio-container');
  timer = setInterval(() => {
    const volume = localStream.getAudioLevel();
  }, 100);
  ```

+ Update the stream after the user switches the mic

  ```javascript
  // Get the new `microphoneId` selected by the user
  localStream.switchDevice('audio', microphoneId);
  ```

+ Listen on device plugging/unplugging

  ```javascript
  navigator.mediaDevices.addEventListener('devicechange', async () => {
    microphoneList = await TRTC.getMicrophones();
      microphoneId = microphoneList[0].deviceId;
    localStream.switchDevice('audio', microphoneId);
  })
  ```

+ Release the mic after the check is completed and stop listening on the volume

  ```javascript
  localStream.close();
  clearInterval(timer);
  ```



#### 4) Speaker check

Speaker check provides an audio player for the user to play back the audio and check whether the selected speaker can be used normally.

+ Provide an MP3 player and prompt the user to increase the device playback volume and play back an MP3 file to check whether the speaker is normal

  ```html
  <audio id="audio-player" src="xxxxx" controls></audio>
  ```

+ Stop playback after the check is completed

  ```javascript
  const audioPlayer = document.getElementById('audio-player');
  if (!audioPlayer.paused) {
      audioPlayer.pause();
  }
  audioPlayer.currentTime = 0;
  ```



#### 5) Network check

+ Call [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient) to create two clients: `uplinkClient` and `downlinkClient`.

+ Make the two clients enter the same room.

+ Use `uplinkClient` to push a stream. Listen on the [NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY) event to check the upstream network quality.

+ Use `downlinkClient` to pull a stream. Listen on the [NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY) event to check the downstream network quality.

+ The entire process takes about 15 seconds. When finished, the average network quality is used to evaluate the upstream and downstream network quality.

> !  The process of checking network quality incurs a small [basic service fee](https://cloud.tencent.com/document/product/647/17157#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1). If the push resolution is not specified, the stream will be pushed at a resolution of 640x480 by default.

```javascript
let uplinkClient = null; // Check the upstream network quality
let downlinkClient = null; // Check the downstream network quality
let localStream = null; // Stream for test
let testResult = {
  // Record the upstream network quality data
  uplinkNetworkQualities: [],
  // Record the downstream network quality data
  downlinkNetworkQualities: [],
  average: {
    uplinkNetworkQuality: 0,
    downlinkNetworkQuality: 0
  }
}

// 1. Check the upstream network quality
async function testUplinkNetworkQuality() {
  uplinkClient = TRTC.createClient({
    sdkAppId: 0, // Enter `sdkAppId`
    userId: 'user_uplink_test',
    userSig: '', // `userSig` of `uplink_test`
    mode: 'rtc'
  });

  localStream = TRTC.createStream({ audio: true, video: true });
  // Set the video profile based on the actual business scenario 
  localStream.setVideoProfile('480p'); 
  await localStream.initialize();

  uplinkClient.on('network-quality', event => {
    const { uplinkNetworkQuality } = event;
    testResult.uplinkNetworkQualities.push(uplinkNetworkQuality);
  });

  // Enter the room where the check will be performed. The room ID must be random to avoid conflicts
  await uplinkClient.join({ roomId: 8080 }); 
  await uplinkClient.publish(localStream);
}

// 2. Check the downstream network quality
async function testDownlinkNetworkQuality() {
  downlinkClient = TRTC.createClient({
    sdkAppId: 0, // Enter `sdkAppId`
    userId: 'user_downlink_test',
    userSig: '', // userSig
    mode: 'rtc'
  });

  downlinkClient.on('stream-added', async event => {
    await downlinkClient.subscribe(event.stream, { audio: true, video: true });
		// Start listening on the network quality event after successful subscription
    downlinkClient.on('network-quality', event => {
      const { downlinkNetworkQuality } = event;
      testResult.downlinkNetworkQualities.push(downlinkNetworkQuality);
    });
  })
  // Enter the room where the check will be performed. The room ID must be random to avoid conflicts 
  await downlinkClient.join({ roomId: 8080 });
}

// 3. Start the check
testUplinkNetworkQuality();
testDownlinkNetworkQuality();

// 4. Stop the check after 15 seconds and calculate the average network quality
setTimeout(() => {
  // Calculate the average upstream network quality
  if (testResult.uplinkNetworkQualities.length > 0) {
    testResult.average.uplinkNetworkQuality = Math.ceil(
      testResult.uplinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.uplinkNetworkQualities.length
    );
  }

  if (testResult.downlinkNetworkQualities.length > 0) {
    // Calculate the average downstream network quality
    testResult.average.downlinkNetworkQuality = Math.ceil(
      testResult.downlinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.downlinkNetworkQualities.length
    );
  }
    
  // The check ends. Clear the relevant status.
  uplinkClient.leave();
  downlinkClient.leave();
  localStream.close();
}, 15 * 1000);
```

## TRTC Compatibility Check

You can use the [TRTC check page](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) to check your current environment where you want to use the TRTC SDK. You can also click **Generate Report** to get the current environment report for environment check and troubleshooting.

