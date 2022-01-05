## TRTCCloud @ TXLiteAVSDK

TRTC main API classes

- **Documentation**: [TRTC SDK for Electron](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/index.html)
- **Sample code**: [TRTC Electron Demo](https://github.com/tencentyun/TRTCSDK/tree/master/Electron)

### Creating TRTC object
```js
const TRTCCloud = require('trtc-electron-sdk').default;
// import TRTCCloud from 'trtc-electron-sdk';
this.rtcCloud = new TRTCCloud();
```

Since v7.9.348, the TRTC SDK for Electron has integrated `trtc.d.ts` for developers using TypeScript.

```javascript
import TRTCCloud from 'trtc-electron-sdk';

const rtcCloud: TRTCCloud = new TRTCCloud();
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

### `TRTCCloud` singleton creation and termination APIs

| API                                             | Description                                                         |
|-----|-----|
| [getTRTCShareInstance](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#.getTRTCShareInstance) | Creates a [TRTCCloud](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html) singleton object during dynamic DLL loading. |
| [destroyTRTCShareInstance](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#.destroyTRTCShareInstance) | Releases a [TRTCCloud](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html) singleton object and frees up resources. |

### Room APIs

| API                                             | Description                                                         |
|-----|-----|
| [enterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enterRoom) | Enters a room. If the room does not exist, the system will create one automatically. |
| [exitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#exitRoom) | Leaves a room. |
| [switchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRoom) | Switches rooms. |
| [switchRole](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRole) | Switches roles. This API applies only to the live streaming modes (`TRTCAppSceneLIVE` and `TRTCAppSceneVoiceChatRoom`). |
| [connectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#connectOtherRoom) | Requests a cross-room call (anchor competition). |
| [disconnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#disconnectOtherRoom)| Ends a cross-room call (anchor competition). |
| [setDefaultStreamRecvMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setDefaultStreamRecvMode) | Sets the audio/video receiving mode (must be called before room entry to take effect). |


### CDN APIs

| API                                             | Description                                                         |
|-----|-----|
| [startPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPublishing) | Starts publishing to Tencent Cloud’s live streaming CDN. |
| [stopPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPublishing) | Stops publishing to Tencent Cloud’s live streaming CDN. |
| [startPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPublishCDNStream) | Starts relaying to the live streaming CDN of a non-Tencent Cloud vendor. |
| [stopPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPublishCDNStream) | Stops relaying to the live streaming CDN of a non-Tencent Cloud vendor. |
| [setMixTranscodingConfig](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMixTranscodingConfig) | Sets On-Cloud MixTranscoding parameters. |


### Video APIs

| API                                             | Description                                                         |
|-----|-----|
| [startLocalPreview](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalPreview) | Enables capturing and preview of the local camera. |
| [stopLocalPreview](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopLocalPreview) | Disables capturing and preview of the local camera. |
| [muteLocalVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalVideo) | Blocks/Unblocks local video. |
| [startRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteView) | Starts playing the video of a remote user. |
| [stopRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopRemoteView) | Stops playing and pulling the video of a remote user. |
| [stopAllRemoteView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAllRemoteView) | Stops playing and pulling the videos of all remote users. |
| [muteRemoteVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteVideoStream) | Pauses/Resumes receiving the video of a specified remote user. |
| [muteAllRemoteVideoStreams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteAllRemoteVideoStreams) | Pauses/Resumes receiving the videos of all remote users. |
| [setVideoEncoderParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderParam) | Sets video encoder parameters. |
| [setNetworkQosParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setNetworkQosParam) | Sets video preference. |
| [setLocalRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalRenderParams) | Sets rendering parameters for the local image (primary stream). |
| [setLocalViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewFillMode) | Sets the rendering mode of the local image (disused). |
| [setRemoteRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParams) | Sets rendering parameters for a remote image. |
| [setRemoteViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteViewFillMode) | Sets the rendering mode of a remote image (disused). |
| [setLocalViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewRotation) | Sets the clockwise rotation of the local image (disused). |
| [setRemoteViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteViewRotation) | Sets the clockwise rotation of a remote image (disused). |
| [setVideoEncoderRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderRotation) | Sets the rotation of encoded video images, i.e., images presented to remote users and recorded by the server. |
| [setLocalViewMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewMirror) | Sets the mirror mode of the local camera's preview image (disused). |
| [setVideoEncoderMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setVideoEncoderMirror) | Sets the mirror mode of encoded images. |
| [enableSmallVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enableSmallVideoStream) | Enables/Disables the dual-channel (big and small images) encoding mode. |
| [setRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteVideoStreamType) | Sets whether to view the big or small image of a specified user (`userId`). |
| [setPriorRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setPriorRemoteVideoStreamType) | Sets video quality preference for audience (disused). |
| [snapshotVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#snapshotVideo) | Takes a video screenshot. |


### Audio APIs

| API                                             | Description                                                         |
|-----|-----|
| [startLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startLocalAudio) | Enables local audio capturing and publishing. |
| [stopLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopLocalAudio) | Disables local audio capturing and publishing. |
| [muteLocalAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalAudio) | Mutes/Unmutes the local user. |
| [muteRemoteAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteAudio) | Mutes a remote user and stops pulling the user’s audio. |
| [muteAllRemoteAudio](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteAllRemoteAudio) | Mutes all remote users and stops pulling their audio. |
| [setAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioCaptureVolume) | Sets the SDK capturing volume. |
| [getAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getAudioCaptureVolume) | Gets the SDK capturing volume. |
| [setAudioPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioPlayoutVolume) | Sets the SDK playback volume. |
| [getAudioPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getAudioPlayoutVolume) | Gets the SDK playback volume. |
| [enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#enableAudioVolumeEvaluation) | Enables/Disables the volume reminder. |
| [startAudioRecording](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startAudioRecording) | Starts audio recording. |
| [stopAudioRecording](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAudioRecording) | Stops audio recording. |
| [setAudioQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioQuality) | Sets audio quality (disused). |
| [setRemoteAudioVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteAudioVolume) | Sets the playback volume of a remote user. |


### Camera APIs

| API                                             | Description                                                         |
|-----|-----|
| [getCameraDevicesList](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCameraDevicesList) | Gets the camera list. |
| [setCurrentCameraDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentCameraDevice) | Sets the camera to use. |
| [getCurrentCameraDevice](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentCameraDevice) | Gets the camera currently in use. |


### Audio device APIs

| API                                             | Description                                                         |
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

| API                                             | Description                                                         |
|-----|-----|
| [setBeautyStyle](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBeautyStyle) | Sets the strength of the beauty, skin brightening, and rosy skin filters. |
| [setWaterMark](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setWaterMark) | Sets the watermark. |


### Substream APIs

| API                                             | Description                                                         |
|-----|-----|
| [startRemoteSubStreamView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startRemoteSubStreamView) | Starts rendering the substream (screen sharing) image of a remote user (disused). |
| [stopRemoteSubStreamView](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopRemoteSubStreamView) | Stops rendering the substream (screen sharing) image of a remote user (disused). |
| [setRemoteSubStreamViewFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteSubStreamViewFillMode) | Sets the rendering mode of substream (screen sharing) images (disused). |
| [setRemoteSubStreamViewRotation](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteSubStreamViewRotation) | Sets the clockwise rotation of substream (screen sharing) images (disused). |
| [getScreenCaptureSources](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources) | Enumerates shareable sources. |
| [selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget) | Sets screen sharing parameters. This API can be called during screen sharing. |
| [startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture) | Starts screen sharing. |
| [pauseScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseScreenCapture) | Pauses screen sharing. |
| [resumeScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeScreenCapture) | Resumes screen sharing. |
| [stopScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopScreenCapture) | Stops screen sharing. |
| [setSubStreamEncoderParam](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSubStreamEncoderParam) | Sets encoder parameters for substream (screen sharing) images. |
| [setSubStreamMixVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSubStreamMixVolume) | Sets the audio mixing volume of substream (screen sharing) video. |
| [addExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#addExcludedShareWindow) | Adds a specified window to the exclusion list of screen sharing. Windows in the list will not be shared.|
| [removeExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeExcludedShareWindow) | Removes a specified window from the exclusion list of screen sharing.|
| [removeAllExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeAllExcludedShareWindow) | Removes all windows from the exclusion list of screen sharing.|


### Custom message sending APIs

| API                                             | Description                                                         |
|-----|-----|
| [sendCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#sendCustomCmdMsg) | Sends a custom message to all users in a room. |
| [sendSEIMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#sendSEIMsg) | Embeds small-volume custom data into video frames. |


### Background music mixing APIs

| API                                             | Description                                                         |
|-----|-----|
| [playBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#playBGM) | Starts background music (disused). |
| [stopBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopBGM) | Stops background music (disused). |
| [pauseBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseBGM) | Pauses background music (disused). |
| [resumeBGM](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeBGM) | Resumes background music (disused). |
| [getBGMDuration](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getBGMDuration) | Gets the total length of the background music file, in milliseconds (disused). |
| [setBGMPosition](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPosition) | Sets the playback progress of background music (disused). |
| [setBGMVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMVolume) | Sets background music volume (disused). |
| [setBGMPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPlayoutVolume) | Sets the local playback volume of background music (disused). |
| [setBGMPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setBGMPublishVolume) | Sets the remote playback volume of background music (disused). |
| [startSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSystemAudioLoopback) | Enables system audio capturing. |
| [stopSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSystemAudioLoopback) | Disables system audio capturing. |
| [setSystemAudioLoopbackVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setSystemAudioLoopbackVolume) | Sets system audio capturing volume. |
| [startPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPlayMusic) | Starts background music. |
| [stopPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPlayMusic) | Stops background music. |
| [pausePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pausePlayMusic) | Pauses background music. |
| [resumePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumePlayMusic) | Resumes background music. |
| [getMusicDurationInMS](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getMusicDurationInMS) | Gets the total length of the background music file, in milliseconds. |
| [seekMusicToPosInTime](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#seekMusicToPosInTime) | Sets the playback progress of background music. |
| [setAllMusicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllMusicVolume) | Sets background music volume. This API is used to control the audio mixing volume of background music. |
| [setMusicPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPlayoutVolume) | Sets the local playback volume of background music. |
| [setMusicPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPublishVolume) | Sets the remote playback volume of background music. |


### Audio effect APIs

| API                                             | Description                                                         |
|-----|-----|
| [playAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#playAudioEffect) | Plays an audio effect (disused). |
| [setAudioEffectVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioEffectVolume) | Sets the volume of an audio effect (disused). |
| [stopAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAudioEffect) | Stops an audio effect (disused). |
| [stopAllAudioEffects](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopAllAudioEffects) | Stops all audio effects (disused). |
| [setAllAudioEffectsVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllAudioEffectsVolume) | Sets the volume of all audio effects (disused). |
| [pauseAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pauseAudioEffect) | Pauses an audio effect (disused). |
| [resumeAudioEffect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumeAudioEffect) | Resumes an audio effect (disused). |


### Device and network testing APIs

| API                                             | Description                                                         |
|-----|-----|
| [startSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeedTest) | Starts network speed testing. This may compromise the quality of video calls and should be avoided during a video call. |
| [stopSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSpeedTest) | Stops network speed testing. |
| [startCameraDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startCameraDeviceTest) | Starts camera test. |
| [stopCameraDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopCameraDeviceTest) | Stops camera test. |
| [startMicDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startMicDeviceTest) | Starts mic testing. |
| [stopMicDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopMicDeviceTest) | Stops mic test. |
| [startSpeakerDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeakerDeviceTest) | Starts speaker testing. |
| [stopSpeakerDeviceTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopSpeakerDeviceTest) | Stops speaker test. |


### Log APIs

| API                                             | Description                                                         |
|-----|-----|
| [getSDKVersion](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getSDKVersion) | Gets the SDK version. |
| [setLogLevel](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogLevel) | Sets the log output level. |
| [setConsoleEnabled](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setConsoleEnabled) | Enables/Disables console log printing. |
| [setLogCompressEnabled](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogCompressEnabled) | Enables/Disables local log compression. |
| [setLogDirPath](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogDirPath) | Sets the path to save logs. |
| [setLogCallback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLogCallback) | Sets the log callback. |
| [callExperimentalAPI](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#callExperimentalAPI) | Calls the experimental API. |


### Disused APIs

| API                                             | Description                                                         |
|-----|-----|
| [setMicVolumeOnMixing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMicVolumeOnMixing) | This API has been disused since v6.9. |


## TRTCCallback @ TXLiteAVSDK

TRTC callback API classes

### Error and warning event callback APIs

| API                                             | Description                                                         |
|-----|-----|
| [onError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onError) | Error callback. This indicates that the SDK encountered an unrecoverable error. Such errors must be listened for, and UI messages should be sent to users if necessary. |
| [onWarning](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onWarning) | Warning callback. This alerts you to non-serious problems such as stutter or recoverable decoding failure. |


### Room event callback APIs

| API                                             | Description                                                         |
|-----|-----|
| [onEnterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoom) | Callback for room entry |
| [onExitRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onExitRoom) | Callback for room exit |
| [onSwitchRole](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRole) | Callback for role switching |
| [onConnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectOtherRoom) | Callback of the result of requesting a cross-room call (anchor competition) |
| [onDisconnectOtherRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onDisconnectOtherRoom) | Callback of the result of ending a cross-room call (anchor competition) |
| [onSwitchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRoom) | Callback for room switching |


### User event callback APIs

| API                                             | Description                                                         |
|-----|-----|
| [onRemoteUserEnterRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRemoteUserEnterRoom) | Callback for the entry of a user |
| [onRemoteUserLeaveRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRemoteUserLeaveRoom) | Callback for the exit of a user |
| [onUserVideoAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVideoAvailable) | Whether camera is enabled for video. |
| [onUserSubStreamAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserSubStreamAvailable) | Callback of whether a user has started screen sharing |
| [onUserAudioAvailable](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserAudioAvailable) | Callback of whether a user is sending audio data |
| [onFirstVideoFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onFirstVideoFrame) | Callback for rendering the first video frame of the local user or a remote user |
| [onFirstAudioFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onFirstAudioFrame) | Callback for playing the first audio frame of a remote user. No notifications are sent for local audio. |
| [onSendFirstLocalVideoFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSendFirstLocalVideoFrame) | Callback for sending the first local video frame |
| [onSendFirstLocalAudioFrame](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSendFirstLocalAudioFrame) | Callback for sending the first local audio frame |
| [onUserEnter](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserEnter) | Callback for the entry of an anchor (disused) |
| [onUserExit](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserExit) | Callback for the exit of an anchor (disused) |


### Callback APIs for statistics on network quality and technical metrics

| API                                             | Description                                                         |
|-----|-----|
| [onNetworkQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onNetworkQuality) | Network quality. This callback is triggered every 2 seconds to collect statistics on the quality of current upstream and downstream data transfer. |
| [onStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStatistics) | Callback of statistics on technical metrics |


### Server event callback APIs

| API                                             | Description                                                         |
|-----|-----|
| [onConnectionLost](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectionLost) | Callback for the disconnection of the SDK from the server |
| [onTryToReconnect](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTryToReconnect) | Callback for the SDK trying to reconnect to the server |
| [onConnectionRecovery](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onConnectionRecovery) | Callback for the reconnection of the SDK to the server |
| [onSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSpeedTest) | Callback of server speed test results. The SDK tests the speed of multiple server addresses, and the result of each test is returned through this callback. |


### Hardware event callback APIs

| API                                             | Description                                                         |
|-----|-----|
| [onCameraDidReady](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onCameraDidReady) | Callback for the camera being ready |
| [onMicDidReady](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onMicDidReady) | Callback for the mic being ready |
| [onUserVoiceVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onUserVoiceVolume) | Callback of volume, including the volume of each user (`userId`) and the total remote volume |
| [onDeviceChange](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onDeviceChange) | Callback for the connection/disconnection of a local device |
| [onTestMicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTestMicVolume) | Volume callback for mic testing |
| [onTestSpeakerVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onTestSpeakerVolume) | Volume callback for speaker testing |
| [onAudioDeviceCaptureVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged) | Callback for volume change of the current audio capturing device |
| [onAudioDevicePlayoutVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged) | Callback for volume change of the current audio playback device |


### Custom message receiving callback APIs

| API                                             | Description                                                         |
|-----|-----|
| [onRecvCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRecvCustomCmdMsg) | Callback for receiving a custom message |
| [onMissCustomCmdMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onMissCustomCmdMsg) | Callback for losing a custom message |
| [onRecvSEIMsg](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onRecvSEIMsg) | Callback for receiving an SEI message |


### Callback APIs for CDN relayed push

| API                                             | Description                                                         |
|-----|-----|
| [onStartPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStartPublishing) | Callback for starting publishing to Tencent Cloud’s live streaming CDN. This callback is triggered by the `startPublishing()` API in `TRTCCloud`. |
| [onStopPublishing](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStopPublishing) | Callback for stopping publishing to Tencent Cloud’s live streaming CDN. This callback is triggered by the `stopPublishing()` API in `TRTCCloud`. |
| [onStartPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStartPublishCDNStream) | Callback for starting relayed push to CDNs |
| [onStopPublishCDNStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStopPublishCDNStream) | Callback for stopping relayed push to CDNs |
| [onSetMixTranscodingConfig](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSetMixTranscodingConfig) | Callback for setting On-Cloud MixTranscoding parameters. This callback is triggered by the `setMixTranscodingConfig()` API in `TRTCCloud`. |

### Callback APIs for system audio capturing
| API                                             | Description                                                         |
|-----|-----|
| [onSystemAudioLoopbackError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSystemAudioLoopbackError) | Callback of the system audio capturing result (only for macOS) |

### Audio effect callback APIs

| API                                             | Description                                                         |
|-----|-----|
| [onAudioEffectFinished](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioEffectFinished) | Callback for the end of an audio effect (disused) |

### Screen sharing callback APIs

| API                                             | Description                                                         |
|-----|-----|
| [onScreenCaptureCovered](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureCovered) | Callback for the screen sharing window being covered. You can prompt users to move the window in this callback. |
| [onScreenCaptureStarted](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureStarted) | Callback for starting screen sharing |
| [onScreenCapturePaused](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCapturePaused) | Callback for pausing screen sharing |
| [onScreenCaptureResumed](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureResumed) | Callback for resuming screen sharing |
| [onScreenCaptureStopped](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onScreenCaptureStopped) | Callback for stopping screen sharing |


### Screenshot callback API

| API                                             | Description                                                         |
|-----|-----|
| [onSnapshotComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSnapshotComplete) | Callback for completing a screenshot |


### Background music callback APIs

| API                                             | Description                                                         |
|-----|-----|
| [onPlayBGMBegin](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMBegin) | Callback for starting background music (disused) |
| [onPlayBGMProgress](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMProgress) | Callback of the playback progress of background music (disused) |
| [onPlayBGMComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onPlayBGMComplete) | Callback for the end of background music (disused) |


## Definitions of Key Types

### Key types

| Type | Description |
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
| [TRTCQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCQuality)| Video quality |
| [TRTCVideoFillMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoFillMode)| Video image fill mode |
| [TRTCBeautyStyle](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCBeautyStyle) | Beauty filter (skin smoothing) algorithm |
| [TRTCAppScene](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCAppScene)| Application scenario |
| [TRTCRoleType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCRoleType)| Role, which applies only to live streaming scenarios (`TRTCAppSceneLIVE`) |
| [TRTCQosControlMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCQosControlMode)| QoS control mode |
| [TRTCVideoQosPreference](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoQosPreference)| Video quality preference |
| [TRTCDeviceState](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCDeviceState)| Device operation |
| [TRTCDeviceType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCDeviceType)| Device type |
| [TRTCWaterMarkSrcType](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCWaterMarkSrcType)| Watermark source type |
| [TRTCTranscodingConfigMode](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCTranscodingConfigMode)| Configuration mode for stream mixing parameters |
