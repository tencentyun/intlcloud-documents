## Version 9.3.201 Released on January 5, 2022

**New features**
- Windows & macOS: added the [onSpeedTestResult](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSpeedTestResult) callback, which returns the result of network speed testing.

**Improvements**
- Windows & macOS: improved the performance of the speed testing API [startSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeedTest).
- Windows & macOS: added the `streamType` parameter to the [muteLocalVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalVideo) API (which is used to pause/resume publishing local video).
- Windows & macOS: added the `streamType` parameter to the [muteRemoteVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteVideoStream) API (which is used to pause/resume receiving a remote video stream).
- Windows & macOS: added the `source`, `captureRect`, and `property` parameters to the [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) API (which is used to configure screen sharing).
- Windows & macOS: added the `params` parameter to the [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) API (which is used to start screen sharing).

**Bug fixing**
- macOS: fixed the camera video capturing issue on macOS 12.
- Windows & macOS: optimized the QoS control policy under poor network conditions to enable smoother communication.
- Windows: improved the AGC algorithm, reducing cases of excessively low or high volume.
- Windows: fixed the frame rate exception for the capturing of screen sharing images.

## Version 8.9.102 Released on August 11, 2021

**New features**
Windows & macOS: added the new parameter `gatewayRtt` to the [onStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStatistics) callback.

**Bug fixing**
- macOS: fixed crash caused by logging on special devices.
- macOS: fixed the issue where, after `setAudioCaptureVolume(0)` is used to mute audio, the mic testing volume is 0.
- Windows: improved performance and fixed the issue of black screen after the camera is turned on.
- Windows: fixed the issue where the resolution is not restored after being automatically reduced during screen sharing.
- Windows & macOS: fixed other bugs.

## Version 8.6.101 Released on May 28, 2021

