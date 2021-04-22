## Version 8.3 Released on January 15, 2021

**New features**

The business logic of custom capturing is optimized:
- iOS & Android & Mac: optimized the audio module to ensure that when you use [enableCustomAudioCapture](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d) to capture and deliver audio data to the SDK, the SDK can still maintain excellent acoustic echo cancellation (AEC) and active noise suppression (ANS) effect.
- iOS & Android: if you need to continue to increase your own sound effects and sound processing logic based on the TRTC SDK, it will be easier if you use version 8.3. In version 8.3, you can use [setCapturedRawAudioFrameDelegateFormat](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86) and other APIs to set the audio data callback format, including the audio sample rate, the number of sound channels, and the number of sample points, so that you can process audio data in your preferred audio format.
- All platforms: if you need to collect video data by yourself and use the audio module of the TRTC SDK at the same time, lip-sync errors may occur. This is because the SDK's internal timeline has its own control logic. Therefore, we provide the [generateCustomPTS](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee) API. When a video image frame is captured, you can call this API and record the current PTS (timestamp). Then provide this timestamp when you call the [sendCustomVideoData](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831) API later on. In this way, lip sync is ensured.
- Windows: added the support for SOCKS5 proxy addresses in domain name format.

**Issues fixed**
- All platforms: fixed the issue where lip-sync errors of recorded content occasionally occur due to audio data timestamp exceptions.
- Windows: improved the compatibility of window sharing in high-DPI environments.
- Windows: added minimized windows to the shareable window list obtained by users. The thumbnails of minimized windows are their process icons.
- Windows: fixed the issue of unnecessary DXGI occupation after the SDK is started.
- iOS: fixed the ANR issue caused by manual focus setting.
- iOS: fixed the issue of occasional failure to switch between the front and rear cameras.
- iOS: fixed the issue of TXVodPlayer crashes caused by playback deceleration.
- iOS: fixed the issue where playback occasionally switches to the receiver by default after members enter the room.
- iOS & Android: optimized the AEC and ANS effect and made the reverb effect also available to in-ear monitoring.
- Android: fixed the issue of green and blurred screens that occasionally occur during hardware decoding.
- Mac: fixed the issue where, during window sharing with the highlighting feature enabled, the borders of a shared window are highlighted and flash if the window is near the edge of the screen.
- Mac: fixed the issue of black screen when the rendering view is moved.


## Version 8.2 Released on December 23, 2020

**New features**
- iOS & Android: added the support for callback of the mixture of all captured and played back audio data, which makes local audio recording easier.
- Android: the video rendering component TXCloudVideoView allows the `addVideoView(new TextureView(getApplicationContext()))` API to use `TextureView` for local rendering.
- Android: custom rendering callback supports RGBA video data.
- Windows: the local camera can capture and play back remote video stream screenshots. For more information, please see [ITRTCCloud.snapshotVideo](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a3769ecbff6c0c4ee7cc5e4b40aaafe96).
- Windows: enabled the `addExcludedShareWindow` and `addIncludedShareWindow` APIs to exclude and forcibly include user-specified windows respectively during screen sharing for higher flexibility.
- Mac & iOS: enabled `TRTCCloud.snapshotVideo` to take screenshots of video stream images even in custom rendering mode.

**Quality improvement**
- Android: improved the quality of the live streaming code for higher video image definition.
- Windows: improved the AEC algorithm for better AEC effect.

**Issues fixed**
- iOS: fixed the issue of audio playback exceptions that occasionally occur when TXVodPlayer and TRTC are used at the same time.
- Android: fixed the issue of black screen during local rendering caused by custom beauty filter.
- Windows: fixed the issue of occasional failure to exit the current process.


## Version 8.1 Released on December 3, 2020

**New features**
- All platforms: added statistical metrics related to remote video lag to `onStatistics`.
- All platforms: enabled the volume adjustment API `setAudioPlayoutVolume (100-150)` to implement sound gain effect.
- iOS & Android: added the `setLocalVideoProcessListener` API to better support third-party beauty filter SDK integration.
- C#: upgraded to the latest API versions.

