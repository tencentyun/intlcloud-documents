## v8.4.1 Released on March 26, 2021

**New features**
- macOS: supported capturing system audio via [startSystemAudioLoopback](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startSystemAudioLoopback), i.e., the system loopback feature that is enabled on Windows. The feature allows the SDK to capture system audio so that anchors can stream local audio or video files to other users.
- macOS: supported callback of the system audio capturing result via [onSystemAudioLoopbackError](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSystemAudioLoopbackError), which allows you to learn about the status of the system audio driver.
- macOS: supported local preview for screen sharing. You can now display screen sharing preview in a small window.
- All platforms: supported the beauty filter plugin architecture.

**Quality improvement**
- All platforms: improved audio quality in the [TRTCAudioQualityMusic](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb) mode, which makes it more suitable for Clubhouse-like audio streaming scenarios.
- All platforms: improved the adaptability to poor network conditions across the audio-video link. Smooth audio and video can be delivered under 70% of extremely poor network conditions.
- Windows: improved audio quality in some streaming scenarios by significantly reducing audio damage.
- Windows: improved performance by 20-30% in some scenarios.

**Bug fixing**
- macOS: fixed the issue where after the screen sharing user switched to sharing the desktop and then back to a specific window on Mac mini (M1), remote users still saw the user’s desktop.
- macOS: fixed the issue where the shared content was not highlighted (on macOS 11.1 and 10.14.5, the green border did not show around the shared content; on macOS 10.3.2, the green border showed, but the shared window flickered when maximized.)
- macOS: fixed the issue where the SDK crashed when users got the screen sharing list on Mac mini (M1) and "" was returned when `sourceName` was null.
- macOS: fixed the issue on Mac mini (M1) where the SDK crashed when `getCurrentMicDevice` was called because `sourceName` was empty.
- Windows: fixed the issue where the SDK crashed when the desktop was shared on Windows Server 2019 Datacenter x64.
- Windows: fixed the issue where screen sharing sometimes ended unexpectedly when the target window was resized during screen sharing.
- Windows: fixed the issue of image capturing failure with some cameras.

## v8.2.7 Released on January 6, 2021

**New APIs**
- Windows & macOS: added [switchRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#switchRoom) to switch rooms.
- Windows & macOS: added [setLocalRenderParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalRenderParams) to set rendering parameters for the local image (primary stream).
- Windows & macOS: added [setRemoteRenderParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteRenderParams) to set rendering parameters for a remote image.
- Windows & macOS: added [startPlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startPlayMusic) to play background music.
- Windows & macOS: added [stopPlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopPlayMusic) to stop background music.
- Windows & macOS: added [pausePlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pausePlayMusic) to pause background music.
- Windows & macOS: added [resumePlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumePlayMusic) to resume background music.
- Windows & macOS: added [getMusicDurationInMS](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getMusicDurationInMS) to get the total length of the background music file, in milliseconds.
- Windows & macOS: added [seekMusicToPosInTime](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#seekMusicToPosInTime) to set the playback progress of background music.
- Windows & macOS: added [setAllMusicVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAllMusicVolume) to set background music volume. This API is used to control the volume of background music when background music is mixed into played audio.
- Windows & macOS: added [setMusicPlayoutVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMusicPlayoutVolume) to set the local playback volume of background music.
- Windows & macOS: added [setMusicPublishVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMusicPublishVolume) to set the remote playback volume of background music.
- Windows & macOS: added [onSwitchRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSwitchRoom) for the callback of room switching.
- Windows & macOS: added [setRemoteAudioVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteAudioVolume) to set the playback volume of a remote user.
- Windows & macOS: added [snapshotVideo](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#snapshotVideo) to take a video screenshot.
- Windows & macOS: added [onSnapshotComplete](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSnapshotComplete) for the callback of the completion of a screenshot.

**Improvements**
- Windows & macOS: supported the string type parameter `strRoomId` for `enterRoom` and `switchRoom`.
- Windows & macOS: fixed other bugs.

## v7.9.348 Released on November 12, 2020

**Improvements**
- Windows: supported the use of Chinese paths to save recording files.
- Windows: supported the anti-covering feature in the window capturing area.

## v7.8.342 Released on October 10, 2020

**New APIs**
- Windows & macOS: added [onAudioDeviceCaptureVolumeChanged](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged) for volume change callback on the current audio capturing device.
- Windows & macOS: added [onAudioDevicePlayoutVolumeChanged](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged) for volume change callback on the current audio playback device.

## v7.7.330 Released on September 11, 2020

**New APIs**
Windows & macOS: added [setAudioQuality](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioQuality) to adjust audio quality.

**Improvements**
- Windows: fixed the issue where CPU utilization was too high when some low-end cameras were used.
- Windows: optimized the compatibility with multiple USB cameras and mics to make it easier to turn on such devices.
- Windows: optimized the selection policy of cameras and mics to avoid audio/video capturing exceptions caused by plugging in and unplugging cameras or mics.
- Windows & macOS: fixed other bugs.

## v7.6.300 Released on August 26, 2020

**New file**
Windows & macOS: added [setCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDeviceMute), [getCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentMicDeviceMute), [setCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerDeviceMute), and [getCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerDeviceMute) to control mics and speakers on PC.

## v7.5.210 Released on August 11, 2020

**Improvements**
- Windows & macOS: fixed the issue where SDK callbacks were not in sequence.
- Windows & macOS: fixed the issue where switching rendering modes caused crashes. 
- Windows & macOS: fixed the issue where rendering failed for certain resolutions. 
- Windows & macOS: fixed other bugs.

## v7.4.204 Released on July 01, 2020

**Improvements**
- Windows: optimized the acoustic echo cancellation (AEC) effect on Windows.
- Windows: improved the compatibility with cameras on Windows.
- Windows: improved the compatibility with audio devices (mics and speakers) on Windows.
- Windows: fixed the issue where the `UserID` called back by `onPlayAudioFrame` on Windows was incorrect.
- Windows: supported system audio mixing on 64-bit Windows.

## v7.2.174 Released on April 20, 2020

**Improvements**
- macOS: fixed the local custom rendering resolution inconsistency issue on macOS.
- Windows: optimized the `getCurrentCameraDevice` logic on Windows to return the first device as the default device when the camera is not used.
- Windows: fixed the issue where the highlighted window was displayed as a gray screen during screen sharing.
- Windows: fixed the issue where the system occasionally froze when users got screen share thumbnails on Windows 10.
- Windows & macOS: fixed the issue where the custom stream ID occasionally failed to take effect immediately after role switching.
- Windows & macOS: fixed the issue where the encoding parameters of screen sharing did not take effect.
- Windows: fixed the issue where it took a long time for a screen shared by a Windows user to be displayed to a WebRTC user.

## v7.1.157 Released on April 02, 2020

**New Features**

Supported [screen sharing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startScreenCapture) via the [primary stream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoStreamType).

**Improvements**
- improved the usability of [preset stream mixing templates](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCTranscodingConfigMode).
- increased the success rate of [stream mixing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMixTranscodingConfig).
- optimized screen sharing on Windows.


## v7.0.149 Released on March 19, 2020

**New file**

Added the [trtc.d.ts](https://intl.cloud.tencent.com/document/product/647/35141) file for TypeScript developers.
