## TRTCCloud @ TXLiteAVSDK

APIs for Tencent Cloud video call feature.

- **Main documentation address: [TRTC SDK for Electron](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/index.html)**
- **Sample code URL**: [TRTC Electron Demo](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)

### Creating TRTC object
```js
const TRTCCloud = require('trtc-electron-sdk').default;
// import TRTCCloud from 'trtc-electron-sdk';
this.rtcCloud = new TRTCCloud();
```

Starting from v7.9.348, the TRTC SDK for Electron has included the `trtc.d.ts` file for the convenience of developers with typescript:

```javascript
import TRTCCloud from 'trtc-electron-sdk';

const rtcCloud: TRTCCloud = new TRTCCloud();
// Get the SDK version number
rtcCloud.getSDKVersion();
```

### Callback settings
```js
subscribeEvents = (rtcCloud) => {
    rtcCloud.on('onError', (errcode, errmsg) => {
    console.info('trtc_demo: onError :' + errcode + " msg" + errmsg);
    }); 
    rtcCloud.on('onEnterRoom', (elapsed) => {
    console.info('trtc_demo: onEnterRoom elapsed:' + elapsed);
    });
    rtcCloud.on('onExitRoom', (reason) => {
    console.info('onExitRoom: userenter reason:' + reason);
    });
};

subscribeEvents(this.rtcCloud);
```

### Creating and terminating an ITRTCCloud singleton