**Quality improvement**
- All platforms: optimized the algorithm for processing audio when users wear headphones to deliver better audio quality.
- Android: optimized the audio pre-processing algorithm to reduce the impact of the AEC, ANS, and AGC algorithms on the audio quality.

**Issues fixed**
- iOS: fixed certain occasional crashes caused by applications being forcibly killed.
- Android: fixed the issue of beauty filter effect exceptions that occasionally occur when the video capturing frame rate is high.
- Windows: fixed the issue of crashes that occasionally occur during screen sharing in high-DPI environments.


## Version 8.0 Released on November 13, 2020

**New features**
- All platforms: added unified C++ APIs. For more information, please see `cpp_interface`/[ITRTCCloud.h](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html).
- All platforms: added the support for room IDs of the string type. For more information, please see `TRTCParams.strRoomId`.
- All platforms: added the device management class `TXDeviceManager`.
- All platforms: added the `TRTCCloud.switchRoom` API to allow direct room switching without stopping capturing.
- All platforms: added the `TRTCCloud.startRemoteView` API to start rendering remote video images.
- All platforms: added the `TRTCCloud.stopRemoteView` API to stop rendering remote video images.
- All platforms: added the `TRTCCloud.getDeviceManager` API to get the device management class.
- All platforms: added the `TRTCCloud.startLocalAudio` API to enable local audio capturing and upstreaming.
- All platforms: added the `TRTCCloud.setRemoteRenderParams` API to configure rendering for remote images.
- All platforms: added the `TRTCCloud.setLocalRenderParams` API to configure rendering for local images.

**Optimizations**
- Android: optimized the logic for switching between software and hardware decoding.
- Windows: optimized the audio quality and AEC effect of system loopback audio capturing.
- Windows: optimized the audio device selection logic to reduce the unexpected mute rate.
- Windows: optimized the switching effect in double-talk scenarios.
- All platforms: optimized the instant streaming effect for role switching in manual subscription mode.
- All platforms: optimized the audio receiving logic to improve the audio effect.
- All platforms: optimized the reliability of `sendCustomCmdMsg`.

**Issues fixed**
- iOS: fixed the issue where the calling of `muteLocalVideo` suspends local video rendering.
- iOS: fixed the issue of occasional crashes caused by system component calling during foreground/background switching.
- iOS: fixed the issue where the audio of in-ear monitoring becomes intermittent when sound effects are enabled.
- Android: fixed the issue where the playback of a sound effect does not stop when a call is connected.
- Android: fixed the issue where starting audio capturing occasionally fails.
- Windows: fixed the issue of occasional black screen during local video rendering.
- Windows: fixed the issue where crashes may occur when processes exit.
- Windows: improved the support for Bluetooth earphones and fixed the issue where Bluetooth earphones are muted.
- Windows: fixed the issue where focus preemption occurs after screen sharing stops.
- All platforms: fixed the exception that occurs when statistics on the packet loss rate are collected during status callback.



## Version 7.9 Released on October 27, 2020
**New features**
- Mac: added the support for users to filter specified windows during screen sharing for better privacy protection.
- Windows: added the support for users to configure the stroke color and border width for the "Sharing" prompt border during screen sharing.
- Windows: added the support for users to enable the high performance mode when sharing the entire desktop.
- All platforms: added the custom encryption feature to allow users to perform secondary processing on encoded audio/video data through exposed C APIs.
- All platforms: added the audio lag information callbacks `audioTotalBlockTime` and `audioBlockRate` to `TRTCRemoteStatistics`.

