## v7.8.342 Released on October 10, 2020

**Added**
- Windows and macOS: added [onAudioDeviceCaptureVolumeChanged](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged) for volume change callback on the current audio capture device.
- Windows and macOS: added [onAudioDevicePlayoutVolumeChanged](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged) for volume change callback on the current audio playback device.

## v7.7.330 Released on September 11, 2020

**Added**
Windows and macOS: added [setAudioQuality](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioQuality) to adjust audio quality.

**Improvements**
- Windows: optimized the issue where the CPU utilization was too high in some low-end cameras.
- Windows: optimized the compatibility with multiple USB cameras and microphones to make it easier to enable such devices.
- Windows: optimized the selection policy of cameras and microphones to avoid exceptions in audio/video capturing caused by plugging in and unplugging cameras or microphones.
- Windows and macOS: fixed other bugs.

## v7.6.300 Released on August 26, 2020

**Added**
Windows and macOS: added [setCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDeviceMute), [getCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentMicDeviceMute), [setCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerDeviceMute), and [getCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerDeviceMute) to control PC microphones and speakers.

## v7.5.210 Released on August 11, 2020

**Improvements**
- Windows and macOS: fixed the issue where SDK callbacks were not in sequence.
- Windows and macOS: fixed the issue where switching rendering modes cause crashes. 
- Windows and macOS: fixed the issue where rendering fails for certain resolutions. 
- Windows and macOS: fixed other bugs.

## v7.4.204 Released on July 01, 2020

**Improvements**
- Windows: optimized the acoustic echo cancellation (AEC) effect on Windows
- Windows: improved the compatibility with camera devices on Windows.
- Windows: improved the compatibility with audio devices (mic and speaker) on Windows.
- Windows: fixed the issue where the `UserID` called back by `onPlayAudioFrame` on Windows was incorrect.
- Windows: system audio mixing is supported on 64-bit Windows now.

## v7.2.174 Released on April 20, 2020

**Improvements**
- macOS: fixed the local custom rendering resolution inconsistency issue on macOS.
- Windows: optimized the `getCurrentCameraDevice` logic on Windows to return the first device as the default device when the camera is not used.
- Windows: fixed the issue where the highlighted window was displayed as a gray screen during screen sharing.
- Windows: fixed the issue where the system will occasionally freeze when getting screen share thumbnails on Windows 10.
- Windows and macOS: fixed the issue where the custom stream ID occasionally do not take effect in time when switching roles.
- Windows and macOS: fixed the issue where the encoding parameters of screen sharing did not take effect.
- Windows: fixed the issue where there’s a delay in displaying video image on webrtc for Windows.

## v7.1.157 Released on April 02, 2020

**Added**

[Screen sharing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startScreenCapture) by the [primary stream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoStreamType) is supported.

**Improvements**
- optimized the accessibility of [preset stream mix template](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCTranscodingConfigMode).
- optimized [Stream mix](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMixTranscodingConfig) for an improved success rate.
- optimized screen sharing on Windows.


## v7.0.149 Released on March 19, 2020

**Added**

Added [trtc.d.ts](https://intl.cloud.tencent.com/document/product/647/35141) file TypeScript developers.
