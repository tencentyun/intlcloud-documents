
The forming rule of version number `major.minor.patch` is as follows:
  - major: major version number. If there is major version refactoring, this field will be incremented. Generally, the APIs of different major versions are not compatible with each other.
  - minor: minor version number. The APIs of different minor versions are compatible with each other. If there is a new or optimized API, this field will be incremented.
  - patch: patch number. If there is a feature improvement or bug fix, this field will be incremented.

>!
> - We recommend you update to the latest version in time for better service stability and online support.
> - For notes on version upgrade, please see [Update Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-00-info-update-guideline.html).

## Version 4.8.6 Released on March 1, 2021

**Improvements**

Supported stereo playback during pull.
>! Unavailable on iOS yet.

**Fixes**

Fixed the issue where the web received the `stream-removed` event when the video was muted and frozen on a mobile device.

## Version 4.8.5 Released on January 29, 2021

**Improvements**

- Supported setting multiple turn servers for [Client.setTurnServer](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#setTurnServer).
- Optimized the `userId` verification logic.

**Fixes**

Fixed the issue where the mute status was occasionally inaccurate after push was started.

## Version 4.8.4 Released on January 15, 2021

**Improvements**

- Supported dynamically calling the [LocalStream.setVideoProfile](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html#setVideoProfile) API.
- Optimized the data reporting logic of the dashboard.
- Optimized the processing logic when autoplay was restricted. For more information, please see [Recommendations for Restricted Autoplay](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-21-advanced-auto-play-policy.html).
- Optimized the processing logic when auto resumption failed upon device plug/unplug. For more information, please see [DEVICE_AUTO_RECOVER_FAILED](https://trtc-1252463788.file.myqcloud.com/web/docs/module-ErrorCode.html#.DEVICE_AUTO_RECOVER_FAILED).

**Fixes**

Fixed the issue where the mute status was occasionally inaccurate after push was resumed.

## Version 4.8.3 Released on January 7, 2021

**Improvements**

Optimized the parameter verification logic of the room entry API `roomId`.

**Fixes**

- Fixed the issue where the version 4.8.2 lacked third-party dependencies.
- Fixed the occasional issue of muted playback when only audio was subscribed to.
- Fixed the issue where `resume` was muted and `getAudioLevel` was 0 on iOS after autoplay was restricted.

## Version 4.8.2 Released on December 31, 2020

**Breaking changes**

Deleted the disused API `setDefaultMuteRemoteStreams`. Please use the [client.unsubscribe](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#unsubscribe) API instead.

**Improvements**

- Optimized the parameter verification logic of the room entry API `roomId`. For more information, please see the [API documentation](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html#join) and [Upgrade Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-00-info-update-guideline.html).
- Optimized the notification timing of `peer-join` and `peer-leave` events.

**Fixes**

Fixed the occasional error of `Cannot read property 'isConnected' of null` during room exit.


## Version 4.8.1 Released on December 25, 2020

**Fixes**

- Fixed the occasional issue where the remote user's voice couldn't be heard on Windows.
- Fixed the issue where the `client.getRemoteVideoStats()` API returned empty data.

## Version 4.8.0 Released on December 18, 2020

**New features**

- Supported On-Cloud MixTranscoding.
- Supported string room IDs on all platforms. For more information, please see the [`userDefineRecordId` parameter of `TRTC.createClient`](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.createClient).

**Improvements**

- Optimized the H.264 support check logic.
- Optimized the device switching logic.
- Optimized the status judgment logic of the `hasAudio`/`hasVideo` APIs.

**Fixes**

- Fixed the occasional issue where reconnection failed after network disconnection.
- Fixed the issue of black screen caused by frequently adding/removing tracks on Safari.

## Version 4.7.1 Released on November 27, 2020

**Improvements**

- Optimized the auto capturing resumption logic when the media device was changed (for example, the interface was loose or the device was plugged/unplugged).
- Added the new error code [DEVICE_AUTO_RECOVER_FAILED](https://trtc-1252463788.file.myqcloud.com/web/docs/module-ErrorCode.html#.DEVICE_AUTO_RECOVER_FAILED), which could be used to prompt when device recovery failed.

**Fixes**

- Fixed the occasional issue of black screen on Chrome 87.
- Fixed the issue where the screen sharing stream disappeared during camera push + screen sharing for Native and resubscription or unsubscription for web.

## Version 4.7.0 Released on November 20, 2020

**New features**

Supported Firefox M56+ and Edge M80+ for the desktop.

**Breaking changes**

[TRTC.checkSystemRequirements](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.checkSystemRequirements) could return detailed check results. For more information, please see the [API documentation](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.checkSystemRequirements) and [Upgrade Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-00-info-update-guideline.html).

**Improvements**

- Optimized the upstream bitrate control logic.
- Optimized the retry logic for getting media devices.
- Optimized the WebSocket reconnection logic.
- Optimized the auto push resumption logic when the device was changed and supported auto push resumption when the mic was plugged/unplugged during audio mixing.


## Version 4.6.7 Released on November 5, 2020

**Fixes**

- Fixed the occasional issue of blurred screen during pull for playback when hardware acceleration was enabled on Chrome.
- Fixed the issue where room entry couldn't be performed for pull in the browser built in WeChat on iOS.

## Version 4.6.6 Released on October 23, 2020

**Improvements**

- Optimized the upstream `peerConnection` reconnection logic.
- Optimized the downstream `peerConnection` reconnection logic.
- Optimized the `TRTC.checkSystemRequirements` check logic.
- Supported screen sharing on Safari. For more information, please see [Screen Sharing Guide](https://trtc-1252463788.file.myqcloud.com/web/docs/tutorial-16-basic-screencast.html).

**Fixes**

Fixed the issue where the `getAudioLevel` value was 0 after audio playback was manually resumed due to the restriction of the autoplay policy.

## Version 4.6.5 Released on October 14, 2020

**Improvements**

- Optimized the WebSocket signaling channel reconnection logic to improve the connection stability.
- Optimized the log output logic.

**Fixes**

- Fixed the issue where the `getAudioLevel` API returned a value of 0 after resubscription on Chrome.
- Fixed the issue of muted playback after resubscription on Safari.
- Fixed the issue where the `getLocalVideoStats` API returned `undefined` after the upstream audio track was replaced with `replaceTrack`.
- Fixed the occasional issue of WebSocket disconnection upon network type switch during call on a mobile device.

## Version 4.6.4 Released on September 24, 2020

**Improvements**

Supported stopping collecting network quality statistics after room exit.

**Fixes**

- Fixed the error of room entry on Chrome 56.
- Fixed the issue of screen rotation during relayed push on a mobile device.
- Fixed the issue of exceptional on-cloud recording when pure audio was pushed.
- Fixed the issue where auto push resumption failed due to inconsistent resolution after the camera was unplugged.

## Version 4.6.3 Released on August 28, 2020

**Improvements**

- Optimized the compatibility check logic.
- Optimized the log reporting logic.
- Optimized the upstream bitrate control logic.

## Version 4.6.2 Released on August 14, 2020

**Improvements**

- Optimized the upstream bitrate control logic.
- Optimized the `switchRole` parameter verification logic.
- Optimized the calculation logic of upstream network quality.
- Optimized the error messages.
- Supported automatically resuming push when the change of the current stream capturing device was detected.

**Fixes**

Fixed the issue where immediate republishing failed after `unpublish` succeeded.

## Version 4.6.1 Released on July 28, 2020

**Improvements**

- Added [TRTC.isScreenShareSupported](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html#.isScreenShareSupported). Safari didn't support screen sharing yet.
- Improved the parameter verification logic of the `subscribe` and `unsubscribe` APIs.
- Added the network quality logging feature.

**Fixes**

- Fixed the issue where the SDK reported `OverconstrainedError` when the media device was not authorized and the device ID passed in by the `TRTC.createStream` API was an empty string.
- Fixed the issue where no log was printed when the upstream `peerConnection` was interrupted.

## Version 4.6.0 Released on July 16, 2020

**New features**

Added the `NETWORK_QUALITY` event.

## Version 4.5.0 Released on July 2, 2020

**New features**

Added the `screenAudio` parameter for the `createStream` API.

**Fixes**

- Fixed the issue where echo cancellation did not work in a browser on Android.
- Fixed the issue where the RTT value returned by the `getTransportStats` API was `NAN`.

## Version 4.4.0 Released on May 28, 2020

**New features**

Supported capturing audio of the system (Windows) or current tab (macOS) during screen sharing on Chrome 74 or above.

## Version 4.3.13 Released on April 16, 2020

**Improvements**

Optimized the availability check logic.

## Version 4.3.12 Released on April 13, 2020

**Fixes**

Fixed a potential exception of `RTCPeerConnection` status change.

## Version 4.3.11 Released on March 28, 2020

**Improvements**

Added check for Mobile QQ Browser, which didn't support the TRTC SDK for Desktop Browser yet.

**Fixes**

Fixed the Boolean returned value type.

## Version 4.3.10 Released on March 17, 2020

**Improvements**

- Optimized the environment check logic.
- Added `name code` for `RtcError`.

## Version 4.3.9 Released on March 13, 2020

**Improvements**

- Added auto deployment environment check.
- Optimized the logging feature.

## Version 4.3.8 Released on February 24, 2020

**Improvements**

Added the `streamId` and `userdefinerecordid` fields for `createClient`.

## Version 4.3.7 Released on February 21, 2020

**Improvements**

Fixed the exception thrown by device switch during screen sharing.

**Fixes**

- Fixed the issue where devices were in use after `MediaStream` was released during device switch.
- Fixed the potential error of the subscription API.

## Version 4.3.6 Released on February 5, 2020

**Fixes**

Adjusted the audio/video playback sequence of `Stream.resume()` and fixed the issue of exceptional playback in WeChat Browser on iOS.

## Version 4.3.5 Released on February 5, 2020

**Improvements**

Added the `publish` timeout check to improve the success rate of signaling.

## Version 4.3.4 Released on January 6, 2020

**Improvements**

Upgraded `core-js` to v3.6.1.

**Fixes**

- Fixed the issue where an exception was thrown after `unpublish` timed out.
- Fixed the v8 issue caused by third-party libraries.

## Version 4.3.3 Released on December 25, 2019

**Improvements**

- Added active environment check for WebRTC support.
- Optimized the SDP response mechanism.
- Optimized the reporting logic.

**Fixes**

Fixed the TURN URL protocol format.

## Version 4.3.2 Released on December 9, 2019

**Improvements**

- Added the automatic reconnection mechanism for downstream ICE disconnection.
- Removed the STUN hole punching operation to increase the success rate and speed of user connection over the private network.
- Uniformly used the UTC time calibrated with the server as the timestamp of log reporting.
- Optimized ICE error reporting.
- Added more key events to `avmonitor` reporting.

**Fixes**

- Fixed the reconnection exception and error of the WebSocket signaling channel 1005.
- Fixed the issue of downstream packet loss rate reporting.

## Version 4.3.1 Released on November 23, 2019

**Improvements**

Added the automatic reconnection mechanism for upstream linkage ICE disconnection during call.

**Fixes**

Fixed the issue where the host ICE candidate of public IP type did not take effect after STUN hole punching failed.

## Version 4.3.0 Released on November 15, 2019

**New features**

Added the `Client.getTransportStats()` API.

**Improvements**

- Supported more detailed log reporting.
- Supported wildcard for event unbinding.
- Extended the connection timeout period to 5 seconds.
- Extended the publishing timeout period to 5 seconds.

**Fixes**

Fixed the issue of exceptional SDK judgment due to modification of the prototype chain by `zone.js`.

## Version 4.2.0 Released on November 4, 2019

**New features**

Added the `Client.off()` API to unbind client events.

**Improvements**

- Optimized the call status statistics.
- Added permission check for `Client.publish()`.
- Added error prompt for autoplay for `Stream.play()/resume()`.

**Fixes**

Fixed the issue where the screen turned black during camera switch with `LocalStream.switchDevice()`.

## Version 4.1.1 Released on October 24, 2019

**Fixes**

- Fixed the issue of lost logs.
- Fixed the issue of lost remote users upon reconnection.

## Version 4.1.0 Released on October 17, 2019

**New features**

- Supported passing the `HTMLDivElement` object to the `Stream.play()` API.
- Added audio bitrate adjustment settings. You could set the audio attribute through `LocalStream.setAudioProfile()`. Two profiles were supported: standard and high.

**Fixes**

- Fixed the issue where the number of `WebAudio Context` values was limited on legacy Chrome.
- Fixed the issue where `replaceTrack()` did not restart the local audio/video player.
- Fixed the issue where the `LocalStream.setScreenProfile()` custom attribute configuration did not take effect.
- Fixed the issues of audio/video player restart and status reporting.

## Version 4.0.0 Released on October 11, 2019

Added the rebuild version of the TRTC SDK for Desktop Browser to provide APIs in the `Client/Stream` model, where the responsibilities of each object were clearer, and the semantics were more concise.
The rebuild version was not compatible with the legacy version. In addition to API changes, it also had the following features:

- Video attributes (resolution, frame rate, and bitrate) were completely controlled by the application through the SDK's `LocalStream.setVideoProfile()` API. The "image settings (Spear Role)" in the Tencent Cloud console for the legacy version were no longer supported.
- The SDK encapsulated an audio/video player in the `Stream` object, and audio/video playback was completely controlled by the SDK.
- The features of subscribing to and unsubscribing from remote streams were offered. You could flexibly control the reception of remote audio, video, or audio/video data streams through the `Client.subscribe()/unsubscribe()` APIs.