**Optimizations**
- iOS: improved the startup speed of the audio module to enable the first audio frame to be captured and sent faster.
- Windows: optimized the AEC algorithm for system audio loopback to deliver better AEC capability when `SystemLoopback` is enabled.
- Windows: optimized the anti-covering capability of screen capturing during screen sharing to allow users to configure filter windows.
- Android: optimized the in-ear monitoring effect for most Android models to reduce the in-ear monitoring delay to a more comfortable level.
- Android: further optimized one-to-one delay in `Music` mode (specified in `startLocalAudio`).
- All platforms: optimized the sound smoothness during the switching between the audience and anchor roles in manual subscription mode.
- All platforms: improved the audio/video call performance in weak network environments to deliver better audio/video smoothness.

**Issues fixed**
- iOS: fixed the occasional failure to render video images in certain scenarios.
- iOS: fixed the issue where noise occasionally occurs when users wear earphones while the default sound quality is used.
- iOS: fixed certain known memory leaks.
- iOS: fixed the issue where crashes occasionally occur after ReplayKit screencap ends.
- iOS: fixed the compilation issue in simulator environments.
- Android: fixed the issue where lip-sync errors occasionally occur on certain phones after an app is switched to the background for a long time and then switched back to the foreground.
- Android: fixed the issue where the microphone is not released after users switch to the background.
- Android: fixed the issue where certain internal OpenGL resources of the SDK are not released in time.
- Windows: fixed the occasional noise problem in a few scenarios.
- All platforms: fixed certain occasional crashes to improve the SDK stability.

