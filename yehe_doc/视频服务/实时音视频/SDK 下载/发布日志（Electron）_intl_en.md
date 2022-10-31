## Version 10.3.401 Released on July 20, 2022

#### Improvements
- Improved performance.
- Updated the underlying library.

## Version 9.3.201 Released on January 5, 2022

#### New features
- Windows & macOS: Added the [onSpeedTestResult](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSpeedTestResult) callback, which returns the result of network speed testing.

#### Improvements
- Windows & macOS: Improved the performance of the speed testing API [startSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeedTest).
- Windows & macOS: Added the `streamType` parameter to the [muteLocalVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalVideo) API.
- Windows & macOS: Added the `streamType` parameter to the [muteRemoteVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteVideoStream) API.
- Windows & macOS: Added the `params` parameter to the [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) API.

#### Bug fixing
- macOS: Fixed the camera video capturing issue on macOS 12.
- Windows & macOS: Optimized the QoS control policy under poor network conditions for smoother communication.
- Windows: Improved the AGC algorithm, reducing cases of excessively low or high volume.
- Windows: Fixed the issue of abnormal capturing frame rate for screen sharing.

## Version 8.9.102 Released on August 11, 2021

#### New features
Windows & macOS: Added the new parameter `gatewayRtt` to the [onStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStatistics) callback.

#### Bug fixing
- macOS: Fixed crash caused by logging on special devices.
- macOS: Fixed the issue where, after `setAudioCaptureVolume(0)` is used to mute audio, the mic testing volume is 0.
- Windows: Improved performance and fixed the issue of black screen after the camera is turned on.
- Windows :Fixed the issue where the resolution is not restored after being automatically reduced during screen sharing.
- Windows & macOS: Fixed other bugs.

## Version 8.6.101 Released on May 28, 2021

