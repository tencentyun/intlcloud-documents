
Tencent Cloud’s media SDKs (RT-Cube) include the TRTC SDK, MLVB SDK, Player SDK, and UGSV SDK. You can choose one of the SDKs to build your application or use the All-in-One SDK.

## Version 10.8 Released on October 27, 2022


### MLVB


#### New features

Android: Added support for sending the system audio when publishing streams using V2TXLivePusher.

#### Improvements

- All platforms: Increased the success rate of playback in the LEB scenario.
- Android: Improved instant streaming performance.

#### Bug fixing

- All platforms: Fixed the issue where, when using V2TXLivePusher to publish streams, the 1101 warning code is not returned under poor network conditions.
- All platforms: Fixed the issue where manual focus fails to work with TXLivePusher\V2TXLivePushe.

### UGSV


#### Improvements

Android & iOS: Reduced stuttering in the playback of background music during editing.

#### Bug fixing

- Android: Fixed the occasional no audio issue if background music is changed multiple times during editing.
- Android: Fixed the black screen issue for image transitions on HUAWEI Mate 50.
- iOS: Fixed the issue where the video bitrate of the generated video increases in iOS 14.

### TRTC


#### New features

All platforms: Added the DJ scratch effect and improved the karaoke experience. For details, see `TXAudioEffectManager.setMusicScratchSpeedRate`.

#### Improvements

Android: Sped up video decoding, which reduces the time to first frame to as short as 50 ms.
All platforms: Improved the accuracy of NTP time. For details, see `TXLiveBase.updateNetworkTime`.

#### Bug fixing

- All platforms: Fixed the occasional issue where, when the streams of a room are mixed and pushed to another TRTC room that does not have upstream audio or video, playback fails and callbacks stop working.
- All platforms: Fixed the occasional issue where, after an audience member changes their role upon room entry, they fail to publish audio and video due to network type change.
- All platforms: Fixed the issue where, after a disconnection, audio quality cannot be changed during reconnection.
- All platforms: Fixed the issue where, after a disconnection, there is sometimes no audio in the published stream during reconnection.
- Android & iOS: Fixed the issue where `muteRemoteVideoStream` removes the last video frame.

### Player


#### Improvements

- Android & iOS: Added the `VOD_PLAY_EVT_LOOP_ONCE_COMPLETE` event, which indicates that one loop of the playlist is finished.
- Android: Fixed the issue where `NetworkInfo.getExtraInfo` is called twice when the SDK is started, improving compliance.

#### Bug fixing

- Android & iOS: Fixed the issue where videos encrypted using VOD’s private protocol fail to be played in certain scenarios.
- Android & iOS: Fixed failure to play some GZIP-compressed videos.
- Android & iOS: Fixed the issue where the duration indicated by the progress bar does not match the actual video length after playback ends.
- iOS: Fixed the issue where, when a video is played by `appid` and `fileid` using the v2 protocol, an error occurs when the SDK gets the original video URL.

## Version 10.7 Released on September 20, 2022


### MLVB


#### New features

iOS & Android: The `startPlay` API of TXLivePlayer\V2TXLivePlayer was renamed `startLivePlay`, and license verification is required. For how to get a license, see “Video Playback License.”

#### Improvements

All platforms: Optimized the buffering policy of `AudioJitterBuffer`.

#### Bug fixing

- All platforms: Fixed the issue where playback of HEv2 audio using V2TXLivePlayer is abnormal in the LEB scenario.
- All platforms: Fixed the issue where, when an IP address is used to publish RTMP streams with TXLivePusher\V2TXLivePusher, publishing fails.
- Windows: Fixed compilation failure on C# because the `V2TXLivePlayerStatistics` constructor is not found.
- iOS: Fixed the issue of low capturing volume on some iPad devices.
- Android: Fixed the occasional issue where Bluetooth earphones are connected, but audio is played from the device’s speaker.

### UGSV


#### Improvements

Android & iOS: Optimized the shooting module to solve the no audio issue, enhancing user experience.

#### Bug fixing

- Android: Fixed the issue where the SDK crashes when the user exits during video preprocessing.
- Android: Fixed failure to apply stickers if a video is not previewed.
- Android: Fixed failure to apply effects when a video is played backwards.
- Android: Fixed the issue where the video processing callback configured for video editing fails to work.
- iOS: Fixed the issue where audio and video are out of sync in saved videos.
- iOS: Fixed failure to splice videos without audio.
- Android & iOS: Fixed the issue of noise in case of repeated shooting.