## Version 7.8 Released on September 29, 2020
**New features**
- Mac: added the callback of system volume changes. For more information, please see [TRTCCloudDelegate.onAudioDevicePlayoutVolumeChanged](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#af24c0f0258e83ab644e242ee0d01277f).
- Windows: added the feature for users to specify areas across screens for screen sharing.
- Windows: added the support for users to filter specified windows for anti-covering during window sharing. For more information, please see [TRTCCloud.addExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae5141a9331c3675f17fbdc922f376b06) and [TRTCCloud.removeExcludedShareWindow](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a08504ce347b593c0191904611da5cfd2).
- Windows: added the callback of system volume changes. For more information, please see [ITRTCCloudCallback.onAudioDevicePlayoutVolumeChanged](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a39cf2644243dceaccd82933f11f4db12).

**Optimizations**
- iOS: added support for using TXVodPlayer and TRTC together as well as AEC.
- iOS & Mac: added support for the feature of pushing a video mute image. For more information, please see [TRTCCloud.setVideoMuteImage](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2).
- Android: added support for the feature of pushing a video mute image. For more information, please see [TRTCCloud.setVideoMuteImage](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d).
- Android: optimized the audio routing policy to allow audio to be played back only from earphones when users wear earphones.
- Android: allows low-delay capturing and playback in certain systems to reduce call delay on Android.
- Android: added support for using TXVodPlayer and TRTC together as well as AEC.
- Windows: compatible with the virtual camera emulator e2eSoft VCam.
- Windows: allows users to call `startLocalPreview` and `startCameraDeviceTest` at the same time.
- Windows: allows users to call `startLocalPreview` to enable local preview while using the primary stream for screen sharing.
- Windows: fixed the issue of long audio delay caused by SDK internal playback buffer.
- Windows: optimized the audio enablement logic to avoid occupying the microphone in playback-only mode.



**Issues fixed**
- iOS: fixed the low playback volume issue of iPhone SE.
- iOS: fixed the issue where crashes occur when `muteRemoteAudio` is called in `TRTCCloud.createSubCloud`.
- iOS: fixed rendering crashes that occasionally occur.
- iOS: fixed the issue where video rendering on certain iPad devices occasionally causes the main thread to crash during foreground/background switching.
- iOS: fixed known memory leaks.
- iOS: fixed the issue where iOS14 prompts "would like to find and connect to devices on your local network".
- Mac: fixed the issue where `getCurrentCameraDevice` always returns `nil`.
- Mac: fixed the issue where certain USB cameras cannot be enabled.
- Mac: fixed the issue where crashes occur when the area size specified for screen sharing is `0`.
- Android: fixed the issue where Android 5.0 devices crash when the `READ_PHONE_STATE` permission is not specified.
- Android: fixed the issue where audio capturing and playback exceptions occur after Bluetooth earphones are disconnected and then connected again.
- Android: fixed known crash issues.
- Windows: fixed the issue where the 64-bit SDK crashes when screen sharing is repeatedly enabled and then disabled.
- Windows: fixed the issue where crashes occur when certain systems use OpenGL.


## Version 7.7 Released on September 8, 2020

**Optimizations**

- All platforms: improved the instant streaming speed of the substream (screen sharing).
- iOS: optimized the internal thread model to improve the operation stability in scenarios with concurrent playback using more than 30 channels.
- iOS & Android: improved the performance of the audio module and reduced the capturing delay of the first audio frame.
- iOS & Android: improved the volume and sound effect performance when TXVodPlayer and TRTC are used at the same time.
- iOS & Android: added the support for sound effect and the background music files in WAV audio format.
- Windows: optimized the issue where the CPU utilization is too high on some low-end cameras.
- Windows: optimized the compatibility with multiple USB cameras and microphones to make it easier to enable such devices.
- Windows: optimized the selection policy of cameras and microphones to avoid exceptions in audio/video capturing caused by plugging in and unplugging cameras or microphones.

**Issues fixed**

- All platforms: fixed the issue where playback exceptions occasionally occur when the `muteLocalVideo` and `muteLocalAudio` APIs are called in weak network environments.
- iOS: fixed the issue where sound effect playback may fail on low-end iPhone or iPad devices.
- iOS: fixed the issue where screen images shared by iPad Pro get distorted.
- iOS: fixed the issue where, during in-app screen sharing, the screen capturing permission request continues to pop up for a few times after being rejected by users.
- Windows: fixed the issue where onExitRoom fails to call back room exit event notifications after laptops or desktops stay in the sleep mode for a long time.
- Windows: fixed the issue where, in `Music` mode, echo leaks occur after [stopSystemAudioLoopback](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23) is enabled.
- Windows: fixed the issue where the player end is occasionally muted when `enterRoom` and `exitRoom` are frequently and quickly called to enter and exit rooms respectively.
- Windows: fixed the issue of SDK compatibility with Visual Studio 2010 project compilation.
- Windows: fixed the issue where the `onUserVideoAvailable` event callback is repeatedly received in manual subscription mode ([setDefaultStreamRecvMode(false,false)](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5)).


## Version 7.6 Released on August 21, 2020
**New features**

- Windows: added the [updateLocalView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ae5211a2739df8d8ec6017559b3aa0299) and [updateRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8c8247cbc679ea144ffb393b6b940c9e) APIs to improve user experience in adjusting HWND rendering windows in real time.
- Windows: added the [getCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f) API to get whether the current Windows PC is muted.
- Windows: added the [setCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f) API to set global mute for the current Windows PC.
- Mac: added the [updateLocalView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) and [updateRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87) APIs to optimize user experience in adjusting the view rendering area in real time.
- Mac: added the [getCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a6ba78519e9c98c1eecd365154882d53f) API to get whether the current Mac computer is muted.
- Mac: added the [setCurrentMicDeviceMute](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a88569e62fe75b7ea98cc012169f22bfe) API to set global mute for the current Mac computer.
- iOS: added the [updateLocalView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb) and [updateRemoteView](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87) APIs to optimize user experience in adjusting the view rendering area in real time.
- iOS: for `TRTCCloudDelegate`, added the [onCapturedRawAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#aeaeaf9e7091c75e1a072d576a57d7f5c) callback function and changed the names of a few other callback functions to [onLocalProcessedAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a73a3e7de3c5c340957f119bb0f8744b0), [onRemoteUserAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#aa392c17c27bae1505f148bf541b7746a), and [onMixedPlayAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e).
- Android: for `TRTCCloudListener`, added the [onCapturedRawAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e) callback function and changed the names of a few other callback functions to [onLocalProcessedAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46), [onRemoteUserAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902), and [onMixedPlayAudioFrame](http://doc.qcloudtrtc.com/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7).

**Optimizations**

- All platforms: optimized the protocol policy of `EnterRoom` to improve the speed and success rate of room entry.
- All platforms: optimized the overall performance consumption and lag issues when a large number of audio channels are subscribed at the same time.
- Mac: added the support for users to specify areas for screen sharing.

**Issues fixed**

- All platforms: fixed the issue where the SDK does not trigger `onEnterRoom` callback when users enter the same room without exiting.
- All platforms: fixed a few internal bugs that may occasionally cause a black screen.
- All platforms: fixed the issue where the screen sharing image cannot be displayed properly when `startRemoteSubStreamView` is called early.
- Windows: fixed a few known handle and GDI leaks.
- Windows: fixed multiple known crash issues.
- Windows: fixed the issue where devices are not automatically started after cameras and microphones are disconnected and then reconnected.
- iOS: fixed the issue where iOS 10 crashes when the background music API passes in file paths of particular rules.
- Android: fixed the issue where the player end is occasionally muted when `enterRoom` and `exitRoom` are frequently and quickly called to enter and exit rooms respectively.
- Android: fixed the issue where black screens occasionally occur during screencap pushes.


## Version 7.5 Released on July 31, 2020

**New features**

- Added the support for dual-stack IPv6 and IPv6-only.
- Added the capability to pull when users enter multiple rooms, supporting super small classes.
- Added the feature of setting the background image (for regulatory purposes, images must first be uploaded through the TRTC console) to MCU On-Cloud MixTranscoding.
- Added the `A+B=>C` and `A+B=>A` modes to MCU On-Cloud MixTranscoding.
- Added the playback buffer time field `jitterBufferDelay` to the real-time status callback function `onStatistics`.

**Optimizations**

- Reduced the delay of end-to-end co-anchoring calls by 40%, compared with that in version 7.4.
- Reduced the in-ear monitoring delay of phones and added the feature for setting sound effects such as voice changing and reverb effects for in-ear monitoring.
- Optimized the player-end network jitter evaluation algorithm to reduce the playback delay.
- Reduced the delay of end-to-end co-anchoring calls for the Android SDK.
- Further reduced the in-ear monitoring delay.
- Optimized the issue where playback view switching causes a black screen.

**Issues fixed**

- Fixed the issue where playback does not take effect after `playBGM` and `pauseBGM` are consecutively called in a function.
- Fixed the issue where `onEnterRoom` callback can still be received occasionally after room exit.
- Fixed the issue where certain models cannot recover after ultra-low resolution encoding fails. 

## Version 7.4 Released on June 24, 2020 

**Optimizations**

Added support for setting the volume of in-ear monitoring.

**Issues fixed**

- Fixed the issue where the local video image blinks once during landscape/portrait mode switching on Android.
- Fixed the issue where custom videos cannot be properly encoded when sent on certain Android phones.
- Fixed the occasional crash of audio packet processing.



## Version 7.3 Released on June 1, 2020

**New features**

- Added the new sound effect management API `TXAudioEffectManager` to support more flexible and diverse sound effect capabilities while retaining the compatibility with legacy APIs.
- Added the `minVideoBitrate` option to the video encoding parameter `setVideoEncoderParam`. This option is recommended for live streaming users who have a high requirement for image quality.

**Optimizations**

- Added transient noise reduction for audio, which can be enabled through `setAudioQuality(TRTCAudioQualitySpeech)`.
- Added the support for sound effect files consisting of packaged assets.
- Improved the local video definition.
- Added the support for the texture mode for custom rendering on the player end to reduce performance overhead.
- Optimized the selection logic of camera capturing resolution to improve the visual effect.
- Optimized the echo processing effect.
- Added the support for the full-linkage 128 Kbps high-quality stereo sound, which can be set through the `setAudioQuality(TRTCAudioQualityMusic)` API.
- Added the support for the `SPEECH` audio mode, which provides a better ANS capability for audio conferencing calls. This audio mode can be set through the `setAudioQuality(TRTCAudioQualitySpeech)` API.
- Added the support for concurrent playback of multiple background music streams to support karaoke scenarios where the vocal and accompaniment are separated. Loop playback of the background music is also supported now.
- You can now call `muteLocalVideo` before `startLocalPreview` to implement the effect of "only preview but no push". You can also call `startLocalPreview` before `enterRoom` to implement this effect.

**Issues fixed**

- Fixed the occasional crash of OpenGL context inside the SDK during custom video capture.
- Fixed the issue where the callback for `setLocalVideoRenderListener` custom rendering is not triggered before room entry.
- Fixed the issue where the video image in the player gets upside down during front/rear camera switch in landscape mode.
- Fixed the low-probability issue where the player screen gets corrupted after room entry if `startLocalPreview` is called first.
- Fixed the occasional crash of hardware encoder.
- Fixed the occasional issue with intermittent local audio recording.
- Fixed the issue where the player cannot automatically play back audio/video if a kill or crash occurs when the push is paused (`muteLocalVideo` or `muteLocalAudio`).



## Version 7.2 Released on April 16, 2020 

**New features**

Added the support for mobile screen sharing on Android, which is suitable for screencap live streaming on the mobile client.

**Optimizations**

- Optimized the performance in call scenarios on low and mid-end Android phones to improve the audio experience.
- Optimized visual effect APIs such as filter and green screen and aggregated them into the `TXCBeautyManager` class for a unified call method.

**Issues fixed**

Fixed the issue where the custom stream ID occasionally does not take effect in time during role switching.



## Version 7.1 Released on March 27, 2020 

**Optimizations**

- The C++ STL basic library is compiled in a fully static manner.
- ANS and AGC are enabled by default for the call volume to improve the audio quality in call mode.
- Fixed the usability of the preset stream mixing template.
- Optimized stream mixing for a higher success rate.

**Issues fixed**

- Fixed the issue where all audio processing values become zero when AGC is enabled/disabled frequently during room entry.
- Fixed the issue where the speed test slows down response to calls of other APIs.
- Fixed the issue where the upstream volume doubles with noise when the process is interrupted by a phone call.
- Fixed the issue of auto-relayed push upon room entry.



## Version 7.0 Released on March 9, 2020 

- Optimized the 3A enabling policy.
- Improved the usability of MCU On-Cloud MixTranscoding.
- Improved the audio smoothness in weak network environments.
- Fixed the issue of OOM caused by repeated consecutive room entry/exit.



## Version 6.9 Released on January 14, 2020 

**New features**

- Added the support for Android 10.0.
- Added the `snapshotVideo()` API to screencap local and remote video images.
- Added the `pauseAudioEffect` and `resumeAudioEffect` APIs to pause and resume a sound effect respectively.
- Added the `setBGMPlayoutVolume` and `setBGMPublishVolume` APIs to set the local playback volume and push/audio mix volume respectively.
- Added the `setRemoteSubStreamViewRotation` API to adjust the rendering rotation angle of substream video playback.
- Added the global volume type mode `setSystemVolumeType(TRTCSystemVolumeTypeVOIP)`, i.e., the call volume is always used, which is mainly used to solve the issue of capturing switching between the Bluetooth earphone and built-in mic.
- Added the `streamId` attribute to the `TRTCParams` parameter for `enterRoom` to set the live stream ID in CDN, which makes it easier for you to bind the live stream to CDN.
- Added the `cloudRecordFileName` attribute to the `TRTCParams` parameter for `enterRoom` to set the on-cloud recording filename for live streaming.
- Added the `TRTCAppSceneAudioCall` scenario, which can be set during `enterRoom`. In this scenario, the TRTC SDK is comprehensively optimized for audio calls.
- Added the `TRTCAppSceneVoiceChatRoom` scenario, which can be set during `enterRoom` to enable the optimizations made by the TRTC SDK for interactive voice chat room scenarios.

**Optimizations**

- Improved the capability of avoiding an interrupted video stream's impact on the recording service, making remote recording files more complete.
- Alleviated the lip-sync error during hardware decoding on certain models.
- Enabled video images to be captured at a 1080p high resolution, delivering a higher definition during watch of mobile live streams on PCs.
- Simplified the error codes for room entry.
- Fixed the occasional issue of slow instant streaming.

**Issues fixed**

- Fixed the occasional crash of the HTTP component.
- Fixed the occasional issue where there is no callback for sound effect playback completion.
- Fixed the occasional issue where the system cannot be recovered from room entry failures.



## Version 6.8 Released on November 15, 2019 

**New features**

- Added the in-ear monitoring capability.
- Enabled users to specify not to automatically pull during room entry.
- Added the `getBeautyManager` API to aggregate beauty filter, image retouching, and animated effect APIs.
- Added image retouching features, such as skin beautifying, eye brightening, teeth whitening, wrinkle removal, and eye bag removal, to the Enterprise Edition.
- Added the `onRemoteUserEnterRoom` and `onRemoteUserLeaveRoom` callbacks to send the room entry and exit notifications of mic-off anchors respectively.

**Optimizations**

- Optimized the PTS generation mechanism.
- Enabled the optimal access point to be automatically selected after network switching.
- Enabled the advance call of `startRemoteView`.

**Issues fixed**

Fixed known crashes.



## Version 6.7 Released on September 30, 2019 

**New features**

- Added permission acquisition configuration for AAR packaging.
- Added CPU usage evaluation on Android 8.0 and above.

**Optimizations**

- Relayed push is faster now.
- Users can now adjust their own playback volume separately.

## Version 6.6 Released on August 2, 2019 

**New features**

- Added the local audio recording feature.
- Added callback APIs for sending the first audio or video frame.
- Added the system volume type setting API.
- Added sound effect APIs, which can be used to play back short sound effects.
- Added the feature of modifying the data output by the custom audio callback API.

**Optimizations**

- Optimized the room entry feature for faster speed and higher success rate.
- Added the support for the remote video muting API.
- Unified the room entry error codes, which are called back through `onEnterRoom`. If the value of `result` is smaller than 0, it indicates a room entry error.
- Optimized the demo to support low-latency big rooms.
- Added the volume setting and volume callback APIs for the player.
- Added the support for local rendering for custom video sending.
- Added the support for 1080p for custom video capturing and sending.
- Added the support for the `SurfaceView` method for local and remote rendering.

**Issues fixed**

- Fixed the issue of relayed push stream mixing.
- Fixed the issue of incorrect local preview angle.



## Version 6.5 Released on June 12, 2019 

**New features**

Added the "low-latency big room" feature to the live streaming mode (TRTCAppSceneLIVE):

- A UDP protocol specially optimized for audio/video is used to deliver an excellent performance even in weak network environments.
- The average watch latency is about 1 second, which can improve the activeness in anchor-viewer interaction.
- Up to 100,000 users can now enter the same room.

**Optimizations**

- Fixed the issue of lip-sync error in weak network environments.
- Optimized the `onStatistics` status callback to call back only existing streams.
- Optimized the playback buffer logic for live streaming `TXLivePlayer` to reduce lagging.
- Increased the recovery speed when `muteLocalVideo` is called first and then the video image on the playback client is canceled.
- Optimized the QoE algorithm in high-latency network environments with a high packet loss rate to improve the performance in weak network environments.
- Optimized the decoder performance and fixed the increasing delay on extremely-low-end Android phones.
- Optimized the volume evaluation algorithm (enableAudioVolumeEvaluation) to make the evaluation result more accurate.
- Optimized the QoE algorithm in video call mode (TRTCAppSceneVideoCall) to further improve the smoothness of one-to-one calls in weak network environments.

  

**Issues fixed**

- Fixed the occasional issue of no callback for `enterRoom`.
- Fixed the issue where no sound is played when audio capturing is disabled.
- Fixed the issue where the screen turns green after the local rendering view is removed and added again.
- Fixed the issue where the remote video image is called back for only 10 times when the resolution is 540p or above during custom rendering callback (`setRemoteVideoRenderDelegate`).



## Version 6.4 Released on April 25, 2019 

**New features**

- Added APIs for mirroring local display and mirroring encoder output.
- Added the setting callback function for the `setMixTranscodingConfig` API.
- Added the eye enlarging, face slimming, chin slimming, and animated widget features to the Enterprise Edition.

**Optimizations**

- Improved the smoothness in weak network environments.
- Optimized the volume callback algorithm to make the volume callback value more reasonable.
- Added the support for specifying data frame timestamps externally for sending custom audio and video data.
- Enhanced the `setMixTranscodingConfig` API to support the `roomID` parameter for cross-room co-anchoring stream mixing.
- Enhanced the `setMixTranscodingConfig` API to support the `pureAudio` parameter for audio stream mixing and recording in pure audio call scenarios.
- Improved the 720p video decoding performance on low-end Android devices.

**Issues fixed**
- Fixed the issue where hands-free mode switching does not work.
- Fixed the issue where the live streaming (TXLivePlayer) latency might irreversibly become higher.
- Fixed the issue where `setVideoEncoderRotation` does not work in live streaming scenarios.
- Fixed the issue where there is no callback for errors after the mic permission is denied on Android.
- Fixed the issue of pop-up after the demo is opened on Android 9.0.
- Fixed the issue where the volume adjustment buttons cannot adjust the viewer volume.



## Version 6.3 Released on April 2, 2019 

**New features**

- Android 64-bit is supported now.
- Added a custom video capturing API: TRTCCloud > sendCustomVideoData.
- Added a custom audio capturing API: TRTCCloud > sendCustomAudioData.
- Added custom video rendering APIs: TRTCCloud > setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate.
- Added a custom audio data callback API: TRTCCloud > setAudioFrameDelegate, which supports the following:
  - Return the mic capturing data: TRTCAudioFrameDelegate > onCapturedAudioFrame.
  - Return the audio data of each remote user: TRTCAudioFrameDelegate > onPlayAudioFrame.
  - Return the mixed audio data played back through the speaker: TRTCAudioFrameDelegate > onMixedPlayAudioFrame.





## Version 6.2 Released on March 8, 2019 

**New features**

- Added the filter level setting API `setFilterConcentration()`.
- Added the `sendSEIMsg()` API to send custom messages through the SEI header information in video frames, which is generally used to insert timestamp information into video streams.
- Added the cross-room call feature `connectOtherRoom`, that is, two existing TRTC rooms can communicate with each other, which can be used in anchor competition across rooms.



**Optimizations**

- Improved the CPU utilization and stability.
- Improved the video image definition in weak network environments.
- Canceled the multi-instance capability of `TRTCCloud` and changed the creation mode to singleton mode, which help avoid compromised user experience due to network resource preemption among multiple `TRTCCloud` instances.

**Issues fixed**

Relayed push in pure audio call scenarios (such as werewolf) is fixed, which needs to be used together with the `bussInfo` field in `TRTCParam`.



## Version 6.1 Released on January 31, 2019 

**Optimizations**

- Screen sharing streams can now be watched.
- Custom video data can now be sent.
- The implementation of CDN relayed push and stream mix is optimized.
- Live streaming and video calls are distinguished between upon room entry.
- The stability is improved, and some occasional crashes are fixed.
- Traffic throttling is optimized to improve the performance in weak network environments.



## Version 6.0 Released on January 18, 2019 

**Optimizations**

- Updated the architecture to the LiteAV kernel.
- Adopted a new QoS algorithm to reduce lagging and improve smoothness.
- Adopted a new audio module to deeply optimize the audio quality in various network conditions.
- Added the support for primary stream/substream encoding (we recommend you enable it only on Windows and macOS devices).
- Added the support for CDN relayed push and stream mixing.





