| API | Description |
|-----|-----|
| [getTRTCShareInstance](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#.getTRTCShareInstance) | This API is used to create [ITRTCCloud](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html) object singleton in dynamic DLL loading. |
| [destroyTRTCShareInstance](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#.destroyTRTCShareInstance) | Releases [ITRTCCloud](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html) singleton object and clear up resources. |

### Room APIs

| API | Description |
|-----|-----|
| [enterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) | Enters room. If the room does not exist, the system will automatically create a new room. |
| [exitRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#exitRoom) | Exits room. |
| [switchRole](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#switchRole) | Switches roles. This API applies only to the LVB scenario (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`). |
| [connectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#connectOtherRoom) | Requests cross-room co-anchoring (cross-room anchor competition). |
| [disconnectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#disconnectOtherRoom)| Ends cross-room co-anchoring (cross-room anchor competition). |


### CDN APIs

| API | Description |
|-----|-----|
| [startPublishing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startPublishing) | Starts pushing to Tencent Cloud LVB CDN. |
| [stopPublishing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopPublishing) | Stops pushing to Tencent Cloud LVB CDN. |
| [startPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startPublishCDNStream) | Starts relaying to a non-Tencent Cloud live stream CDN. |
| [stopPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopPublishCDNStream) | Stops relaying to a non-Tencent Cloud live stream CDN. |
| [setMixTranscodingConfig](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMixTranscodingConfig) | Sets On-Cloud MixTranscoding parameters. |


### Video APIs

| API | Description |
|-----|-----|
| [startLocalPreview](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview) | Enables capture and preview of the local camera. |
| [stopLocalPreview](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopLocalPreview) | Disables capture and preview of the local camera.  |
| [muteLocalVideo](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteLocalVideo) | Specifies whether to block local video image. |
| [startRemoteView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) | Starts displaying remote video image. |
| [stopRemoteView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopRemoteView) | Stops displaying remote video image and pulling the video data stream from the remote user. |
| [stopAllRemoteView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAllRemoteView) | Stops displaying all remote video images and pulling the video data stream from remote users. |
| [muteRemoteVideoStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteVideoStream) | Pauses receiving specified remote video stream. |
| [muteAllRemoteVideoStreams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteAllRemoteVideoStreams) | Stops receiving all remote video streams. |
| [setVideoEncoderParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderParam) | Sets video encoder parameters. |
| [setNetworkQosParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setNetworkQosParam) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewFillMode) | Sets rendering mode of local image. |
| [setRemoteViewFillMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteViewFillMode) | Sets rendering mode of remote image. |
| [setLocalViewRotation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewRotation) | Sets clockwise rotation angle of local image. |
| [setRemoteViewRotation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteViewRotation) | Sets clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderRotation) | Sets the direction of image output by video encoder (i.e., video image viewed by remote users and recorded by the server). |
| [setLocalViewMirror](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewMirror) | Sets the mirror mode of local camera's preview image. |
| [setVideoEncoderMirror](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderMirror) | Sets the mirror mode of image output by encoder. |
| [enableSmallVideoStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enableSmallVideoStream) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteVideoStreamType) | Selects whether to view the big or small image of the specified `userId`. |
| [setPriorRemoteVideoStreamType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setPriorRemoteVideoStreamType) | Sets the video quality preferred by viewers. |


### Audio API functions

| API | Description |
|-----|-----|
| [startLocalAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio) | Enables local audio capture and upstreaming. |
| [stopLocalAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopLocalAudio) | Disables local audio capture and upstreaming. |
| [muteLocalAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteLocalAudio) | Mutes local audio. |
| [muteRemoteAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteAudio) | Mutes one user's audio and stops pulling the audio data stream from the remote user. |
| [muteAllRemoteAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteAllRemoteAudio) | Mutes all users' audio and stops pulling the audio data stream from remote users. |
| [setAudioCaptureVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioCaptureVolume) | Sets the SDK capture volume. |
| [getAudioCaptureVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getAudioCaptureVolume) | Gets the SDK capture volume. |
| [setAudioPlayoutVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioPlayoutVolume) | Sets the SDK playback volume. |
| [getAudioPlayoutVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getAudioPlayoutVolume) | Gets the SDK playback volume.。 |
| [enableAudioVolumeEvaluation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enableAudioVolumeEvaluation) | Enables or disables volume reminder. |
| [startAudioRecording](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startAudioRecording) | Starts audio recording. |
| [stopAudioRecording](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAudioRecording) | Stops audio recording. |
| [setAudioQuality](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioQuality) | Sets audio quality. |


### Camera APIs

| API | Description |
|-----|-----|
| [getCameraDevicesList](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCameraDevicesList) | Gets list of cameras. |
| [setCurrentCameraDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentCameraDevice) | Sets the camera to be used. |
| [getCurrentCameraDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentCameraDevice) | Gets the currently used camera. |


### Audio device APIs

| API | Description |
|-----|-----|
| [getMicDevicesList](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getMicDevicesList) | Gets list of mics. |
| [getCurrentMicDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentMicDevice) | Gets the currently used mic. |
| [setCurrentMicDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDevice) | Sets the mic to be used. |
| [getCurrentMicDeviceVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentMicDeviceVolume) | Gets current system mic volume level. |
| [setCurrentMicDeviceVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDeviceVolume) | Sets current system mic volume level. |
| [setCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDeviceMute) | Sets whether to mute current system mic. |
| [getCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentMicDeviceMute) | Gets whether the current system mic is muted. |
| [getSpeakerDevicesList](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getSpeakerDevicesList) | Gets speaker list. |
| [getCurrentSpeakerDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerDevice) | Gets the currently used speaker. |
| [setCurrentSpeakerDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerDevice) | Sets the speaker to be used. |
| [getCurrentSpeakerVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerVolume) | Gets current system speaker volume level. |
| [setCurrentSpeakerVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerVolume) | Sets current system speaker volume level. |
| [setCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerDeviceMute) | Sets whether to mute current system speaker. |
| [getCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerDeviceMute) | Gets whether the current system speaker is muted. |

### Beauty effects APIs

| API | Description |
|-----|-----|
| [setBeautyStyle](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBeautyStyle) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setWaterMark](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setWaterMark) | Sets watermark. |


### Substream APIs

| API | Description |
|-----|-----|
| [startRemoteSubStreamView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteSubStreamView) | Starts rendering the substream (screen sharing) image of a remote user. |
| [stopRemoteSubStreamView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopRemoteSubStreamView) | Stops rendering the substream (screen sharing) image of a remote user. |
| [setRemoteSubStreamViewFillMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteSubStreamViewFillMode) | Sets a rendering mode for the substream (screen sharing) image. |
| [setRemoteSubStreamViewRotation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteSubStreamViewRotation) | Sets clockwise rotation angle of the substream (screen sharing) image. |
| [getScreenCaptureSources](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getScreenCaptureSources) | Enumerates shareable windows. |
| [selectScreenCaptureTarget](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#selectScreenCaptureTarget) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [startScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startScreenCapture) | Starts screen sharing. |
| [pauseScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pauseScreenCapture) | Pauses screen sharing. |
| [resumeScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumeScreenCapture) | Resumes screen sharing. |
| [stopScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopScreenCapture) | Stops screen capture. |
| [setSubStreamEncoderParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setSubStreamEncoderParam) | Sets encoder parameters for the substream (screen sharing). |
| [setSubStreamMixVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setSubStreamMixVolume) | Sets audio mixing volume level of the substream (screen sharing). |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#sendCustomCmdMsg) | Sends custom message to all users in the room. |
| [sendSEIMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#sendSEIMsg) | Embeds custom data of a small size in video frames. |


### Background audio mixing APIs

| API | Description |
|-----|-----|
| [playBGM](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#playBGM) | Starts background music. |
| [stopBGM](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopBGM) | Stops background music. |
| [pauseBGM](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pauseBGM) | Pauses background music. |
| [resumeBGM](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumeBGM) | Resumes background music. |
| [getBGMDuration](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getBGMDuration) | Gets the total duration of the background music file in milliseconds. |
| [setBGMPosition](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBGMPosition) | Sets playback progress of background music. |
| [setBGMVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBGMVolume) | Sets background music volume level. |
| [setBGMPlayoutVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBGMPlayoutVolume) | Sets local playback volume level of the background music. |
| [setBGMPublishVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBGMPublishVolume) | Sets remote playback volume level of the background music. |
| [startSystemAudioLoopback](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startSystemAudioLoopback) | Enables system audio capture (Currently the SDK does not support system audio mixing on MacOS and 64-bit Windows. This feature is only supported on 32-bit Windows). |
| [stopSystemAudioLoopback](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopSystemAudioLoopback) | Disables system audio capture (Currently the SDK does not support system audio mixing on MacOS and 64-bit Windows. This feature is only supported on 32-bit Windows). |
| [setSystemAudioLoopbackVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setSystemAudioLoopbackVolume) | Sets system audio capture volume level (Currently the SDK does not support system audio mixing on MacOS and 64-bit Windows. This feature is only supported on 32-bit Windows). |


### Sound effect API functions

| API | Description |
|-----|-----|
| [playAudioEffect](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#playAudioEffect) | Plays the sound effect. |
| [setAudioEffectVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioEffectVolume) | Sets sound effect volume level. |
| [stopAudioEffect](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAudioEffect) | Stops the sound effect. |
| [stopAllAudioEffects](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAllAudioEffects) | Stops all sound effects. |
| [setAllAudioEffectsVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAllAudioEffectsVolume) | Sets the volume level of all sound effects. |
| [pauseAudioEffect](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pauseAudioEffect) | Pauses the sound effect. |
| [resumeAudioEffect](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumeAudioEffect) | Resumes the sound effect. |


### Device and network test APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startSpeedTest) | Starts network speed test (do not test during a video call to avoid affecting the call quality). |
| [stopSpeedTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopSpeedTest) | Stops server speed test. |
| [startCameraDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startCameraDeviceTest) | Starts camera test. |
| [stopCameraDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopCameraDeviceTest) | Stops camera test. |
| [startMicDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startMicDeviceTest) | Starts mic test. |
| [stopMicDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopMicDeviceTest) | Stops mic test. |
| [startSpeakerDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startSpeakerDeviceTest) | Starts speaker test. |
| [stopSpeakerDeviceTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopSpeakerDeviceTest) | Stops speaker test. |


### Log APIs

| API | Description |
|-----|-----|
| [getSDKVersion](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getSDKVersion) | Gets SDK version information. |
| [setLogLevel](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLogLevel) | Sets log output level. |
| [setConsoleEnabled](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setConsoleEnabled) | Enables or disables console log printing. |
| [setLogCompressEnabled](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLogCompressEnabled) | Enables or disables local log compression. |
| [setLogDirPath](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLogDirPath) | Sets log storage path. |
| [setLogCallback](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLogCallback) | Sets log callback. |
| [callExperimentalAPI](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#callExperimentalAPI) | Calls experimental API. |


### Disused APIs

| API | Description |
|-----|-----|
| [setMicVolumeOnMixing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMicVolumeOnMixing) | Disused since v6.9. |


## TRTCCallback @ TXLiteAVSDK

Callback APIs for Tencent Cloud video call feature.

### Error events and warning events

| API | Description |
|-----|-----|
| [onError](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onError) | Callback for error, which indicates that the SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onWarning) | Callback for warning. This callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onEnterRoom) | Callback of room entry. |
| [onExitRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onExitRoom) | Callback of room exit. |
| [onSwitchRole](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSwitchRole) | Callback of role switching. |
| [onConnectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectOtherRoom) | Callback of result of requesting cross-room co-anchoring (anchor competition). |
| [onDisconnectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onDisconnectOtherRoom) | Callback of the result of ending cross-room co-anchoring (anchor competition). |


### User event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRemoteUserEnterRoom) | A user enters the current room. |
| [onRemoteUserLeaveRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRemoteUserLeaveRoom) | A user exits the current room. |
| [onUserVideoAvailable](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) | Whether camera is enabled. |
| [onUserSubStreamAvailable](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserSubStreamAvailable) | Whether screen sharing is enabled. |
| [onUserAudioAvailable](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable) | Whether audio upstreaming is enabled. |
| [onFirstVideoFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onFirstVideoFrame) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onFirstAudioFrame) | Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently). |
| [onSendFirstLocalVideoFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSendFirstLocalVideoFrame) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSendFirstLocalAudioFrame) | The first local audio frame data has been sent. |
| [onUserEnter](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserEnter) | Disused API: an anchor enters the current room. |
| [onUserExit](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserExit) | Disused API: an anchor exits the current room. |


### Callbacks of statistics on quality and technical metrics

| API | Description |
|-----|-----|
| [onNetworkQuality](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onNetworkQuality) | Network quality: this callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStatistics) | Callback of technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectionLost) | The connection between SDK and server is closed. |
| [onTryToReconnect](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onTryToReconnect) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectionRecovery) | The connection between SDK and server has been restored. |
| [onSpeedTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSpeedTest) | Callback of server speed test. SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onCameraDidReady) | Camera is ready. |
| [onMicDidReady](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onMicDidReady) | Mic is ready. |
| [onUserVoiceVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVoiceVolume) | Callback of volume level, including the volume level of each `userId` and total remote volume level. |
| [onDeviceChange](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onDeviceChange) | Callback of local device connection and disconnection. |
| [onTestMicVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onTestMicVolume) | Callback of test mic volume level. |
| [onTestSpeakerVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onTestSpeakerVolume) | Callback of test speaker volume level. |
| [onDeviceChange](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onDeviceChange) | Callback of volume change on the current audio capture device. |
| [onDeviceChange](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onDeviceChange) | Callback of volume change on the current audio playback device. |


