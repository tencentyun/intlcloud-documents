## TRTCCloud @ TXLiteAVSDK

Main API class for the TRTC video call feature.

- **Main documentation address**: [TRTC SDK for Electron](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/index.html)
- **Sample code address**: [TRTC Demo for Electron](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)

### Creating TRTC object
```js
const TRTCCloud = require('trtc-electron-sdk');
this.rtcCloud = new TRTCCloud();
```

Starting from v7.0.149, the TRTC SDK for Electron has included the `trtc.d.ts` file for the convenience of developers with TypeScript:

```javascript
// Enable ES Module interoperability mode (esModuleInterop=true)
import * as trtc_namespace from 'trtc-electron-sdk';

const TRTCCloud = require('trtc-electron-sdk');

const rtcCloud: trtc_namespace.TRTCCloud = new TRTCCloud();
// Get the SDK version number
rtcCloud.getSDKVersion();
```

### Setting callbacks
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
| [getTRTCShareInstance](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#.getTRTCShareInstance) | Creates [ITRTCCloud](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html) object singleton when loading dll files dynamically. |
| [destroyTRTCShareInstance](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#.destroyTRTCShareInstance) | Releases [ITRTCCloud](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html) object singleton and clears resources. |

### Room APIs

| API | Description |
|-----|-----|
| [enterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enterRoom) | Enters room. If the room does not exist, the system will automatically create a room. |
| [exitRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#exitRoom) | Exits room. |
| [switchRole](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#switchRole) | Switches role. This API applies only to the live streaming scenario (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`). |
| [connectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#connectOtherRoom) | Requests cross-room co-anchoring (cross-room anchor competition). |
| [disconnectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#disconnectOtherRoom)| Disables cross-room co-anchoring (cross-room anchor competition). |


### CDN APIs

| API | Description |
|-----|-----|
| [startPublishing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startPublishing) | Starts pushing to Tencent Cloud LVB CDN. |
| [stopPublishing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopPublishing) | Stops pushing to Tencent Cloud LVB CDN. |
| [startPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startPublishCDNStream) | Starts relaying to a non-Tencent Cloud live streaming CDN. |
| [stopPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopPublishCDNStream) | Stops pushing to a non-Tencent Cloud live streaming CDN. |
| [setMixTranscodingConfig](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMixTranscodingConfig) | Sets On-Cloud MixTranscoding parameters. |


### Video APIs

| API | Description |
|-----|-----|
| [startLocalPreview](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalPreview) | Starts local camera capturing and preview. |
| [stopLocalPreview](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopLocalPreview) | Stops local camera capturing and preview. |
| [muteLocalVideo](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteLocalVideo) | Specifies whether to block local video image. |
| [startRemoteView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteView) | Starts displaying remote video image. |
| [stopRemoteView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopRemoteView) | Stops displaying remote video image and pulling the video data stream of remote user. |
| [stopAllRemoteView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAllRemoteView) | Stops displaying all remote video images and pulling the video data streams of all remote users. |
| [muteRemoteVideoStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteVideoStream) | Pauses receiving specified remote video stream. |
| [muteAllRemoteVideoStreams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteAllRemoteVideoStreams) | Stops receiving all remote video streams. |
| [setVideoEncoderParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderParam) | Sets video encoder parameters. |
| [setNetworkQosParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setNetworkQosParam) | Sets network bandwidth limit parameters. |
| [setLocalViewFillMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewFillMode) | Sets the rendering mode of local image. |
| [setRemoteViewFillMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteViewFillMode) | Sets the rendering mode of remote image. |
| [setLocalViewRotation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewRotation) | Sets the clockwise rotation angle of local image. |
| [setRemoteViewRotation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteViewRotation) | Sets the clockwise rotation angle of remote image. |
| [setVideoEncoderRotation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderRotation) | Sets direction of image output by video encoder (i.e., image viewed by remote user and recorded by server). |
| [setLocalViewMirror](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalViewMirror) | Sets mirror mode of local camera's preview image. |
| [setVideoEncoderMirror](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setVideoEncoderMirror) | Sets the mirror mode of image output by encoder. |
| [enableSmallVideoStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enableSmallVideoStream) | Enables dual-channel encoding mode with big and small images. |
| [setRemoteVideoStreamType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteVideoStreamType) | Selects whether to view the big or small image of the specified `userId`. |
| [setPriorRemoteVideoStreamType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setPriorRemoteVideoStreamType) | Sets the video quality preferred by viewers. |


### Audio APIs

| API | Description |
|-----|-----|
| [startLocalAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startLocalAudio) | Enables local audio capturing and upstreaming. |
| [stopLocalAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopLocalAudio) | Disables local audio capturing and upstreaming. |
| [muteLocalAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteLocalAudio) | Mutes local audio. |
| [muteRemoteAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteRemoteAudio) | Mutes specified remote user's audio and stops pulling the audio data stream of remote user. |
| [muteAllRemoteAudio](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#muteAllRemoteAudio) | Mutes all users' audio and stops pulling audio data streams of remote users. |
| [setAudioCaptureVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioCaptureVolume) | Sets SDK capturing volume level. |
| [getAudioCaptureVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getAudioCaptureVolume) | Gets SDK capturing volume level. |
| [setAudioPlayoutVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioPlayoutVolume) | Sets SDK playback volume level. |
| [getAudioPlayoutVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getAudioPlayoutVolume) | Gets SDK playback volume level. |
| [enableAudioVolumeEvaluation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#enableAudioVolumeEvaluation) | Enables or disables volume reminder. |
| [startAudioRecording](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startAudioRecording) | Starts audio recording. |
| [stopAudioRecording](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAudioRecording) | Stops audio recording. |
| [setAudioQuality](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioQuality) | Sets audio quality. |



### Camera APIs

| API | Description |
|-----|-----|
| [getCameraDevicesList](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCameraDevicesList) | Gets camera list. |
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
| [setCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDeviceMute) | Sets the mute status of the current system mic. |
| [getCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentMicDeviceMute) | Gets the mute status of the current system mic. |
| [getSpeakerDevicesList](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getSpeakerDevicesList) | Gets speaker list. |
| [getCurrentSpeakerDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerDevice) | Gets the currently used speaker. |
| [setCurrentSpeakerDevice](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerDevice) | Sets the speaker to be used. |
| [getCurrentSpeakerVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerVolume) | Gets current system speaker volume level. |
| [setCurrentSpeakerVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerVolume) | Sets current system speaker volume level. |
| [setCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerDeviceMute) | Sets the mute status of the current system speaker. |
| [getCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerDeviceMute) | Gets the mute status of the current system speaker. |

### Beauty filter APIs

| API | Description |
|-----|-----|
| [setBeautyStyle](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBeautyStyle) | Sets effect levels of beauty, brightening, and rosy skin filters. |
| [setWaterMark](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setWaterMark) | Sets watermark. |


### Substream APIs

| API | Description |
|-----|-----|
| [startRemoteSubStreamView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startRemoteSubStreamView) | Starts rendering the substream (screen sharing) image of remote user. |
| [stopRemoteSubStreamView](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopRemoteSubStreamView) | Stops rendering the substream (screen sharing) image of remote user. |
| [setRemoteSubStreamViewFillMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteSubStreamViewFillMode) | Sets the rendering mode of substream (screen sharing) image. |
| [setRemoteSubStreamViewRotation](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteSubStreamViewRotation) | Sets the clockwise rotation angle of substream (screen sharing) image. |
| [getScreenCaptureSources](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getScreenCaptureSources) | Enumerates shareable windows. |
| [selectScreenCaptureTarget](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#selectScreenCaptureTarget) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [startScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startScreenCapture) | Starts screen sharing. |
| [pauseScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pauseScreenCapture) | Pauses screen sharing. |
| [resumeScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumeScreenCapture) | Resumes screen sharing. |
| [stopScreenCapture](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopScreenCapture) | Stops screen sharing. |
| [setSubStreamEncoderParam](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setSubStreamEncoderParam) | Sets encoding parameters for substream (screen sharing). |
| [setSubStreamMixVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setSubStreamMixVolume) | Sets the audio mixing volume level of substream (screen sharing). |


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
| [getBGMDuration](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getBGMDuration) | Gets the total length of background music file in milliseconds. |
| [setBGMPosition](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBGMPosition) | Sets background music playback progress. |
| [setBGMVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBGMVolume) | Sets the playback volume level of background music. |
| [setBGMPlayoutVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBGMPlayoutVolume) | Sets the local playback volume level of background music. |
| [setBGMPublishVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setBGMPublishVolume) | Sets the remote playback volume level of background music. |
| [startSystemAudioLoopback](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startSystemAudioLoopback) | Enables system audio capturing (currently, system audio mixing is supported only for Windows 32-bit but not for macOS/Windows 64-bit. If called on an unsupported system, this API will not work). |
| [stopSystemAudioLoopback](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopSystemAudioLoopback) | Disables system audio capturing (currently, system audio mixing is supported only for Windows 32-bit but not for macOS/Windows 64-bit. If called on an unsupported system, this API will not work). |
| [setSystemAudioLoopbackVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setSystemAudioLoopbackVolume) | Sets the volume level of system audio capturing (currently, system audio mixing is supported only for Windows 32-bit but not for macOS/Windows 64-bit. If called on an unsupported system, this API will not work). |


### Sound effect APIs

| API | Description |
|-----|-----|
| [playAudioEffect](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#playAudioEffect) | Plays back sound effect. |
| [setAudioEffectVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioEffectVolume) | Sets sound effect volume level. |
| [stopAudioEffect](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAudioEffect) | Stops sound effect. |
| [stopAllAudioEffects](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopAllAudioEffects) | Stops all sound effects. |
| [setAllAudioEffectsVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAllAudioEffectsVolume) | Sets the volume level of all sound effects. |
| [pauseAudioEffect](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pauseAudioEffect) | Pauses sound effect. |
| [resumeAudioEffect](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumeAudioEffect) | Resumes sound effect. |


### Device and network test APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startSpeedTest) | Starts network speed test (do not test during a video call so as to avoid affecting the call quality). |
| [stopSpeedTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopSpeedTest) | Stops network speed test. |
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
| [setConsoleEnabled](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setConsoleEnabled) | Disables or enables console log printing. |
| [setLogCompressEnabled](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLogCompressEnabled) | Enables or disables local log compression. |
| [setLogDirPath](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLogDirPath) | Sets log storage path. |
| [setLogCallback](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLogCallback) | Sets log callback. |
| [callExperimentalAPI](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#callExperimentalAPI) | Calls experimental API. |


### Disused APIs

| API | Description |
|-----|-----|
| [setMicVolumeOnMixing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMicVolumeOnMixing) | Disused since v6.9. |


## TRTCCallback @ TXLiteAVSDK

Callback API class for TRTC video call feature.

### Error events and warning events

| API | Description |
|-----|-----|
| [onError](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onError) | Callback for error: SDK encountered an irrecoverable error and must be listened on. Corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onWarning) | Callback for warning: this callback is used to alert to some non-serious problems such as lag or recoverable decoding failure. |


### Room event callbacks

| API | Description |
|-----|-----|
| [onEnterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onEnterRoom) | Callback for room entry. |
| [onExitRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onExitRoom) | Callback for room exit. |
| [onSwitchRole](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSwitchRole) | Callback for role switching. |
| [onConnectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectOtherRoom) | Callback for result of requesting cross-room co-anchoring (cross-room anchor competition). |
| [onDisconnectOtherRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onDisconnectOtherRoom) | Callback for result of ending cross-room co-anchoring (cross-room anchor competition). |


### Member event callbacks

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRemoteUserEnterRoom) | A user enters the current room. |
| [onRemoteUserLeaveRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRemoteUserLeaveRoom) | A user exits the current room. |
| [onUserVideoAvailable](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVideoAvailable) | Whether camera is enabled for video. |
| [onUserSubStreamAvailable](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserSubStreamAvailable) | Whether screen sharing is enabled. |
| [onUserAudioAvailable](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserAudioAvailable) | Whether audio upstreaming is enabled. |
| [onFirstVideoFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onFirstVideoFrame) | Rendering of the first frame of a local or remote user starts. |
| [onFirstAudioFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onFirstAudioFrame) | Playback of the first audio frame of a remote user starts (local audio is not supported for notification currently). |
| [onSendFirstLocalVideoFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSendFirstLocalVideoFrame) | The first local video frame data has been sent. |
| [onSendFirstLocalAudioFrame](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSendFirstLocalAudioFrame) | The first local audio frame data has been sent. |
| [onUserEnter](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserEnter) | Disused API: an anchor enters the current room. |
| [onUserExit](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserExit) | Disused API: an anchor exits the current room. |


### Statistics collection and quality callbacks

| API | Description |
|-----|-----|
| [onNetworkQuality](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onNetworkQuality) | Network quality: this callback is triggered once every 2 seconds to collect statistics of the current network upstreaming and downstreaming quality. |
| [onStatistics](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStatistics) | Callback for technical metric statistics. |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectionLost) | The connection between SDK and server is closed. |
| [onTryToReconnect](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onTryToReconnect) | The SDK tries to connect to the server again. |
| [onConnectionRecovery](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onConnectionRecovery) | The connection between SDK and server has been restored. |
| [onSpeedTest](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSpeedTest) | Callback for server speed test. SDK tests the speed of multiple server IPs, and the test result of each IP is returned through this callback notification. |


### Hardware device event callbacks

| API | Description |
|-----|-----|
| [onCameraDidReady](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onCameraDidReady) | Camera is ready. |
| [onMicDidReady](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onMicDidReady) | Mic is ready. |
| [onUserVoiceVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onUserVoiceVolume) | Callback for volume level, including the volume level of each `userId` and total remote volume level. |
| [onDeviceChange](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onDeviceChange) | Callback for local device connection and disconnection. |
| [onTestMicVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onTestMicVolume) | Callback for mic volume level in test. |
| [onTestSpeakerVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onTestSpeakerVolume) | Callback for speaker volume level in test. |


### Custom message reception callbacks

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRecvCustomCmdMsg) | Callback for receipt of custom message. |
| [onMissCustomCmdMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onMissCustomCmdMsg) | Callback for loss of custom message. |
| [onRecvSEIMsg](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onRecvSEIMsg) | Callback for receipt of SEI message. |


### CDN relayed push callbacks

| API | Description |
|-----|-----|
| [onStartPublishing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStartPublishing) | Callback for starting pushing to Tencent Cloud LVB CDN, which corresponds to the `startPublishing()` API in `TRTCCloud`. |
| [onStopPublishing](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStopPublishing) | Callback for stopping pushing to Tencent Cloud LVB CDN, which corresponds to the `stopPublishing()` API in `TRTCCloud`. |
| [onStartPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStartPublishCDNStream) | Callback for completion of starting relayed push to CDN. |
| [onStopPublishCDNStream](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onStopPublishCDNStream) | Callback for completion of stopping relayed push to CDN. |
| [onSetMixTranscodingConfig](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSetMixTranscodingConfig) | Callback for setting On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in `TRTCCloud`. |


### Sound effect callbacks

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onAudioEffectFinished) | Callback for sound effect playback end. |


### Screen sharing callbacks

| API | Description |
|-----|-----|
| [onScreenCaptureCovered](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureCovered) | This callback will be returned by the SDK when a window for screen sharing is covered and cannot be properly captured. It can be used to ask the user to move the covering window away. |
| [onScreenCaptureStarted](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureStarted) | This callback will be returned by the SDK when screen sharing is started. |
| [onScreenCapturePaused](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCapturePaused) | This callback will be returned by the SDK when screen sharing is paused. |
| [onScreenCaptureResumed](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureResumed) | This callback will be returned by the SDK when screen sharing is resumed. |
| [onScreenCaptureStopped](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onScreenCaptureStopped) | This callback will be returned by the SDK when screen sharing is stopped. |


### Background audio mixing event callbacks

| API | Description |
|-----|-----|
| [onPlayBGMBegin](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onPlayBGMBegin) | Playback of background music starts. |
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
| [TRTCAppScene](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCAppScene)| Application scenario. |
| [TRTCRoleType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCRoleType)| Role, which applies only to the LVB scenario (`TRTCAppSceneLIVE`). |
| [TRTCQosControlMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCQosControlMode)| Bandwidth limit mode. |
| [TRTCVideoQosPreference](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoQosPreference)| Image quality preference. |
| [TRTCDeviceState](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCDeviceState)| Device operation. |
| [TRTCDeviceType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCDeviceType)| Device type. |
| [TRTCWaterMarkSrcType](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCWaterMarkSrcType)| Watermark image source type. |
| [TRTCTranscodingConfigMode](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCTranscodingConfigMode)| MixTranscoding parameter configuration mode. |