### TRTC


#### New features

- All platforms: You can now independently adjust the audio volume of each stream in On-Cloud MixTranscoding. For details, see `TRTCMixUser.soundLevel`.
- All platforms: Added the `onRemoteAudioStatusUpdated` API, which is used to monitor the audio status of remote streams.

#### Improvements

- All platforms: Upgraded the encoding engine, improving the video quality of screen sharing streams.
- All platforms: Improved rate control for encoding under poor network conditions.

#### Bug fixing

- iOS: Fixed the issue of low capturing volume on some iPad devices.
- Android: Fixed the occasional issue where Bluetooth earphones are connected, but audio is played from the device’s speaker.
- All platforms: Fixed the issue where the SDK occasionally crashes if a user enters and leaves the room repeatedly.

### Player


#### Improvements

- Android & iOS: The `startPlay` API for VOD playback was renamed `startVodPlay`.
- Android & iOS: The `startPlay` API for live playback was renamed `startLivePlay`.
- iOS: Fixed the issue where, if the player is switched to the foreground after remaining in the background for a long time, playback fails.
- Android: Fixed failure to play some videos in old Android versions.




## Version 10.6 Released on September 9, 2022

### MLVB

#### New features

iOS & Android & macOS: TXLivePlayer and V2TXLivePlayer in the All-in-One SDK supported HLS playback, adaptive bitrate playback, and seamless bitrate change.

#### Improvements

- All platforms: Fixed the issue where audio volume is low in the music mode.
- Android & iOS: Fixed the issue of audio loss when call volume is used.
- Android: Fixed occasional echoes.

#### Bug fixing

- All platforms: Fixed the issue where, in the LEB scenario, after the internet disconnects and reconnects, V2TXLivePlayer fails to reconnect immediately.
- All platforms: Fixed the issue where, in the LEB scenario, when a UDP channel fails to be established, V2TXLivePlayer is not able to switch to a TCP channel.
- macOS: Fixed the issue where echo cancellation occasionally fails to work after the mic is changed.

### UGSV

#### Bug fixing
- Android: Short videos are now encoded using the High Profile.
- Android: A message is now shown if the format of a background music file is not supported.
- iOS: Fixed the issue of noise when videos are played in slow motion.

### TRTC
#### Improvements

- All platforms: Sped up room entry in IPv6 networks.
- All platforms: Improved the audio recovery performance and audio-to-video synchronization under bad network conditions, enhancing user experience.
- All platforms: Improved the ability to maintain connection under poor network conditions, reducing disconnections.
- All platforms: Fixed the issue where the volume is low in the music mode (which is specified when `startLocalAudio` is called).
- macOS: Improved call experiences when Bluetooth earphones are used, reducing noise and delivering clearer audio.
- Android: Supported stereo audio capturing for more devices.
- Android: Fixed occasional echoes, improving call experience.

#### Bug fixing
- Android & iOS: Fixed the issue of audio loss in the speech mode (which is specified when `startLocalAudio` is called).
- macOS: Fixed the issue where echo cancellation occasionally fails to work after the mic is changed.

### Player

#### Improvements

- Android & iOS: Added callbacks of image sprites, URLs, and other information for file ID playback.
- Android & iOS: Reduced the SDK package size.

#### Bug fixing
iOS: Fixed the issue where, in some scenarios, after videos encrypted using VOD’s private protocol are downloaded, playback fails.

## All-in-One SDK 10.5 Released on August 24, 2022
### MLVB
#### Improvements
- Android: Optimized memory management for video decoding, preventing the accumulation of memory leaks.
- Windows: Optimized noise suppression for the built-in mic, especially in the music mode.
- macOS: Fixed the frequent noise issue when the mic is turned on.

#### Bug fixing
- All platforms: Fixed the issue where, in the LEB scenario with V2TXLivePlayer, SEI messages are sometimes not received.
- All platforms: Fixed the issue where, in the LEB scenario with V2TXLivePlayer, audio is missing because the timestamp moves backward.

### UGSV
#### Bug fixing
- Android: Fixed the green screen issue in videos made from pictures on HarmonyOS.
- Android: Fixed the issue of incorrect length for edited videos.
- Android: Fixed failure to play or re-encode videos with multiple audio tracks.
- Android: Fixed the issue where the “rock light” effect is applied only once during the selected time period.
- Android & iOS: Fixed the issue where, after a video segment is deleted during shooting, the playback progress of the background music does not match.