### Callbacks of custom message receipt

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRecvCustomCmdMsg) | Callback of receipt of a custom message. |
| [onMissCustomCmdMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onMissCustomCmdMsg) | Callback of loss of a custom message. |
| [onRecvSEIMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRecvSEIMsg) | Callback of receipt of an SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStartPublishing) | Callback of starting pushing to Tencent Cloud LVB CDN, which corresponds to the `startPublishing()` API in `TRTCCloud`. |
| [onStopPublishing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStopPublishing) | Callback of stopping pushing to Tencent Cloud LVB CDN, which corresponds to the `stopPublishing()` API in `TRTCCloud`. |
| [onStartPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStartPublishCDNStream) | Callback of completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStopPublishCDNStream) | Callback of completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSetMixTranscodingConfig) | Callback of setting On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in `TRTCCloud`. |


### Audio effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onAudioEffectFinished) | Callback of audio effect playback end. |


### Screen sharing callbacks

| API | Description |
|-----|-----|
| [onScreenCaptureCovered](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureCovered) | This callback will be returned by the SDK when a window for screen sharing is covered and cannot be properly captured. It can be used to ask the user to move the covering window away. |
| [onScreenCaptureStarted](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureStarted) | This callback will be returned by the SDK when screen sharing is started. |
| [onScreenCapturePaused](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCapturePaused) | This callback will be returned by the SDK when screen sharing is paused. |
| [onScreenCaptureResumed](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureResumed) | This callback will be returned by the SDK when screen sharing is resumed. |
| [onScreenCaptureStoped](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureStoped) | This callback will be returned by the SDK when screen sharing is stopped. |