#### New features
- Windows & macOS: Added APIs for excluding windows from screen sharing: [addExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#addExcludedShareWindow), [removeExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeExcludedShareWindow), [removeAllExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeAllExcludedShareWindow).
- Windows & macOS: Added the `isMinimizeWindow` field to the data returned by the [getScreenCaptureSources](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources) API.
- Windows & macOS: Added support for passing constructor functions as parameters to APIs.

#### Bug fixing
- Windows: Fixed the issue where paths containing Chinese characters are not supported for plugin loading.
- Windows & macOS: Fixed the `webgl context lost` issue.
- Windows & macOS: Fixed the issue where the videos of remote users freeze after the local user switches to the low-quality stream (dual-stream mode enabled).
- Windows & macOS: Fixed the issue where, when a user enters the room and starts pulling streams, the images of remote users are blurred before they gradually become clear.

## Version 8.4.1 Released on March 26, 2021

#### New features
- macOS: Added support for capturing system audio via [startSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSystemAudioLoopback), i.e., the system loopback feature that is enabled on Windows. The feature allows the SDK to capture system audio so that anchors can stream local audio or video files to other users.
- macOS: Added the [onSystemAudioLoopbackError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSystemAudioLoopbackError) callback, which updates you on the status of the system audio driver.
- macOS: Added support for local preview for screen sharing. You can now display screen sharing preview in a small window.
- All platforms: Added support for beauty filter plugins.

#### Improvements
- All platforms: Improved audio quality in the [music](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) mode, which makes it more suitable for Clubhouse-like audio streaming scenarios.
- All platforms: Improved the adaptability to poor network conditions. Smooth audio and video can be delivered even when the packet loss rate reaches 70%.
- Windows: Improved audio quality in some streaming scenarios by significantly reducing audio damage.
- Windows: Improved performance by 20%-30% in some scenarios.

#### Bug fixing
- macOS: Fixed the issue where, after the screen sharing user switches to desktop sharing and then back to the sharing of a specific window on Mac mini (M1), remote users still see the user’s desktop.
- macOS: Fixed the issue where the shared content is not highlighted (on macOS 11.1 and 10.14.5, there isn’t a green border around the shared content; on macOS 10.3.2, the green border is displayed, but the shared window flickers when maximized).
- macOS: Fixed the issue where, when users on Mac mini (M1) get the screen sharing list, the SDK crashes because `sourceName` is null and "" is returned.
- macOS: Fixed the issue on Mac mini (M1) where, when `getCurrentMicDevice` is called, the SDK crashes because `sourceName` is empty.
- Windows: Fixed the issue where the SDK crashes when the desktop is shared on Windows Server 2019 Datacenter x64.
- Windows: Fixed the issue where screen sharing sometimes ends unexpectedly when the target window is resized during screen sharing.
- Windows: Fixed image capturing failure with some cameras.

## Version 8.2.7 Released on January 6, 2021

#### New features
- Windows & macOS: Added the [switchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRoom) API.
- Windows & macOS: Added the [setLocalRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalRenderParams) API, which can be used to set rendering parameters for the local image (primary stream).
- Windows & macOS: Added the [setRemoteRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParams) API, which can be used to set rendering parameters for a remote image.
- Windows & macOS: Added the [startPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPlayMusic) API, which is used to play background music.
- Windows & macOS: Added the [stopPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPlayMusic) API, which is used to stop background music.
- Windows & macOS: Added the [pausePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pausePlayMusic) API, which is used to pause background music.
- Windows & macOS: Added the [resumePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumePlayMusic) API, which is used to resume background music.
- Windows & macOS: Added the [getMusicDurationInMS](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getMusicDurationInMS) API, which is used to get the total length of the background music file, in milliseconds.
- Windows & macOS: Added the [seekMusicToPosInTime](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#seekMusicToPosInTime) API, which is used to set the playback progress of background music.
- Windows & macOS: Added the [setAllMusicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllMusicVolume) API, which is used to set the audio mixing volume of background music.
- Windows & macOS: Added the [setMusicPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPlayoutVolume) API, which is used to set the local playback volume of background music.
- Windows & macOS: Added the [setMusicPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPublishVolume) API, which is used to set the remote playback volume of background music.
- Windows & macOS: Added the [onSwitchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRoom) callback for room switching.
- Windows & macOS: Added the [setRemoteAudioVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteAudioVolume) API, which is used to set the playback volume of a remote user.
- Windows & macOS: Added the [snapshotVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#snapshotVideo) API, which is used to take a video screenshot.
- Windows & macOS: Added the [onSnapshotComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSnapshotComplete) callback for the completion of a screenshot.

#### Improvements
- Windows & macOS: Added support for string-type `strRoomId` for the `enterRoom` and `switchRoom` APIs.
- Windows & macOS: Fixed other bugs.

## Version 7.9.348 Released on November 12, 2020
#### Improvements
- Windows: Added support for the use of paths containing Chinese characters to save recording files.
- Windows: Added support for the anti-covering feature in the window capturing area.

## Version 7.8.342 Released on October 10, 2020
#### New features
- Windows & macOS: Added the [onAudioDeviceCaptureVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged) callback for volume change of the current audio capturing device.
- Windows & macOS: Added the [onAudioDevicePlayoutVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged) callback for volume change of the current audio playback device.

## Version 7.7.330 Released on September 11, 2020
#### New features
Windows & macOS: Added the [setAudioQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioQuality) API, which is used to adjust audio quality.

#### Improvements
- Windows: Fixed the issue of high CPU utilization when some low-end cameras are used.
- Windows: Improved compatibility with multiple USB cameras and mics to make it easier to turn on such devices.
- Windows: Optimized the selection policy of cameras and mics to avoid audio/video capturing errors caused by device change.
- Windows & macOS: Fixed other bugs.

## Version 7.6.300 Released on August 26, 2020
#### New features
Windows & macOS: Added APIs [setCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDeviceMute), [getCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDeviceMute), [setCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerDeviceMute), and [getCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerDeviceMute), which are used to control mics and speakers on PC.

## Version 7.5.210 Released on August 11, 2020
#### Improvements
- Windows & macOS: Fixed the issue where SDK callbacks are not in sequence.
- Windows & macOS: Fixed the issue where switching rendering modes causes crashes. 
- Windows & macOS: Fixed the issue where rendering fails for certain resolutions. 
- Windows & macOS: Fixed other bugs.

## Version 7.4.204 Released on July 01, 2020
#### Improvements
- Windows: Optimized the acoustic echo cancellation (AEC) effect on Windows.
- Windows: Improved compatibility with cameras on Windows.
- Windows: Improved compatibility with audio devices (mics and speakers) on Windows.
- Windows: Fixed the issue where the `UserID` returned by `onPlayAudioFrame` is incorrect on Windows.
- Windows: Added support for system audio mixing on 64-bit Windows.

## Version 7.2.174 Released on April 20, 2020
#### Improvements
- macOS: Fixed occasional resolution inconsistency for local custom rendering on macOS.
- Windows: Optimized the `getCurrentCameraDevice` logic on Windows to return the first device when the camera is not used.
- Windows: Fixed the issue where the highlighted window is displayed as a gray screen during screen sharing.
- Windows: Fixed the issue where the system occasionally freezes when users get screen share thumbnails on Windows 10.
- Windows & macOS: Fixed the issue where the custom stream ID occasionally fails to take effect immediately after role switching.
- Windows & macOS: Fixed the issue where encoding parameters for screen sharing do not take effect.
- Windows: Fixed the issue where it takes a long time for a screen shared by a Windows user to be displayed to a WebRTC user.

## Version 7.1.157 Released on April 02, 2020
#### New features
Supported [screen sharing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) via the [primary stream](ttps://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoStreamType).

#### Improvements
- Improved the usability of [preset stream mixing templates](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCTranscodingConfigMode).
- Increased the success rate of [stream mixing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMixTranscodingConfig).
- Optimized screen sharing on Windows.


## Version 7.0.149 Released on March 19, 2020
#### New features
Added the [trtc.d.ts](https://intl.cloud.tencent.com/document/product/647/35141) file for TypeScript developers.
