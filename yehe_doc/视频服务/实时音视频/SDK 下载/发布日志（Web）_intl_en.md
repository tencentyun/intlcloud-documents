A version number is in the format of `major.minor.patch`, where:

- `major`: major version number. If there is major version refactoring, this field will be incremented. Generally, the APIs of different major versions are not compatible with each other.
- `minor`: minor version number. The APIs of different minor versions are compatible with each other. If there is a new or optimized API, this field will be incremented.
- `patch`: patch number. If there is a feature improvement or bug fix, this field will be incremented.

> !
> - You are advised to update to the latest version in a timely manner for service stability and better online support.
> - For notes on version updates, please see [Update Guidelines](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html).

## Version 4.14.4 @2022.09.30

**Improvement**

- Avoid the issue that Mac Firefox reports an error when camera captures below 352 * 288 resolution.[Firefox issue](https://bugzilla.mozilla.org/show_bug.cgi?id=1529907).
- Optimize task scheduling and reduce resource consumption.

**Bug Fixed**

- Fix the issue that the videoTrack occasionally fails when unplug and plug in camera after replacing videoTrack with localStream.replaceTrack.

## Version 4.14.3 @2022.09.09

**Bug Fixed**

- Fixed the issue that occasionally fails to TRTC.getCameras() in 'use strict' mode when using Chrome Privacy Mode.
- Fixed the problem of abnormal volume acquisition when entering a room without interaction on the page.

## Version 4.14.2 @2022.08.26

**Feature**

- Support calling the native interface [getCapabilities](https://developer.mozilla.org/en-US/docs/Web/API/InputDeviceInfo/getCapabilities) on the device item obtained from [TRTC.getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#getCameras) and [TRTC.getMicrophone](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#getMicrophones).

**Improvement**

- Optimize the recovery logic of device capture abnormality in the scenarios of iOS (receiving phone call, alarm, waking up Siri).
- Optimize the H264 support detection logic to avoid the issue that Android Chrome 88 or below does not support H264 when the browser is first opened.

## Version 4.14.1 @2022.08.11

**Feature**

- Support for sending SEI messages, [Client.sendSEIMessage](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#sendSEIMessage).

**Improvement**

- Improve [Client.switchRole](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#switchRole) interface robustness.

## Version 4.14.0 @2022.08.05

**Breaking Change**

- Modify the callback parameters of the [Client.on('client-banned')](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#CLIENT_BANNED) event, to be noted when upgrading.

**Feature**

- Support for setting capture volume, [LocalStream.setAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioCaptureVolume).

**Improvement**

- Modify the [Client.on('client-banned')](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#CLIENT_BANNED) event callback parameter to add a passive kickout reason.
- Avoid the issue that Firefox screen sharing capture resolution is not as expected.
- Avoid the issue of occasional black screen of local stream playback in iOS Safari.
- Optimize small stream encoding performance for low-end PC devices.

**Bug Fixed**

- Fix the issue that the screen sharing bitrate is not as expected in certain scenarios.

## Version 4.13.0 @2022.07.08

**Feature**

- Add an new API [Client.destroy](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#destroy). [Client life cycle](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html)

**Improvement**

- Improve the encoding performance of small stream.
- Add an new stream event: [DEVICE_AUTO_RECOVERED](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.DEVICE_AUTO_RECOVERED).

**Bug Fixed**

- Fix the issue that when [Client.startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startMixTranscode) interface initiates cloud mixing, the mixing does not continue after the network is disconnected for more than 30s and the network is restored.

- Fix the problem that when [Client.startPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startPublishCDNStream) interface pushes the stream to CDN, the network is disconnected for more than 30s and the CDN stream is disconnected after the network is restored.

## Version 4.12.7 @2022.06.17

- Change default video profile to `480p_2`, refer to [LocalStream.setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setVideoProfile).
- Improve auto-resume playback success rate.
- Improve mute state accuracy after disconnection and reconnection.
- Circumvent the Mac Safari 15.1 muteVideo page crash issue。[webkit bug](https://bugs.webkit.org/show_bug.cgi?id=232006).

**Bug Fixed**

- Fix the problem that `stream-added` event is not thrown occasionally in Dual-Stream Mode (non-autoSubscribe)。

## Version 4.12.6 @2022.06.10

**Improvement**

- Add avoid-repeated join room logic for client.join api. refer to: [Update Guidelines](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html)

## Version 4.12.5 @2022.05.20

**Bug Fixed**

- Fix the issue that loading trtc.umd.js cause error in IE browser.
- Fix the issue that small stream plays abnormally when the subscription status changes.
- Add workaround for Chrome 70 and below, where moving the div container causes playback to pause.

## Version 4.12.4 @2022.05.07

**Improvement**

- Optimize the process of joining room and reduce the time taken to join room.
- Optimize the logic of switching small stream.

**Bug Fixed**

- Fix the issue that stream-added event is not fired occasionally.
- Fix the issue that Firefox can't capture 480p with Logitech camera.
- Fix the issue that iPad WKWebview reports an error when loading sdk

## Version 4.12.3 @2022.04.19

**Improvement**

- Optimize iOS 13 and 14 high-resolution capture logic.
- Optimize event listening logic to avoid SDK catching business-side errors.
- Added Safari volume reporting for easy dashboard troubleshooting.

**Bug Fixed**

- Fix the issue that the SDK failed to reconnect after the network disconnection was restored in live mode.
- Fix the issue of iOS 11 getting volume abnormality.

## Version 4.12.2 @2022.04.02

**Improvement**

- Optimize volume calculation logic to reduce memory usage and performance overhead.

**Bug Fixed**

- Fix the issue that user was kicked occasionally when page is invisible for long time.
- Fix the echo issue after switching camera in iOS 15.2 ~ 15.4. Reference: [iOS Safari known issue case 11](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-02-info-webrtc-issues.html#h2-4).

## Version 4.12.1 @2022.03.18

**Note**

- Before upgrading, please read the [Update Guidelines](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html).

**Improvement**

- [stream.play](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html#play) supports repeat calls, mirroring, and dynamic modification of playback parameters.
- Improve the automatic recovery logic.

**Bug Fixed**

- Fix the issue of black screen of small streams at the remote end after muteVideo/unmuteVideo.
- Fix the issue that `stream-subscribed` event is thrown after client.setRemoteVideoStreamType.

**Breaking Change**

- The `mirror` parameter of [TRTC.createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createStream) is deprecated, use [stream.play](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html#play) instead.

## Version 4.12.0 @2022.03.04

**Note**

- Before upgrading, please read the [Update Guidelines](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html).

**Feature**

- [client.setRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setRemoteVideoStreamType) return a Promise object.

**Improvement**

- Improve the accuracy of overseas server scheduling.

**Bug Fixed**

- Fix the issue of receiving unexpected [CLIENT_BANNED](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CLIENT_BANNED) event occasionally.

## Version 4.11.13 @2022.02.17

**Improvement**

- Update Typescript decalration file on npm package.
- Improve the param validation logic of [stream.play](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html#play).

**Bug Fixed**

- [LocalStream.initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize) failed before user grant permission on iOS 13.
- The event [AUDIO_VOLUME](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.AUDIO_VOLUME) may received value of 0.

## Version 4.11.12 @2022.01.11

**Improvement**

- Add `index.d.ts` file to npm package.
- Optimize the logic of [stream.close()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html#close).
- Optimize the signaling interaction logic of frequent publish/unpublish on the push side.

**Bug Fixed**

- Page crash when useing "Request Desktop Website" to make a call on iOS 15.1. Reference: [Safari issues case 7](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-02-info-webrtc-issues.html#h2-4).
- The bitrate of [LocalStream.setAudioProfile('high')](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioProfile) is set to 192kbps(128kbps expected).

## Version 4.11.11 @2021.12.17

**Improvement**

- Optimize the logic of capture recovery when device capturing error.
- Optimize the style of AutoplayDialog.

## Version 4.11.10 @2021.12.03

**Bug Fixed**

- AutoPlayDialog cannot be disabled by setting `enableAutoPlayDialog` to false.
- repeated calls to `stream.play` are not blocked by SDK.

## Version 4.11.9 Released on November 26, 2021

**Note**

- Before upgrading, please read the [Update Guidelines](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html).

**Improvement**

- To solve the autoplay failure issue, SDK will show an UI dialog to guide users to click the page when autoplay failure occurs. Reference: [Suggested Solutions for Autoplay Restrictions](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-21-advanced-auto-play-policy.html).
- Optimize the workaround logic of page crash issue in iOS 15.1. Reference: [Safari issues case 7](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-02-info-webrtc-issues.html#h2-4).
- To avoid possible audio playback silent issue, [TRTC.getMicrophones](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getMicrophones) no longer returns microphones with deviceId 'default' & 'communications'. Reference: [Chrome issues case 8 & 9](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-02-info-webrtc-issues.html#h2-2).
- Optimize logic of [LocalStream.switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#switchDevice).
- Improve the accuracy of codec support detection in webview environments.

**Bug Fixed**

- client.publish occasionally throws an error that TRTC is not supported.

## Version 4.11.8 Released on November 5, 2021

**Improvement**

- Add workaround for the occasional video playback black screen issue in iOS 15.0. Reference: [Safari issues case 6](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-02-info-webrtc-issues.html#h2-4).
- Add workaround for the page crash issue in iOS 15.1. Reference: [Safari issues case 7](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-02-info-webrtc-issues.html#h2-4).

## Version 4.11.7 Released on September 30, 2021

**Improvement**

- Add strong verification of API params.
- Add Chinese error message for development mode(Loglevel is set to [Debug](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.LogLevel)).
- Improve the success rate of automatic recapture in case of media device capture exceptions.
- Optimize the call recovery logic after system sleep and reopen.
- Add trtc.esm.js and trtc.umd.js to npm package.

## Version 4.11.6 Released on September 10, 2021

**Improvements**

- Optimized the signaling scheduling logic, improving the success rate of room entry under poor network conditions. If you are using SDK v4.11.5, we recommend that you update to this version.

## Version 4.11.5 Released on September 4, 2021

**Improvements**

- Supported dynamic signaling channel scheduling, improving connection success rate under poor network conditions.

**Bug fixing**

- Fixed occasional failure to receive the `stream-added` event callback after reconnection.
- Fixed the occasional issue where the frame rate drops to 0 after screen sharing continues for a long time.

## Version 4.11.4 Released on August 20, 2021

**Improvements**

- Improved the accuracy of the H.264 support check for OPPO and vivo built-in browsers.
- Supported auto capturing resumption (triggered in case of capturing error).
- Added timeout logic for the `subscribe` API. For details, see the error code [API_CALL_TIMEOUT](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ErrorCode.html#.API_CALL_TIMEOUT).

**Bug fixing**

- Fixed occasional failure to pull streams on Safari for iOS in some older versions.
- Fixed the issue where the mute status is inaccurate after the switching of devices.
- Fixed the occasional issue where exceptions occur when the room entry API is called again after timeout.
- Fixed the issue where, after a remote stream is unpublished, the audio/video player is not terminated in a timely manner.

## Version 4.11.3 Released on July 30, 2021

**Improvements**

- Optimized the exception handling logic for the `publish` and `subscribe` APIs.
- Optimized the recovery policy for audio mixing plugins.

**Bug fixing**

- Fixed the occasional inaccuracy of the `peer-leave` notification.

## Version 4.11.2 Released on July 23, 2021

**Improvements**

- Supported TURN server scheduling, improving connection success rate.
- Added the `hasSmall` property, which indicates whether a remote user has substream video, to [Client.getRemoteMutedState](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteMutedState).

**Bug fixing**

- Fixed the issue where the SDK is unavailable when LocalStorage is disabled.
- Fixed the occasional issue where API requests are not rejected when publishing exceptions occur.

## Version 4.11.1 Released on June 25, 2021

**Improvements**

- Supported the beauty filter plugin. For details, please see [Enabling Beauty Filters](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-28-advanced-beauty.html).
- Improved statistical accuracy.

## Version 4.11.0 Released on June 18, 2021

**New features**

Supported dual streams (primary and substream). For detailed directions, please see [Enabling Dual Streams](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-27-advanced-small-stream.html).

**Improvements**

Optimized the event notification order.

## Version 4.10.3 Released on June 11, 2021

**Improvements**

- Optimized the quality measuring logic and allowed getting call quality statistics via a server-side API.
- Added statistics on RTT and packet loss to [ClientEvent.NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.NETWORK_QUALITY).
- Optimized the API verification logic to prevent exceptions caused by repeated calls.
- Optimized the playback logic, reducing audio loading time.

## Version 4.10.2 Released on May 24, 2021

**Improvements**

- Optimized the implementation logic of the `switchDevice` API, fixing occasional failure to switch to the front camera in Huawei Browser.
- Increased the accuracy of the [StreamEvent.CONNECTION_STATE_CHANGED](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.CONNECTION_STATE_CHANGED) event notification.

**Bug fixing**

- Fixed occasional failure to play screen sharing streams on native applications.
- Fixed occasional failure to receive the `stream-removed` event after reconnection.

## Version 4.10.1 Released on April 30, 2021

**New features**

- Added the [StreamEvent.CONNECTION_STATE_CHANGED](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.CONNECTION_STATE_CHANGED) event for the change of stream connection status.
- Added the [Client.getTransportStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getTransportStats) API, which can be used to obtain downstream RTT.
- Supported using the [Client.getRemoteVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteVideoStats) API to obtain statistics of the substream (screen sharing).

**Improvements**

Optimized the implementation logic of the [Client.switchRole](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#switchRole) API.

**Bug fixing**

- Fixed the issue where the `mute` event is occasionally triggered before `stream-added`.
- Fixed the issue where no audio can be heard sometimes after room entry.

## Version 4.10.0 Released on April 16, 2021

**Improvements**

Optimized the parameter verification logic of the [localStream.switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#switchDevice), [localStream.addTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#addTrack), and [localStream.removeTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#removeTrack) APIs.

## Version 4.9.0 Released on March 19, 2021

**New features**

- Supported the callback of volume. For details, see the [client.enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableAudioVolumeEvaluation) API.

**Improvements**

Changed the default port number of the WebSocket protocol to 443.

**Bug fixing**

- Fixed the issue where audience cannot receive the callbacks of room entry and exit by an anchor in live streaming scenarios.
- Fixed occasional failure to reconnect when string-type room IDs are used.

**Breaking change**

Supported returning detailed results of browser compatibility check via [TRTC.checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.checkSystemRequirements). For details, please see the [API document](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.checkSystemRequirements) and [Update Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html).

## Version 4.8.6 Released on March 1, 2021

**Improvements**

Supported stereo audio playback.
> ! Not supported on iOS yet.

**Bug fixing**

Fixed the issue where the `stream-removed` event is received when audio and video are disabled on a mobile device.

## Version 4.8.5 Released on January 29, 2021

**Improvements**

- Supported configuring multiple TURN servers via [client.setTurnServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setTurnServer).
- Optimized the `userId` verification logic.

**Bug fixing**

Fixed the issue where the mute status is occasionally inaccurate after stream pushing starts.

## Version 4.8.4 Released on January 15, 2021

**Improvements**

- Supported dynamically calling the [localStream.setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setVideoProfile) API.
- Optimized the data reporting logic of the dashboard.
- Optimized the logic of dealing with autoplay restrictions. For details, please see [Suggested Solutions for Autoplay Restrictions](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-21-advanced-auto-play-policy.html).
- Optimized the logic of dealing with failure to recover audio/video capturing after device connection/disconnection. For more information, please see [DEVICE_AUTO_RECOVER_FAILED](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ErrorCode.html#.DEVICE_AUTO_RECOVER_FAILED).

**Bug fixing**

Fixed the issue where the mute status is occasionally inaccurate after stream pushing is resumed.

## Version 4.8.3 Released on January 7, 2021

**Improvements**

Optimized the verification logic for the `roomId` parameter of the room entry API.

**Bug fixing**

- Fixed the lack of third-party dependencies in version 4.8.2.
- Fixed the issue where no audio is played when a user subscribes only to audio streams.
- Fixed the occasional issue where no audio is played or `getAudioLevel` returns `0` after playback is resumed from autoplay restrictions on iOS.

## Version 4.8.2 Released on December 31, 2020

**Improvements**

- Optimized the verification logic for the `roomId` parameter of the room entry API. For more information, please see the [API document](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#join) and [Update Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html).
- Optimized the timing of the `peer-join` and `peer-leave` notifications.

**Bug fixing**

Fixed the occasional `Cannot read property 'isConnected' of null` error during room exit.

**Breaking change**

Deleted the disused API `setDefaultMuteRemoteStreams`. Please use the `autoSubscribe` parameter of [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient) instead.

## Version 4.8.1 Released on December 25, 2020

**Bug fixing**

- Fixed occasional failure to hear remote users’ audio on Windows.
- Fixed the issue where the `client.getRemoteVideoStats()` API returns empty data.

## Version 4.8.0 Released on December 18, 2020

**New features**

- Supported On-Cloud MixTranscoding.
- Supported string-type room IDs on all platforms. For details, please see the `useStringRoomId` parameter of [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient).
- Allowed users to disable auto subscription. For details, please see the `autoSubscribe` parameter of [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient).

**Improvements**

- Optimized the H.264 support check logic.
- Optimized the device switching logic.
- Optimized the status identification logic of the `hasAudio` and `hasVideo` APIs.

**Bug fixing**

- Fixed occasional failure to reconnect after network disconnection.
- Fixed black screen caused by frequent track adding or removing on Safari for iOS.

## Version 4.7.1 Released on November 27, 2020

**Improvements**

- Optimized the auto capturing resumption logic upon switch of media devices (which may be caused by a loose port or device plugging/unplugging).
- Added the error code [DEVICE_AUTO_RECOVER_FAILED](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ErrorCode.html#.DEVICE_AUTO_RECOVER_FAILED), which indicates failure to restart a device.

**Bug fixing**

- Fixed occasional black screen on Chrome 87.
- Fixed the issue where, when both camera and screen sharing streams are pushed from a native application, users on web fail to pull screen sharing streams after subscribing to and unsubscribing from the streams repeatedly.

## Version 4.7.0 Released on November 20, 2020

**New features**

Supported desktop Firefox M56+ and Edge M80+.

**Improvements**

- Optimized the upstream bitrate control logic.
- Optimized the retry logic for getting media devices.
- Optimized the WebSocket reconnection logic.
- Supported auto push resumption when a mic is plugged in/unplugged during audio mixing, optimizing the auto push resumption logic.

**Breaking change**

Supported returning detailed results of browser compatibility check via [TRTC.checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.checkSystemRequirements). For more information, please see the [API document](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.checkSystemRequirements) and [Update Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html).

## Version 4.6.7 Released on November 5, 2020

**Bug fixing**

- Fixed occasional screen corruption during playback when hardware acceleration is enabled on Chrome.
- Fixed failure to enter rooms and pull streams on WeChat’s built-in browser for iOS.

## Version 4.6.6 Released on October 23, 2020

**Improvements**

- Optimized the retry logic for upstream peer connection.
- Optimized the retry logic for downstream peer connection.
- Optimized the logic of `TRTC.checkSystemRequirements`.
- Supported screen sharing on Safari. For details, please see [Screen Sharing Guide](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html).

**Bug fixing**

Fixed the issue where `getAudioLevel` returns `0` after audio playback is manually resumed due to autoplay restrictions.

## Version 4.6.5 Released on October 14, 2020

**Improvements**

- Optimized the logic for reestablishing WebSocket signaling channels, improving connection stability.
- Optimized the log output logic.

**Bug fixing**

- Fixed the issue where `getAudioLevel` returns `0` after resubscription on Chrome.
- Fixed the issue where no audio is played after resubscription on Safari.
- Fixed the issue where the `getLocalVideoStats` API returns `undefined` after the upstream audio track is replaced via `replaceTrack`.
- Fixed occasional WebSocket disconnection upon change of network type during calls on a mobile device.

## Version 4.6.4 Released on September 24, 2020

**Improvements**

Allowed stopping the collection of network quality statistics after room exit.

**Bug fixing**

- Fixed the room entry error on Chrome 56.
- Fixed the issue where image is rotated when relayed push is enabled on mobile devices.
- Fixed on-cloud recording exceptions when audio-only streams are pushed.
- Fixed failure to automatically resume push after the camera is unplugged due to inconsistent resolution.

## Version 4.6.3 Released on August 28, 2020

**Improvements**

- Optimized the compatibility check logic.
- Optimized the log reporting logic.
- Optimized the upstream bitrate control logic.

## Version 4.6.2 Released on August 14, 2020

**Improvements**

- Optimized the upstream bitrate control logic.
- Optimized the `switchRole` parameter verification logic.
- Optimized the logic of measuring upstream network quality.
- Optimized error messages.
- Supported automatically resuming push when change of the stream capturing device is detected.

**Bug fixing**

Fixed failure to publish again immediately after `unpublish` succeeds.

## Version 4.6.1 Released on July 28, 2020

**Improvements**

- Supported checking via [TRTC.isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.isScreenShareSupported) whether screen sharing is supported. Safari does not support screen sharing.
- Optimized the parameter verification logic for the `subscribe` and `unsubscribe` APIs.
- Added network quality logs.

**Bug fixing**

- Fixed the “OverconstrainedError” error when access to media devices is not granted and an empty device ID is passed in the `TRTC.createStream` API.
- Fixed the issue where no log is printed when upstream peer connection is lost.

## Version 4.6.0 Released on July 16, 2020

**New features**

Added the `NETWORK_QUALITY` event.

## Version 4.5.0 Released on July 2, 2020

**New features**

Added the `screenAudio` parameter to the `createStream` API.

**Bug fixing**

- Fixed the issue where echo cancellation does not work in browsers for Android.
- Fixed the issue where the RTT value returned by the `getTransportStats` API is `NAN`.

## Version 4.4.0 Released on May 28, 2020

**New features**

Supported capturing system audio (on Windows) or audio of the current tab (on macOS) during screen sharing on Chrome 74 or above.

## Version 4.3.14 Released on April 29, 2020

**Bug fixing**

Fixed the `muted` and `unmute` events for Mini Program.

## Version 4.3.13 Released on April 16, 2020

**Improvements**

Optimized the availability check logic.

## Version 4.3.12 Released on April 13, 2020

**Bug fixing**

Fixed a potential `RTCPeerConnection` status change exception.

## Version 4.3.11 Released on March 28, 2020

**Improvements**

Supported detection of mobile QQ Browser, which does not support TRTC SDK for desktop browsers at the moment.

**Bug fixing**

Fixed Boolean return types.

## Version 4.3.10 Released on March 17, 2020

**Improvements**

- Optimized the environment detection logic.
- Added `name code` for `RtcError`.

## Version 4.3.9 Released on March 13, 2020

**Improvements**

- Supported automatic detection of the deployment environment.
- Optimized logging.

## Version 4.3.7 Released on February 21, 2020

**Improvements**

Fixed the issue where an exception is throw upon device switch during screen sharing.

**Bug fixing**

- Fixed the device occupation issue by releasing MediaStream after device switch.
- Fixed the potential error of the subscription API.

## Version 4.3.6 Released on February 25, 2020

**Bug fixing**

Adjusted the audio/video playback sequence of `Stream.resume()`, and fixed autoplay exceptions in WeChat’s built-in browser on iOS.

## Version 4.3.5 Released on February 5, 2020

**Improvements**

Added timeout check for the `publish` API, improving the success rate of signaling.

## Version 4.3.4 Released on January 6, 2020

**Improvements**

Updated `core-js` to version 3.6.1.

**Bug fixing**

- Fixed the issue where an exception is thrown after `unpublish` times out.
- Fixed the issue where third-party libraries cause decline in the performance of V8.

## Version 4.3.3 Released on December 25, 2019

**Improvements**

- Added the ability to check whether the environment supports WebRTC.
- Optimized the SDP response mechanism.
- Optimized the reporting logic.

**Bug fixing**

Optimized the TURN URL protocol format.

## Version 4.3.2 Released on December 9, 2019

**Improvements**

- Supported automatic reconnection after downstream ICE disconnection.
- Removed the STUN hole punching step to increase the success rate and speed of user connection via private networks.
- Used the server-calibrated UTC time as the timestamp for log reporting.
- Optimized ICE error reporting.
- Added more key events to `avmonitor`.

**Bug fixing**

- Fixed the 1005 reconnection error of WebSocket signaling channels.
- Fixed the issue with the reporting of downstream packet loss rate.

## Version 4.3.1 Released on November 23, 2019

**Improvements**

Supported automatic reconnection when upstream ICE disconnects during calls.

**Bug fixing**

Fixed the issue where the host ICE candidate of public IP type does not take effect after STUN hole punching fails.

## Version 4.3.0 Released on November 15, 2019

**New features**

Added the `client.getTransportStats()` API.

**Improvements**

- Made log reporting more detailed.
- Supported wildcard characters for event unbinding.
- Extended the connection timeout threshold to 5 seconds.
- Extended the publishing timeout threshold to 5 seconds.

**Bug fixing**

Fixed the issue of abnormal SDK judgment due to modification of the prototype chain of `zone.js`.

## Version 4.2.0 Released on November 4, 2019

**New features**

Added the `client.off()` API, which can be used to unbind client events.

**Improvements**

- Optimized the collection of call status statistics.
- Added permission check for `client.publish()`.
- Added an auto playback error prompt for `stream.play()` and `stream.resume()`.

**Bug fixing**

Fixed black screen when the camera is switched via `localStream.switchDevice()`.

## Version 4.1.1 Released on October 24, 2019

**Bug fixing**

- Fixed log loss.
- Fixed the loss of remote users who reconnect after disconnection.

## Version 4.1.0 Released on October 17, 2019

**New features**

- Supported passing object `HTMLDivElement` in the `stream.play()` API.
- Supported setting audio attributes via `localStream.setAudioProfile()`. Currently, two profiles are supported: standard and high.

**Bug fixing**

- Fixed the restriction on the number of WebAudio Context on Chrome.
- Fixed the issue where the local audio/video player is not restarted after `replaceTrack()`.
- Fixed the issue where custom settings via `localStream.setScreenProfile()` do not take effect.
- Fixed the issues with the restart of the audio/video player and status reporting.

## Version 4.0.0 Released on October 11, 2019

Provided APIs in the Client/Stream format, allowing for clearer role assignment and naming.
The new version is not compatible with the legacy version. In addition to APIs, the new version introduced the following changes:

- Changed the method of setting video attributes. All video attributes (resolution, frame rate, and bitrate) are now set using the `localStream.setVideoProfile()` API of the SDK via applications. The new version does not support setting video attributes via “Image Settings” (Spear Role) in the Tencent Cloud console.
- Integrated an audio/video player into the stream object. Playback is now solely controlled by the SDK.
- Supported subscribing to and unsubscribing from remote audio/video streams via the `client.subscribe()` and `client.unsubscribe()` APIs.