**New features**
- Windows & macOS: added APIs for excluding windows from screen sharing: [addExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#addExcludedShareWindow), [removeExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeExcludedShareWindow), [removeAllExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeAllExcludedShareWindow).
- Windows & macOS: added the `isMinimizeWindow` field to the return code of the sharable window enumerating API [getScreenCaptureSources](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources).
- Windows & macOS: supported passing constructor functions as parameters to APIs.

**Bug fixing**
- Windows: fixed the issue where paths containing Chinese characters are not supported for plugin loading.
- Windows & macOS: fixed the `webgl context lost` issue.
- Windows & macOS: fixed the issue where the images of remote users freeze after the local user switches to the small image (dual-channel encoding enabled).
- Windows & macOS: fixed the issue where, when a user enters the room and starts pulling streams, the images of remote users are blurred before they gradually become clear.

## v8.4.1 Released on March 26, 2021

**New features**
- macOS: supported capturing system audio via [startSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSystemAudioLoopback), i.e., the system loopback feature that is enabled on Windows. The feature allows the SDK to capture system audio so that anchors can stream local audio or video files to other users.
- macOS: supported callback of the system audio capturing result via [onSystemAudioLoopbackError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSystemAudioLoopbackError), which allows you to learn about the status of the system audio driver.
- macOS: supported local preview for screen sharing. You can now display screen sharing preview in a small window.
- All platforms: supported the beauty filter plugin architecture.

**Quality improvement**
- All platforms: improved audio quality in the [music](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) mode, which makes it more suitable for Clubhouse-like audio streaming scenarios.
- All platforms: improved the adaptability to poor network conditions. Smooth audio and video can be delivered even when the packet loss rate reaches 70%.
- Windows: improved audio quality in some streaming scenarios by significantly reducing audio damage.
- Windows: improved performance by 20%-30% in some scenarios.

**Bug fixing**
- macOS: fixed the issue where, after the screen sharing user switches to desktop sharing and then back to the sharing of a specific window on Mac mini (M1), remote users still see the user’s desktop.
- macOS: fixed the issue where the shared content is not highlighted (on macOS 11.1 and 10.14.5, there isn’t a green border around the shared content; on macOS 10.3.2, the green border is displayed, but the shared window flickers when maximized).
- macOS: fixed the issue where, when users on Mac mini (M1) get the screen sharing list, the SDK crashes because `sourceName` is null and "" is returned.
- macOS: fixed the issue on Mac mini (M1) where, when `getCurrentMicDevice` is called, the SDK crashes because `sourceName` is empty.
- Windows: fixed the issue where the SDK crashes when the desktop is shared on Windows Server 2019 Datacenter x64.
- Windows: fixed the issue where screen sharing sometimes ends unexpectedly when the target window is resized during screen sharing.
- Windows: fixed image capturing failure with some cameras.

## v8.2.7 Released on January 6, 2021

**New features**
- Windows & macOS: added [switchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRoom) to switch rooms.
- Windows & macOS: added [setLocalRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalRenderParams) to set rendering parameters for the local image (primary stream).
- Windows & macOS: added [setRemoteRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParams) to set rendering parameters for a remote image.
- Windows & macOS: added [startPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPlayMusic) to play background music.
- Windows & macOS: added [stopPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPlayMusic) to stop background music.
- Windows & macOS: added [pausePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pausePlayMusic) to pause background music.
- Windows & macOS: added [resumePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumePlayMusic) to resume background music.
- Windows & macOS: added [getMusicDurationInMS](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getMusicDurationInMS) to get the total length of the background music file, in milliseconds.
- Windows & macOS: added [seekMusicToPosInTime](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#seekMusicToPosInTime) to set the playback progress of background music.
- Windows & macOS: added [setAllMusicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllMusicVolume) to set the audio mixing volume of background music.
- Windows & macOS: added [setMusicPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPlayoutVolume) to set the local playback volume of background music.
- Windows & macOS: added [setMusicPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPublishVolume) to set the remote playback volume of background music.
- Windows & macOS: added the [onSwitchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRoom) callback for room switching.
- Windows & macOS: added [setRemoteAudioVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteAudioVolume) to set the playback volume of a remote user.
- Windows & macOS: added [snapshotVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#snapshotVideo) to take a video screenshot.
- Windows & macOS: added the [onSnapshotComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSnapshotComplete) callback for the completion of a screenshot.

**Improvements**
- Windows & macOS: supported string-type `strRoomId` for the `enterRoom` and `switchRoom` APIs.
- Windows & macOS: fixed other bugs.

## v7.9.348 Released on November 12, 2020

**Improvements**
- Windows: supported the use of paths containing Chinese characters to save recording files.
- Windows: supported the anti-covering feature in the window capturing area.

## v7.8.342 Released on October 10, 2020

**New features**
- Windows & macOS: added the [onAudioDeviceCaptureVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged) callback for volume change of the current audio capturing device.
- Windows & macOS: added the [onAudioDevicePlayoutVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged) callback for volume change of the current audio playback device.

## v7.7.330 Released on September 11, 2020

**New features**
Windows & macOS: added [setAudioQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioQuality) to adjust audio quality.

**Improvements**
- Windows: fixed the issue of high CPU utilization when some low-end cameras are used.
- Windows: optimized the compatibility with multiple USB cameras and mics to make it easier to turn on such devices.
- Windows: optimized the selection policy of cameras and mics to avoid audio/video capturing exceptions caused by the connection/disconnection of cameras and mics.
- Windows & macOS: fixed other bugs.

## v7.6.300 Released on August 26, 2020

**New features**
Windows & macOS: added [setCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDeviceMute), [getCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDeviceMute), [setCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerDeviceMute), and [getCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerDeviceMute) to control mics and speakers on PC.

## v7.5.210 Released on August 11, 2020

**Improvements**
- Windows & macOS: fixed the issue where SDK callbacks are not in sequence.
- Windows & macOS: fixed the issue where switching rendering modes causes crashes. 
- Windows & macOS: fixed the issue where rendering fails for certain resolutions. 
- Windows & macOS: fixed other bugs.

## v7.4.204 Released on July 01, 2020

**Improvements**
- Windows: optimized the acoustic echo cancellation (AEC) effect on Windows.
- Windows: improved the compatibility with cameras on Windows.
- Windows: improved the compatibility with audio devices (mics and speakers) on Windows.
- Windows: fixed the issue where the `UserID` returned by `onPlayAudioFrame` is incorrect on Windows.
- Windows: supported system audio mixing on 64-bit Windows.

## v7.2.174 Released on April 20, 2020

**Improvements**
- macOS: fixed occasional resolution inconsistency for local custom rendering on macOS.
- Windows: optimized the `getCurrentCameraDevice` logic on Windows to return the first device as the default device when the camera is not used.
- Windows: fixed the issue where the highlighted window is displayed as a gray screen during screen sharing.
- Windows: fixed the issue where the system occasionally freezes when users get screen share thumbnails on Windows 10.
- Windows & macOS: fixed the issue where the custom stream ID occasionally fails to take effect immediately after role switching.
- Windows & macOS: fixed the issue where the encoding parameters of screen sharing do not take effect.
- Windows: fixed the issue where it takes a long time for a screen shared by a Windows user to be displayed to a WebRTC user.

## v7.1.157 Released on April 02, 2020

**New features**

Supported [screen sharing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) via the [primary stream](ttps://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoStreamType).

**Improvements**
- Improved the usability of [preset stream mixing templates](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCTranscodingConfigMode).
- Increased the success rate of [stream mixing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMixTranscodingConfig).
- Optimized screen sharing on Windows.


## v7.0.149 Released on March 19, 2020

**New features**

Added the [trtc.d.ts](https://intl.cloud.tencent.com/document/product/647/35141) file for TypeScript developers.