### TRTC

#### Improvements

- All platforms: Optimized the QoS control policy, enhancing user experience under poor network conditions.
- iOS & Android: Reduced end-to-end latency and improved in-ear monitoring experience.
- Android: Optimized memory management for video decoding, preventing the accumulation of memory leaks.
- Windows: Optimized noise suppression for the built-in mic, especially in the music mode.
- macOS: Fixed the frequent noise issue when the mic is turned on.

#### Bug fixing
All platforms: Fixed occasional errors for the [OnUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) and [OnUserAudioAvailable](https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudListener__android.html#ac1a0222f5b3e56176151eefe851deb05) callbacks when a user enters and leaves different rooms consecutively.

### Player

#### Bug fixing
Android & iOS: Fixed failure to play URLs that do not include video formats at the end.

## All-in-One SDK 10.4 Released on July 25, 2022
### MLVB
#### New features
iOS & Android: V2TXLivePlayer can now freeze the last frame after playback ends.

#### Improvements
- All platforms: Fixed the issue of high memory usage when TXLivePlayer\V2TXLivePlayer plays FLV streams.
- Android: Fixed occasional playback stutter with TXLivePlayer\V2TXLivePlayer.
- Android: Improved the compatibility of low-latency in-ear monitoring and dual-channel capturing.
- Android: Optimized the policy for switching from hardware to software decoding.
- iOS: Fixed the issue of low capturing volume on iPad.

#### Bug fixing
Android: Fixed the issue where TXLivePlayer\V2TXLivePlayer occasionally switches to software decoding when playing streams.

### UGSV

#### Improvements
Android: Added the `setBGMLoop` API for video editing.

#### Bug fixing
- Android: Fixed the issue of `setWaterMark` not working.
- Android: Fixed the issue where, when videos are previewed, TXVideoEditor fails to use the specified rendering mode.

### TRTC
#### New features
- iOS & Android: Added support for the RGBA32 format for custom capturing. For details, see `sendCustomVideoData`.
- Windows & macOS: Added support for watermark preview after configuration. For details, see `setWaterMark`.

#### Improvements
- Android: Improved the compatibility of low-latency in-ear monitoring and dual-channel capturing.
- Android: Optimized the policy for switching from hardware to software decoding.
- iOS: Fixed the issue of low capturing volume on iPad.

#### Bug fixing
- All platforms: Fixed occasional room entry/exit callback errors.
- Windows: Fixed the issue where, after the window shared changes, the new window is not displayed in full.

### Player
#### Improvements
Android & iOS: Added support for adaptive bitrate HLS playback.

#### Bug fixing
- Android: Fixed abnormal intervals for the `onNetStatus` callback and the progress callback.
- Android: Fixed the null pointer exception caused by failure to call `setConfig`.
- iOS: Fixed the stuttering issue when videos are replayed in some scenarios.

## All-in-One SDK 10.3 Released on July 8, 2022

### MLVB

**New features:**
All platforms: TXLivePlayer\V2TXLivePlayer added support for HLS playback.

**Improvement:**
- All platforms: Improved audio quality in the music mode.
- All platforms: Optimized the SEI parsing logic. TXLivePlayer\V2TXLivePlayer can parse some non-standard SEI messages now.
- All platforms: Fixed the issue of audio and video being out of sync as a result of the timestamp moving backward when TXLivePlayer\V2TXLivePlayer plays FLV or RTMP streams.

**Bug fixing:**
- All platforms: Fixed the abnormal audio that occurs when TXLivePlayer\V2TXLivePlayer plays some AAC-HEv2 streams in the LEB scenario.
- All platforms: Fixed incorrect cache calculation with TXLivePlayer.

### UGSV

**Bug fixing:**
- Android: Fixed the issue of `setZoom` not working during video shooting.
- Android: Fixed failure to shoot videos with Samsung Galaxy S22.
- iOS: Fixed failure to trigger the callback for custom video pre-processing.

### TRTC

**New features:**
- Windows: Added support for recording live streaming sessions and audio/video calls to local storage. For details, see the description of `ITXLiteAVLocalRecord`.
- Windows & macOS: Added a parameter to `startMicDeviceTest`, which allows you to specify whether to play the audio captured during mic testing. For details, see the description of `startMicDeviceTest`.

**Improvement:** 
All platforms: Improved audio quality in the music mode.

**Bug fixing:**
- All platforms: Fixed occasional errors for the user list callback.
- Windows: Fixed the issue where videos sometimes freeze during playback.
- Windows: Fixed occasional video playback failure.
- Windows: Fixed the echo issue for custom audio capturing.

### Player

**New features:**
iOS: Added support for picture-in-picture playback.

**Bug fixing:**
- Android: Fixed the issue where, when hardware decoding is used and a video playlist is played in the background, the player fails to automatically play the next video when one video is finished.
- Android & iOS: Fixed failure to trigger the callback when seeking is completed.

## All-in-One SDK 10.2 Released on June 26, 2022

### MLVB

**New features:**

- All platforms: Added support for license authentication for playback with TXLivePlayer\V2TXLivePlayer.
- All platforms: Added support for HTTP header configuration for FLV playback with V2TXLivePlayer.
- All platforms: Allowed changing audio encoding parameters dynamically when pushing RTMP streams with TXLivePusher\V2TXLivePusher.

**Improvement:** 

- All platforms: Optimized the adaptive bitrate API of V2TXLivePlayer for LEB.
- All platforms: Fixed the issue where V2TXLivePlayer takes a long time to reconnect in the LEB scenario.
- All platforms: Fixed the issue of small local cache size when TXLivePlayer\V2TXLivePlayer plays FLV or RTMP streams.
- Android: Sped up the loading of the first frame for playback with TXLivePlayer\V2TXLivePlayer.
- iOS: Reduced the size of the iOS SDK package.
- iOS: Packaged `TXLiveBase.h` into the MLVB SDK.

**Bug fixing:** 

- All platforms: Fixed the issue where the stutter rate limit configured for TXLivePlayer does not take effect.
- All platforms: Fixed abnormal timing of the callback for the first audio/video frame when V2TXLivePusher pushes RTC streams.
- Android: Fixed the black screen issue that occurs when TXLivePlayer\V2TXLivePlayer stops and starts playback within a short period of time.

### UGSV

**New features:**

Android: Added support for editing videos without audio tracks.

**Improvement:** 

Android: Sped up the loading of the first frame for short video playback.

**Bug fixing:** 

- Android: Fixed the issue where the wrong section of video is cropped during video shooting.
- Android: Fixed incorrect aspect ratio for H.265 videos decoded with hardware.
- iOS: Fixed the issue of incorrect video clipping time.
- iOS: Fixed occasional noise that occurs in videos shot with devices with OS later than iOS 14.
- iOS: Fixed the issue where the SDK occasionally crashes when the user returns to the shooting view after finishing video shooting.

### TRTC

**New features:**
- All platforms: Launched a new API for stream mixing and relaying, which offers more powerful features and greater flexibility. For details, see the description of `startPublishMediaStream`.
- All platforms: Added support for 3D spatial audio. For details, see the description of `enable3DSpatialAudioEffect`.
- All platforms: Added support for voice activity detection. This feature works even when local audio is muted (`muteLoalAudio`) or the capturing volume is set to zero (`setAudioCaptureVolume`). It allows you to remind users when they are talking but have not turned their mics on. For details, see the description of `enableAudioVolumeEvaluation`.
- All platforms: Added support for checking a user’s permission when they switch roles. For details, see the description of `switchRole(TRTCRoleType role, const char* privateMapKey)`.
- iOS & macOS: The C++ API for custom pre-processing supported using textures for video processing.

**Improvement:** 
- Android: Optimized in-ear monitoring, reducing latency.
- Android: Optimized audio capturing, fixing the issue of noise on some devices.
- iOS: Optimized the processing of upstream video data, reducing CPU and GPU usage.
- Windows & macOS: Improved encoding for screen sharing. The height and width of the output video are no longer limited by the window size.
- Windows: Reduced memory fragmentation and performance overhead.

**Bug fixing:** 
- All platforms: Fixed the issue where push occasionally fails after changing to a different type of network.
- iOS: Fixed the issue of noise in recording files saved locally on some devices with iOS 14.

### Player

**Improvement:** 
Android & iOS: Optimized the callback of information including cached bytes and IP address during playback.

**Bug fixing:** 
- Android & iOS: Fixed failure to play H.265 videos when hardware decoding is used.
- Android & iOS: Fixed HLS playback errors.
- iOS: Fixed failure to get `supportedBitrates` in some scenarios.