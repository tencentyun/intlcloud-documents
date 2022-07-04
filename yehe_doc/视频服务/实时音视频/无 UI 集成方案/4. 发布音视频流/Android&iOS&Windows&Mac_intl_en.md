This document describes how an anchor publishes audio/video streams. "Publishing" refers to turning on the mic and camera to make the audio heard and video seen by other users in the room.

![](https://qcloudimg.tencent-cloud.cn/raw/3f49218df6a0cc1a106f9a61c23fdb98.png)
## Call Guide

[](id:step1)
### Step 1. Perform prerequisite steps

Import the SDK and configure the application permissions as instructed in [iOS](https://intl.cloud.tencent.com/document/product/647/35092).

[](id:step2)

### Step 2. Enable camera preview
You can call the **startLocalPreview** API to enable camera preview. The SDK will request camera permission from the system. Camera images can be captured only after the permission is granted.

You can call the **setLocalRenderParams** API to set rendering parameters for the local preview. Playback may be choppy if rendering parameters are set after preview is enabled, so if you want to set rendering parameters, we recommend you call this API before enabling preview.

You can call the **TXDeviceManager** API to switch between the front and rear cameras, set the focus mode, and turn the flash on/off.

You can adjust the beauty filter effect and image quality as instructed in [Setting Image Quality](https://intl.cloud.tencent.com/document/product/647/35153).

<dx-codeblock>
::: Android  java
// Set the preview mode of the local video image: Enable horizontal mirroring and set the fill mode for the video image
TRTCCloudDef.TRTCRenderParams param = new TRTCCloudDef.TRTCRenderParams();
param.fillMode   = TRTCCloudDef.TRTC_VIDEO_RENDER_MODE_FILL;
param.mirrorType = TRTCCloudDef.TRTC_VIDEO_MIRROR_TYPE_AUTO;
mCloud.setLocalRenderParams(param);

// Enable local camera preview (`localCameraVideo` is the control used to render the local video image)
TXCloudVideoView cameraVideo = findViewById(R.id.txcvv_main_local);
mCloud.startLocalPreview(true, cameraVideo);

// Use `TXDeviceManager` to enable autofocus and turn on the flash
TXDeviceManager manager = mCloud.getDeviceManager();
if (manager.isAutoFocusEnabled()) {
    manager.enableCameraAutoFocus(true);
}
manager.enableCameraTorch(true);
:::
::: iOS  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// Set the preview mode of the local video image: Enable horizontal mirroring and set the fill mode for the video image
TRTCRenderParams *param = [[TRTCRenderParams alloc] init];
param.fillMode   = TRTCVideoFillMode_Fill;
param.mirrorType = TRTCVideoMirrorTypeAuto;
[self.trtcCloud setLocalRenderParams:param];

// Enable local camera preview (`localCameraVideoView` is the control used to render the local video image)
[self.trtcCloud startLocalPreview:YES view:localCameraVideoView];

// Use `TXDeviceManager` to enable autofocus and turn on the flash
TXDeviceManager *manager = [self.trtcCloud getDeviceManager];
if ([manager isAutoFocusEnabled]) {
    [manager enableCameraAutoFocus:YES];
}
[manager enableCameraTorch:YES];
:::
::: Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// Set the preview mode of the local video image: Enable horizontal mirroring and set the fill mode for the video image
TRTCRenderParams *param = [[TRTCRenderParams alloc] init];
param.fillMode   = TRTCVideoFillMode_Fill;
param.mirrorType = TRTCVideoMirrorTypeAuto;
[self.trtcCloud setLocalRenderParams:param];

// Enable local camera preview (`localCameraVideoView` is the control used to render the local video image)
[self.trtcCloud startLocalPreview:localCameraVideoView];
:::
::: Windows  C++
// Set the preview mode of the local video image: Enable horizontal mirroring and set the fill mode for the video image
liteav::TRTCRenderParams render_params;
render_params.mirrorType = liteav::TRTCVideoMirrorType_Enable;
render_params.fillMode = TRTCVideoFillMode_Fill;
trtc_cloud_->setLocalRenderParams(render_params);

// Enable local camera preview (`view` is the control handle used to render the local video image)
liteav::TXView local_view = (liteav::TXView)(view);
trtc_cloud_->startLocalPreview(local_view);
:::
</dx-codeblock>


[](id:step3)
### Step 3. Enable mic capture
You can call **startLocalAudio** to start mic capture. You need to specify the `quality` parameter when calling the API to set the capturing mode. A higher quality isn't necessarily better. You need to set an appropriate quality based on your business scenario.

- **SPEECH**
In this mode, the SDK audio module is dedicated to capturing audio signals and filtering environmental noise as much as possible. In addition, the audio data in this mode has the highest immunity to a poor network quality. Therefore, it is especially suitable for scenarios highlighting audio communication, such as video calls and online meetings.
- **MUSIC**
In this mode, the SDK uses a high audio processing bandwidth and stereo mode to maximize the capture quality while adjusting the audio DSP module to the lowest level, so as to deliver the best audio quality possible. Therefore, it is suitable for music live streaming scenarios, especially where an anchor uses a professional sound card to live stream music.
- **DEFAULT**
In this mode, the SDK uses the smart recognition algorithm to recognize the current environment and selects the most appropriate processing mode accordingly. However, the recognition algorithm may sometimes be inaccurate. If you are very familiar with the use cases of your product, we recommend you select `SPEECH` or `MUSIC` for better audio communication or music quality.

<dx-codeblock>
::: Android  java
// Enable mic capture and set `quality` to `SPEECH` (it has a high noise suppression and strong immunity to poor network conditions)
mCloud.startLocalAudio(TRTCCloudDef.TRTC_AUDIO_QUALITY_SPEECH );

// Enable mic capture and set `quality` to `MUSIC` (it captures high fidelity audio with minimum audio quality loss, and is recommended to be used with a professional sound card)
mCloud.startLocalAudio(TRTCCloudDef.TRTC_AUDIO_QUALITY_MUSIC);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// Enable mic capture and set `quality` to `SPEECH` (it has a high noise suppression and strong immunity to poor network conditions)
[self.trtcCloud startLocalAudio:TRTCAudioQualitySpeech];

// Enable mic capture and set `quality` to `MUSIC` (it captures high fidelity audio with minimum audio quality loss, and is recommended to be used with a professional sound card)
[self.trtcCloud startLocalAudio:TRTCAudioQualityMusic];
:::
::: Windows  C++
// Enable mic capture and set `quality` to `SPEECH` (it has a high noise suppression and strong immunity to poor network conditions)
trtc_cloud_->startLocalAudio(TRTCAudioQualitySpeech);

// Enable mic capture and set `quality` to `MUSIC` (it captures high fidelity audio with minimum audio quality loss, and is recommended to be used with a professional sound card)
trtc_cloud_->startLocalAudio(TRTCAudioQualityMusic);
:::
</dx-codeblock>

[](id:step4)
### Step 4. Enter a TRTC room

Make the current user enter a TRTC room as instructed in [Entering a Room](https://intl.cloud.tencent.com/document/product/647/47645). The SDK will start publishing an audio stream to remote users upon a successful room entry.

>! You can enable camera preview and mic capture after room entry (`enterRoom`), but in live streaming scenarios, you need to leave a certain amount of time for the anchor to test the mic and adjust the beauty filters; therefore, it is more common to turn on the camera and mic first and then enter a room.

<dx-codeblock>
::: Android  java
mCloud = TRTCCloud.sharedInstance(getApplicationContext());
mCloud.setListener(mTRTCCloudListener);

// Assemble TRTC room entry parameters. Replace the field values in `TRTCParams` with your own parameter values
// Replace each field in TRTCParams with your own parameters
TRTCCloudDef.TRTCParams param = new TRTCCloudDef.TRTCParams();
params.sdkAppId = 1400000123;  // Replace with your own SDKAppID
params.userId = "denny";       // Replace with your own user ID  
params.roomId = 123321;        // Replace with your own room number
params.userSig = "xxx";        // Replace with your own userSig
params.role = TRTCCloudDef.TRTCRoleAnchor;

// If your scenario is live streaming, set the application scenario to `TRTC_APP_SCENE_LIVE`
// If your application scenario is a group video call, use "TRTC_APP_SCENE_LIVE"
mCloud.enterRoom(param, TRTCCloudDef.TRTC_APP_SCENE_LIVE);        
:::

::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
self.trtcCloud.delegate = self;

// Assemble TRTC room entry parameters. Replace the field values in `TRTCParams` with your own parameter values
// Replace each field in TRTCParams with your own parameters
TRTCParams *params = [[TRTCParams alloc] init];
params.sdkAppId = 1400000123;  // Replace with your own SDKAppID
params.roomId = 123321; // Replace with your own room number
params.userId = @"denny";   // Replace with your own userid  
params.userSig = @"xxx"; // Replace with your own userSig
params.role = TRTCRoleAnchor;

// If your scenario is live streaming, set the application scenario to `TRTC_APP_SCENE_LIVE`
// If your application scenario is a group video call, use "TRTC_APP_SCENE_LIVE"
[self.trtcCloud enterRoom:params appScene:TRTCAppSceneLIVE];
:::

::: Windows  C++
trtc_cloud_ = getTRTCShareInstance();

// Assemble TRTC room entry parameters. Replace the field values in `TRTCParams` with your own parameter values
// Replace each field in TRTCParams with your own parameters
liteav::TRTCParams params;
params.sdkAppId = 1400000123;  // Replace with your own SDKAppID
params.userId = "denny";       // Replace with your own user ID  
params.roomId = 123321;        // Replace with your own room number
params.userSig = "xxx";        // Replace with your own userSig
params.role = TRTCCloudDef.TRTCRoleAnchor;

// If your scenario is live streaming, set the application scenario to `TRTC_APP_SCENE_LIVE`
// If your application scenario is a group video call, use "TRTC_APP_SCENE_LIVE"
trtc_cloud_->enterRoom(params, liteav::TRTCAppSceneLIVE);
:::
</dx-codeblock>


[](id:step5)
### Step 5. Switch the role

**Role in TRTC**
- In video call (`TRTC_APP_SCENE_VIDEOCALL`) and audio call (`TRTC_APP_SCENE_AUDIOCALL`) scenarios, you don't need to set the role when entering a room, as each user is an anchor by default in these two scenarios.
- In video live streaming (`TRTC_APP_SCENE_LIVE`) and audio live streaming (`TRTC_APP_SCENE_VOICE_CHATROOM`) scenarios, each user needs to set their own role to anchor or audience when entering a room.

**Role switch**
In TRTC, only anchors can publish audio/video streams.
Therefore, if you set the role to audience when entering a room, you need to call the **switchRole** API first to switch the role to anchor before publishing audio/video streams. This process is the so-called "mic-on".

<dx-codeblock>
::: Android java
// If your current role is audience, you need to call `switchRole` first to switch to anchor
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
mCloud.switchRole(TRTCCloudDef.TRTCRoleAnchor);
mCloud.startLocalAudio(TRTCCloudDef.TRTC_AUDIO_QUALITY_DEFAULT);
mCloud.startLocalPreview(true, cameraVide);

// If role switch failed, the error code of the `onSwitchRole` callback is not `0`
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
@Override
public void onSwitchRoom(final int errCode, final String errMsg) {
    if (errCode != 0) {
        Log.d(TAG, "Switching operation failed...");
    }   
}
:::
::: iOS ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// If your current role is audience, you need to call `switchRole` first to switch to anchor
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
[self.trtcCloud switchRole:TRTCRoleAnchor];
[self.trtcCloud startLocalAudio:TRTCAudioQualityDefault];
[self.trtcCloud startLocalPreview:YES view:localCameraVideoView];

// If role switch failed, the error code of the `onSwitchRole` callback is not `0`
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
- (void)onSwitchRoom:(TXLiteAVError)errCode errMsg:(nullable NSString *)errMsg {
    if (errCode != 0) {
        NSLog(@"Switching operation failed... ");
    }   
}
:::
::: Mac ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// If your current role is audience, you need to call `switchRole` first to switch to anchor
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
[self.trtcCloud switchRole:TRTCRoleAnchor];
[self.trtcCloud startLocalAudio:TRTCAudioQualityDefault];
[self.trtcCloud startLocalPreview:localCameraVideoView];

// If role switch failed, the error code of the `onSwitchRole` callback is not `0`
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
- (void)onSwitchRoom:(TXLiteAVError)errCode errMsg:(nullable NSString *)errMsg {
    if (errCode != 0) {
        NSLog(@"Switching operation failed... ");
    }   
}
:::
::: Windows C++
// If your current role is audience, you need to call `switchRole` first to switch to anchor
// If your current role is 'audience', you need to call switchRole to switch to 'anchor' first
trtc_cloud_->switchRole(liteav::TRTCRoleAnchor);
trtc_cloud_->startLocalAudio(TRTCAudioQualityDefault);
trtc_cloud_->startLocalPreview(hWnd);

// If role switch failed, the error code of the `onSwitchRole` callback is not `ERR_NULL` (i.e., 0)
// If switching operation failed, the error code of the 'onSwitchRole' is not zero
void onSwitchRoom(TXLiteAVError errCode, const char* errMsg) {
    if (errCode != ERR_NULL) {
        printf("Switching operation failed...");
    }
}
:::
</dx-codeblock>

**Note:** If there are too many anchors in a room, `switchRole` will fail, and TRTC will notify you of the error code through `onSwitchRole`. Therefore, if you no longer want to publish audio/video streams, you need to call `switchRole` again to switch to audience. This process is the so-called "mic-off".

>? Only an anchor can publish audio/video streams, but you cannot make each user enter the room as an anchor. For the specific reason, see [1. How many concurrent audio/video streams can a room have at most?](#speed1).

## Advanced Guide

[](id:speed1)
### 1. How many concurrent audio/video streams can a room have at most?
A TRTC room can have up to **50** concurrent audio/video streams. When the number of streams reaches 50, additional streams will be automatically dropped.
With proper **role management**, 50 concurrent audio/video streams can meet the needs of most scenarios, from a one-to-one video call to live streams watched by tens of thousands of users.

"Role management" refers to how roles are assigned to users entering a room.
- If a user is an anchor in live streaming, a teacher in online education, or a host in an online meeting, they can be assigned the anchor role.
- If a user is a live stream viewer, a student in online education, or an attendee in an online meeting, they should be assigned the audience role; otherwise, the room will quickly reach the maximum number of anchors.

When an audience member wants to publish an audio/video stream (mic on), they need to be switched to the anchor role through `switchRole`. When they no longer want to publish their audio/video streams (mic off), they need to be switched back to the audience role immediately.

With appropriate role management, generally no more than 50 anchors in a room need to publish audio/video streams concurrently. If a room contains more than six anchors, audience members will find it difficult to distinguish between speakers who are speaking at the same time.









