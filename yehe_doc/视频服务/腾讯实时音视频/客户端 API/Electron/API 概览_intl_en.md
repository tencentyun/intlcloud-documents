## TRTCCloud @ TXLiteAVSDK

APIs for Tencent Cloud’s video call feature

- **Documentation: [TRTC Electron SDK](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)**
- **Sample code**: [TRTC Electron Demo](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)

### Creating TRTC objects
```js
const TRTCCloud = require('trtc-electron-sdk').default;
// import TRTCCloud from 'trtc-electron-sdk';
this.rtcCloud = new TRTCCloud();
```

Since version 7.9.348, TRTC SDK for Electron has integrated `trtc.d.ts` for developers using TypeScript.

```javascript
import TRTCCloud from 'trtc-electron-sdk';

const rtcCloud: TRTCCloud = new TRTCCloud();
// Get the SDK version number.
rtcCloud.getSDKVersion();
```

### Setting callback
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

### Creating and terminating ITRTCCloud singletons

| API | Description |
|-----|-----|
| [getTRTCShareInstance](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#.getTRTCShareInstance) | Creates a [ITRTCCloud](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html) singleton object during dynamic DLL loading. |
| [destroyTRTCShareInstance](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#.destroyTRTCShareInstance) | Releases a [ITRTCCloud](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html) singleton object and frees up resources. |

### Room APIs

| API | Description |
|-----|-----|
| [enterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom) | Enters a room. If the room does not exist, the system will create one automatically. |
| [exitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#exitRoom) | Exits a room. |
| [switchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRoom) | Switches rooms. |
| [switchRole](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRole) | Switches roles. This API applies only to the live streaming modes (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`). |
| [connectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#connectOtherRoom) | Requests cross-room co-anchoring (anchor competition). |
| [disconnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#disconnectOtherRoom)| Ends cross-room co-anchoring (anchor competition). |


### CDN APIs

| API | Description |
|-----|-----|
| [startPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPublishing) | Starts pushing to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPublishing) | Stops pushing to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPublishCDNStream) | Starts relaying to the live streaming CDN of a non-Tencent Cloud vendor. |
| [stopPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPublishCDNStream) | Stops relaying to the live streaming CDN of a non-Tencent Cloud vendor. |
| [setMixTranscodingConfig](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMixTranscodingConfig) | Sets On-Cloud MixTranscoding parameters. |


### Video APIs

| API | Description |
|-----|-----|
| [startLocalPreview](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview) | Enables capture and preview of the local camera. |
| [stopLocalPreview](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopLocalPreview) | Disables capture and preview of the local camera. |
| [muteLocalVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalVideo) | Block/Unblocks local video. |
| [startRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView) | Starts displaying the video image of a remote user. |
| [stopRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopRemoteView) | Stops displaying the video image of a remote user and pulling the user’s video stream. |
| [stopAllRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAllRemoteView) | Stops displaying the video images of all users and pulling their video streams. |
| [muteRemoteVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteVideoStream) | Pauses receiving a specified remote video stream. |
| [muteAllRemoteVideoStreams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteAllRemoteVideoStreams) | Stops receiving all remote video streams. |
| [setVideoEncoderParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam) | Sets video encoder parameters. |
| [setNetworkQosParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setNetworkQosParam) | Sets QoS control parameters. |
| [setLocalRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalRenderParams) | Sets rendering parameters for the local image (primary stream). |
| [setLocalViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewFillMode) | Disused API: sets the rendering mode of the local image. |
| [setRemoteRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParams) | Sets rendering parameters for a remote image. |
| [setRemoteViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteViewFillMode) | Disused API: sets the rendering mode of a remote image. |
| [setLocalViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewRotation) | Disused API: sets the clockwise rotation degree of the local image. |
| [setRemoteViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteViewRotation) | Disused API: sets the clockwise rotation degree of a remote image. |
| [setVideoEncoderRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderRotation) | Sets the rotation degree of encoded video images, i.e., images presented to remote users and recorded by the server. |
| [setLocalViewMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewMirror) | Disused API: sets the mirror mode of the local camera's preview image. |
| [setVideoEncoderMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderMirror) | Sets the mirror mode of encoded images. |
| [enableSmallVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enableSmallVideoStream) | Enables the dual-channel (big and small images) encoding mode. |
| [setRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteVideoStreamType) | Sets whether to view the big or small image of a specified `userId`. |
| [setPriorRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setPriorRemoteVideoStreamType) | Disused API: sets video quality preferences for viewers. |
| [snapshotVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#snapshotVideo) | Takes a video screenshot. |


### Audio APIs

| API | Description |
|-----|-----|
| [startLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio) | Enables local audio capture and upstream data transfer. |
| [stopLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopLocalAudio) | Disables local audio capture and upstream data transfer. |
| [muteLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalAudio) | Mutes local audio. |
| [muteRemoteAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio) | Mutes a remote user and stops pulling the user’s audio stream. |
| [muteAllRemoteAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteAllRemoteAudio) | Mutes all remote users and stops pulling their audio streams. |
| [setAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioCaptureVolume) | Sets the SDK capture volume. |
| [getAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getAudioCaptureVolume) | Gets the SDK capture volume. |
| [setAudioPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioPlayoutVolume) | Sets the SDK playback volume. |
| [getAudioPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getAudioPlayoutVolume) | Gets the SDK playback volume. |
| [enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enableAudioVolumeEvaluation) | Enables/Disables volume reminders. |
| [startAudioRecording](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startAudioRecording) | Starts audio recording. |
| [stopAudioRecording](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAudioRecording) | Stops audio recording. |
| [setAudioQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioQuality) | Disused API: sets audio quality. |
| [setRemoteAudioVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteAudioVolume) | Sets the playback volume of a remote user. |


### Camera APIs

| API | Description |
|-----|-----|
| [getCameraDevicesList](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCameraDevicesList) | Gets the camera list. |
| [setCurrentCameraDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentCameraDevice) | Sets the camera to use. |
| [getCurrentCameraDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentCameraDevice) | Gets the camera currently in use. |


### Audio device APIs

| API | Description |
|-----|-----|
| [getMicDevicesList](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getMicDevicesList) | Gets the mic list. |
| [getCurrentMicDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDevice) | Gets the mic currently in use. |
| [setCurrentMicDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDevice) | Sets the mic to use. |
| [getCurrentMicDeviceVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDeviceVolume) | Gets the current mic volume. |
| [setCurrentMicDeviceVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDeviceVolume) | Sets the current mic volume. |
| [setCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDeviceMute) | Mutes/Unmutes the current mic. |
| [getCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDeviceMute) | Gets whether the current mic is muted. |
| [getSpeakerDevicesList](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getSpeakerDevicesList) | Gets the speaker list. |
| [getCurrentSpeakerDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerDevice) | Gets the speaker currently in use. |
| [setCurrentSpeakerDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerDevice) | Sets the speaker to use. |
| [getCurrentSpeakerVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerVolume) | Gets the current speaker volume. |
| [setCurrentSpeakerVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerVolume) | Sets the current speaker volume. |
| [setCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerDeviceMute) | Mutes/Unmutes the current speaker. |
| [getCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerDeviceMute) | Gets whether the current speaker is muted. |

### Beauty filter APIs

| API | Description |
|-----|-----|
| [setBeautyStyle](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBeautyStyle) | Sets the strength of the beauty, brightening, and rosy skin filters. |
| [setWaterMark](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setWaterMark) | Sets watermarks. |


### Substream APIs

| API | Description |
|-----|-----|
| [startRemoteSubStreamView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteSubStreamView) | Disused API: starts rendering the substream (screen sharing) image of a remote user. |
| [stopRemoteSubStreamView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopRemoteSubStreamView) | Disused API: stops rendering the substream (screen sharing) image of a remote user. |
| [setRemoteSubStreamViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteSubStreamViewFillMode) | Disused API: sets the rendering mode of substream (screen sharing) images. |
| [setRemoteSubStreamViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteSubStreamViewRotation) | Disused API: sets the clockwise rotation degree of substream (screen sharing) images. |
| [getScreenCaptureSources](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources) | Enumerates shareable windows. |
| [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) | Sets screen sharing parameters. This method can be called during screen sharing. |
| [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) | Starts screen sharing. |
| [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture) | Pauses screen sharing. |
| [resumeScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeScreenCapture) | Resumes screen sharing. |
| [stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture) | Stops screen sharing. |
| [setSubStreamEncoderParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSubStreamEncoderParam) | Sets encoder parameters for substream (screen sharing) images. |
| [setSubStreamMixVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSubStreamMixVolume) | Sets the audio mixing volume of substream (screen sharing) images. |


### Custom message sending APIs

| API | Description |
|-----|-----|
| [sendCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#sendCustomCmdMsg) | Sends a custom message to all users in the room. |
| [sendSEIMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#sendSEIMsg) | Embeds small-volume custom data in video frames. |


### Background audio mixing APIs

| API | Description |
|-----|-----|
| [playBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#playBGM) | Disused API: starts background music. |
| [stopBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopBGM) | Disused API: stops background music. |
| [pauseBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseBGM) | Disused API: pauses background music. |
| [resumeBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeBGM) | Disused API: resumes background music. |
| [getBGMDuration](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getBGMDuration) | Disused API: gets the total length of the background music file, in milliseconds. |
| [setBGMPosition](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPosition) | Disused API: sets the playback progress of background music. |
| [setBGMVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMVolume) | Disused API: sets background music volume. |
| [setBGMPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPlayoutVolume) | Disused API: sets the local playback volume of background music. |
| [setBGMPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPublishVolume) | Disused API: sets the remote playback volume of background music. |
| [startSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSystemAudioLoopback) | Enables system audio capture. Currently, the SDK does not support system audio mixing on macOS or 64-bit Windows. This API can be called only on 32-bit Windows for the time being. |
| [stopSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSystemAudioLoopback) | Disables system audio capture Currently, the SDK does not support system audio mixing on macOS or 64-bit Windows. This API can be called only on 32-bit Windows for the time being. |
| [setSystemAudioLoopbackVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSystemAudioLoopbackVolume) | Sets the system audio capture volume. Currently, the SDK does not support system audio mixing on macOS or 64-bit Windows. This API can be called only on 32-bit Windows for the time being. |
| [startPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPlayMusic) | Starts background music. |
| [stopPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPlayMusic) | Stops background music. |
| [pausePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pausePlayMusic) | Pauses background music. |
| [resumePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumePlayMusic) | Resumes background music. |
| [getMusicDurationInMS](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getMusicDurationInMS) | Gets the total length of the background music file, in milliseconds. |
| [seekMusicToPosInTime](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#seekMusicToPosInTime) | Sets the playback progress of background music. |
| [setAllMusicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllMusicVolume) | Sets background music volume. This API is used to control the playback volume of background music. |
| [setMusicPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPlayoutVolume) | Sets the local playback volume of background music. |
| [setMusicPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPublishVolume) | Sets the remote playback volume of background music. |


### Audio effect APIs

| API | Description |
|-----|-----|
| [playAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#playAudioEffect) | Disused API: plays an audio effect. |
| [setAudioEffectVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioEffectVolume) | Disused API: sets the volume of an audio effect. |
| [stopAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAudioEffect) | Disused API: stops an audio effect. |
| [stopAllAudioEffects](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAllAudioEffects) | Disused API: stops all audio effects. |
| [setAllAudioEffectsVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllAudioEffectsVolume) | Disused API: sets the volume of all audio effects. |
| [pauseAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseAudioEffect) | Disused API: pauses an audio effect. |
| [resumeAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeAudioEffect) | Disused API: resumes an audio effect. |


### Device and network testing APIs

| API | Description |
|-----|-----|
| [startSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeedTest) | Starts network speed testing. This may compromise the quality of video calls and should be avoided during a video call. |
| [stopSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSpeedTest) | Stops server speed testing. |
| [startCameraDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startCameraDeviceTest) | Starts camera testing. |
| [stopCameraDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopCameraDeviceTest) | Stops camera testing. |
| [startMicDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startMicDeviceTest) | Starts mic testing. |
| [stopMicDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopMicDeviceTest) | Stops mic testing. |
| [startSpeakerDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeakerDeviceTest) | Starts speaker testing. |
| [stopSpeakerDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSpeakerDeviceTest) | Stops speaker testing. |


### Log APIs

| API | Description |
|-----|-----|
| [getSDKVersion](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getSDKVersion) | Gets the SDK version. |
| [setLogLevel](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogLevel) | Sets the log output level. |
| [setConsoleEnabled](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setConsoleEnabled) | Enables/Disables console log printing. |
| [setLogCompressEnabled](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogCompressEnabled) | Enables/Disables local log compression. |
| [setLogDirPath](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogDirPath) | Sets the path to save logs. |
| [setLogCallback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogCallback) | Sets the log callback. |
| [callExperimentalAPI](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#callExperimentalAPI) | Calls the experimental API. |


### Disused APIs

| API | Description |
|-----|-----|
| [setMicVolumeOnMixing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMicVolumeOnMixing) | This API has been disused since version 6.9. |


## TRTCCallback @ TXLiteAVSDK

Callback APIs for Tencent Cloud’s video call feature.

### Error and warning event callback APIs

| API | Description |
|-----|-----|
| [onError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onError) | Error callback, which indicates that the SDK encountered an irrecoverable error and must be listened on. The corresponding UI reminders should be displayed based on the actual conditions. |
| [onWarning](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onWarning) | Warning callback. This alerts you to non-serious problems such as lag or recoverable decoding failure. |


### Room event callback APIs

| API | Description |
|-----|-----|
| [onEnterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom) | Callback of room entry |
| [onExitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onExitRoom) | Callback of room exit |
| [onSwitchRole](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRole) | Callback of role switching |
| [onConnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectOtherRoom) | Callback of the result of requesting cross-room co-anchoring (anchor competition) |
| [onDisconnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onDisconnectOtherRoom) | Callback of the result of ending cross-room co-anchoring (anchor competition) |
| [onSwitchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRoom) | Callback of room switching |


### User event callback APIs

| API | Description |
|-----|-----|
| [onRemoteUserEnterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRemoteUserEnterRoom) | Callback of the entry of a user |
| [onRemoteUserLeaveRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRemoteUserLeaveRoom) | Callback of the exit of a user |
| [onUserVideoAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable) | Callback of whether a user has enabled the camera |
| [onUserSubStreamAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserSubStreamAvailable) | Callback of whether a user has started screen sharing |
| [onUserAudioAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable) | Callback of whether a user is sending audio data |
| [onFirstVideoFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onFirstVideoFrame) | Callback of the rendering of the first video frame of the local user or remote users |
| [onFirstAudioFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onFirstAudioFrame) | Callback of the playing of the first audio frame of a remote user. No notifications are sent for local audio |
| [onSendFirstLocalVideoFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSendFirstLocalVideoFrame) | Callback of the sending of the first local video frame |
| [onSendFirstLocalAudioFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSendFirstLocalAudioFrame) | Callback of the sending of the first local audio frame |
| [onUserEnter](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserEnter) | Disused API: callback of the entry of an anchor |
| [onUserExit](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserExit) | Disused API: callback of the exit of an anchor |


### Callback of statistics on quality and technical metrics

| API | Description |
|-----|-----|
| [onNetworkQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onNetworkQuality) | Network quality. This callback is triggered every 2 seconds to collect statistics on the quality of current upstream and downstream data transfer. |
| [onStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStatistics) | Callback of statistics on technical metrics |


### Server event callbacks

| API | Description |
|-----|-----|
| [onConnectionLost](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectionLost) | Callback of the disconnection of the SDK from the server |
| [onTryToReconnect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTryToReconnect) | Callback of the SDK trying to connect to the server again |
| [onConnectionRecovery](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectionRecovery) | Callback of the reconnection of the SDK to the server |
| [onSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSpeedTest) | Callback of server speed test results. The SDK tests the speed of multiple server IPs, and the result of each test is returned through this callback. |


### Hardware event callback APIs

| API | Description |
|-----|-----|
| [onCameraDidReady](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onCameraDidReady) | Callback of the camera being ready |
| [onMicDidReady](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onMicDidReady) | Callback of the mic being ready |
| [onUserVoiceVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVoiceVolume) | Callback of volume, including the volume of each `userId` and the total remote volume |
| [onDeviceChange](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onDeviceChange) | Callback of the connection/disconnection of a local device |
| [onTestMicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTestMicVolume) | Callback of mic testing volume |
| [onTestSpeakerVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTestSpeakerVolume) | Callback of speaker testing volume |
| [onAudioDeviceCaptureVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged) | Callback of volume change of the current audio capture device |
| [onAudioDevicePlayoutVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged) | Callback of volume change of the current audio playback device |


### Custom message receiving callback APIs

| API | Description |
|-----|-----|
| [onRecvCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRecvCustomCmdMsg) | Callback of the receipt of a custom message |
| [onMissCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onMissCustomCmdMsg) | Callback of the missing of a custom message |
| [onRecvSEIMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRecvSEIMsg) | Callback of the receipt of an SEI message |


### Callback APIs for CDN relayed push

| API | Description |
|-----|-----|
| [onStartPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStartPublishing) | Callback of starting to push to Tencent Cloud’s live streaming CDN, which corresponds to the `startPublishing()` API in `TRTCCloud` |
| [onStopPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStopPublishing) | Callback of stopping pushing to Tencent Cloud’s live streaming CDN, which corresponds to the `stopPublishing()` API in `TRTCCloud`. |
| [onStartPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStartPublishCDNStream) | Callback of the completion of starting relayed push to CDNs |
| [onStopPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStopPublishCDNStream) | Callback of the completion of stopping relayed push to CDNs |
| [onSetMixTranscodingConfig](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSetMixTranscodingConfig) | Callback of setting On-Cloud MixTranscoding parameters, which corresponds to the `setMixTranscodingConfig()` API in `TRTCCloud` |


### Audio effect callback API

| API | Description |
|-----|-----|
| [onAudioEffectFinished](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioEffectFinished) | Disused API: callback of ending audio effect playback |


### Screen sharing callback APIs

| API | Description |
|-----|-----|
| [onScreenCaptureCovered](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureCovered) | Callback of screencapturing failure because the target window is covered. This callback can be used to prompt users to move the window. |
| [onScreenCaptureStarted](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureStarted) | Callback of starting screen sharing |
| [onScreenCapturePaused](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCapturePaused) | Callback of pausing screen sharing |
| [onScreenCaptureResumed](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureResumed) | Callback of resuming screen sharing |
| [onScreenCaptureStopped](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureStopped) | Callback of stopping screen sharing |


### Screenshot callback API

| API | Description |
|-----|-----|
| [onSnapshotComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSnapshotComplete) | Callback of the completion of a screenshot |


### Background music callbacks APIs

| API | Description |
|-----|-----|
| [onPlayBGMBegin](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMBegin) | Disused API: callback of starting background music |
| [onPlayBGMProgress](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMProgress) | Disused API: callback of the playback progress of background music |
| [onPlayBGMComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMComplete) | Disused API: callback of ending background music playback |


## Definitions of Key Classes

### Key classes

| Class | Description |
|-----|-----|
| [TRTCParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCParams.html)| Room entry parameters |
| [TRTCVideoEncParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCVideoEncParam.html) | Video encoding parameters |
| [TRTCNetworkQosParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCNetworkQosParam.html) | QoS control parameters |
| [TRTCQualityInfo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCQualityInfo.html)| Video quality |
| [TRTCVolumeInfo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCVolumeInfo.html) | Volume |
| [TRTCSpeedTestResult](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCSpeedTestResult.html)| Network speed testing result |
| [TRTCMixUser](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCMixUser.html)| Position of the image of each channel in On-Cloud MixTranscoding |
| [TRTCTranscodingConfig](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCTranscodingConfig.html)| On-Cloud MixTranscoding configuration |
| [TRTCPublishCDNParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCPublishCDNParam.html)| CDN relayed push parameters |
| [TRTCAudioRecordingParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCAudioRecordingParams.html)| Audio recording parameters |
| [TRTCLocalStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCLocalStatistics.html)| Local audio/video statistics |
| [TRTCRemoteStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCRemoteStatistics.html) | Remote audio/video statistics |
| [TRTCStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCStatistics.html)| Statistics |

### Enumerated values

| Enumerated Value | Description |
|-----|-----|
| [TRTCVideoResolution](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolution)| Video resolution |
| [TRTCVideoResolutionMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoResolutionMode)| Video resolution mode |
| [TRTCVideoStreamType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoStreamType) | Video stream type |
| [TRTCQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCQuality)| Image quality |
| [TRTCVideoFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoFillMode)| Video image fill mode |
| [TRTCBeautyStyle](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCBeautyStyle) | Beauty filter (skin smoothing) algorithm |
| [TRTCAppScene](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCAppScene)| Application scenario |
| [TRTCRoleType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCRoleType)| Role, which applies only to live streaming scenarios (`TRTCAppSceneLIVE`). |
| [TRTCQosControlMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCQosControlMode)| QoS control mode |
| [TRTCVideoQosPreference](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoQosPreference)| Image quality preference |
| [TRTCDeviceState](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCDeviceState)| Device operation |
| [TRTCDeviceType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCDeviceType)| Device type |
| [TRTCWaterMarkSrcType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCWaterMarkSrcType)| Watermark source type |
| [TRTCTranscodingConfigMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCTranscodingConfigMode)| Configuration mode for stream mixing parameters |