### Callbacks of background music related events

| API | Description |
|-----|-----|
| [onPlayBGMBegin](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onPlayBGMBegin) | Starts the playback of background music. |
| [onPlayBGMProgress](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onPlayBGMProgress) | Progress of background music playback. |
| [onPlayBGMComplete](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onPlayBGMComplete) | Playback of background music ends. |


## Definitions of Key Classes

### Key classes

| Class | Description |
|-----|-----|
| [TRTCParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCParams.html)| Room entry parameters. |
| [TRTCVideoEncParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCVideoEncParam.html) | Video encoding parameters. |
| [TRTCNetworkQosParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCNetworkQosParam.html) | Network bandwidth limit parameters. |
| [TRTCQualityInfo](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCQualityInfo.html)| Video quality. |
| [TRTCVolumeInfo](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCVolumeInfo.html) | Volume level. |
| [TRTCSpeedTestResult](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCSpeedTestResult.html)| Network speed test result. |
| [TRTCMixUser](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCMixUser.html)| Position information of each channel of subimage in On-Cloud MixTranscoding. |
| [TRTCTranscodingConfig](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCTranscodingConfig.html)| On-Cloud MixTranscoding configuration. |
| [TRTCPublishCDNParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCPublishCDNParam.html)| CDN relayed push parameters. |
| [TRTCAudioRecordingParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCAudioRecordingParams.html)| Audio recording parameters. |
| [TRTCLocalStatistics](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCLocalStatistics.html)| Local audio/video statistics. |
| [TRTCRemoteStatistics](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCRemoteStatistics.html) | Remote audio/video statistics. |
| [TRTCStatistics](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCStatistics.html)| Statistics. |

### Enumerated values

| Enumerated Value | Description |
|-----|-----|
| [TRTCVideoResolution](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoResolution)| Video resolution. |
| [TRTCVideoResolutionMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoResolutionMode)| Video resolution mode. |
| [TRTCVideoStreamType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoStreamType) | Video stream type. |
| [TRTCQuality](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCQuality)| Image quality level. |
| [TRTCVideoFillMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoFillMode)| Video image fill mode. |
| [TRTCBeautyStyle](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCBeautyStyle) | Beauty filter (skin smoothing) algorithm. |
| [TRTCAppScene](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCAppScene)| Use cases. |
| [TRTCRoleType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCRoleType)| Role, which applies only to the live streaming scenario (`TRTCAppSceneLIVE`). |
| [TRTCQosControlMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCQosControlMode)| Bandwidth limit mode. |
| [TRTCVideoQosPreference](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoQosPreference)| Image quality preference. |
| [TRTCDeviceState](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCDeviceState)| Device operation. |
| [TRTCDeviceType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCDeviceType)| Device type. |
| [TRTCWaterMarkSrcType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCWaterMarkSrcType)| Watermark image source type. |
| [TRTCTranscodingConfigMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCTranscodingConfigMode)| MixTranscoding parameter configuration mode. |
