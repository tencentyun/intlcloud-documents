This document describes how to subscribe to the audio/video streams of another user in the room, i.e., how to play back the audio/video of another user. For the sake of convenience, "another user in the room" is called a "remote user" in this document.
![](https://qcloudimg.tencent-cloud.cn/raw/c8ae41656c97fe546b9c4b0b857b0746.png)

## Call Guide

[](id:step1)
### Step 1. Perform prerequisite steps

Import the SDK and configure the application permissions as instructed in [iOS](https://intl.cloud.tencent.com/document/product/647/35092).

[](id:step2)
### Step 2. Set the subscription mode (optional)
You can call the **setDefaultStreamRecvMode** API in `TRTCCloud` to set the subscription mode. TRTC provides two subscription modes:
- Automatic subscription: The SDK automatically plays back remote users’ audio without additional manual operations required. This is the default subscription mode.
- Manual subscription: The SDK doesn't automatically pull or play back remote users’ audio. You need to call **muteRemoteAudio(userId, false)** to play back the audio.
>! If you do not call `setDefaultStreamRecvMode`, the automatic subscription mode will be used. However, if you want to use the manual subscription mode, note that `setDefaultStreamRecvMode` can take effect only if it is called before `enterRoom`.


[](id:step3)
### Step 3. Enter a TRTC room
Make the current user enter a TRTC room as instructed in [Entering a Room](https://intl.cloud.tencent.com/document/product/647/47645). A user can subscribe to the audio/video streams of a remote user only after a successful room entry.


[](id:step4)
### Step 4. Play back an audio stream
You can call `muteRemoteAudio("denny", true)` to mute the remote user `denny` and then call `muteRemoteAudio("denny", false)` to unmute `denny`.

<dx-codeblock>
::: Android  Java
// Mute the user with ID denny
mCloud.muteRemoteAudio("denny", true);
// Unmute the user with ID denny
mCloud.muteRemoteAudio("denny", false);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// Mute the user with ID denny
[self.trtcCloud muteRemoteAudio:@"denny" mute:YES];
// Unmute the user with ID denny
[self.trtcCloud muteRemoteAudio:@"denny" mute:YES];
:::
::: Windows  C++
// Mute the user with ID denny
trtc_cloud_->muteRemoteAudio("denny", true);
// Unmute the user with ID denny
trtc_cloud_->muteRemoteAudio("denny", false);
:::
</dx-codeblock>


[](id:step5)
### Step 5. Play back a video stream

#### 1. Start and stop playback (startRemoteView + stopRemoteView)
You can call `startRemoteView` to play back the video of a remote user, but only after you pass in a view object to the SDK as the rendering control that carries the user's video image.

The first parameter of `startRemoteView` is `userId` of the remote user, the second is the stream type of the user, and the third is the view object to be passed in. The second parameter `streamType` has three valid values:
- TRTCVideoStreamTypeBig: The primary stream, which is generally used to display the user's camera image.
- TRTCVideoStreamTypeSub: The substream, which is generally used to display the user's screen sharing image.
- TRTCVideoStreamTypeSmall: A lower quality video of the user's primary stream. You can play back the lower quality video of a remote user only after the user enables dual-stream mode (`enableEncSmallVideoStream`). The high quality stream and low quality stream cannot be played back at the same time.

You can call the `stopRemoteView` API to stop playing back the video of one remote user or call the `stopAllRemoteView` API to stop playing back videos of all remote users.

<dx-codeblock>
::: Android  java
// Play back the camera (primary stream) image of `denny`
mCloud.startRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG, cameraView);
// Play back the screen sharing (substream) image of `denny`
mCloud.startRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SUB, screenView);
// Play back the lower quality video image of `denny` (The high quality stream and low quality stream cannot be played back at the same time)
mCloud.startRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_SMALL, cameraView);
// Stop playing back the camera image of `denny`
mCloud.stopRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG, cameraView);
// Stop playing back the video images of all remote users
mCloud.stopAllRemoteView();
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// Play back the camera (primary stream) image of `denny`
[self.trtcCloud startRemoteView:@"denny" streamType:TRTCVideoStreamTypeBig view:cameraView];
// Play back the screen sharing (substream) image of `denny`
[self.trtcCloud startRemoteView:@"denny" streamType:TRTCVideoStreamTypeSub view:screenView];
// Play back the lower quality video image of `denny` (The high quality stream and low quality stream cannot be played back at the same time)
[self.trtcCloud startRemoteView:@"denny" streamType:TRTCVideoStreamTypeSmall view:cameraView];
// Stop playing back the camera image of `denny`
[self.trtcCloud stopRemoteView:@"denny" streamType:TRTCVideoStreamTypeBig view:cameraView];
// Stop playing back the video images of all remote users
[self.trtcCloud stopAllRemoteView];
:::
::: Windows  C++
// Play back the camera (primary stream) image of `denny`
trtc_cloud_->startRemoteView("denny", liteav::TRTCVideoStreamTypeBig, (liteav::TXView)(hWnd));
// Play back the screen sharing (substream) image of `denny`
trtc_cloud_->startRemoteView("denny", liteav::TRTCVideoStreamTypeSub, (liteav::TXView)(hScreenWnd));
// Play back the lower quality video image of `denny` (The high quality stream and low quality stream cannot be played back at the same time)
trtc_cloud_->startRemoteView("denny", liteav::TRTCVideoStreamTypeSmall, (liteav::TXView)(hWnd));
// Stop playing back the camera image of `denny`
trtc_cloud_->stopRemoteView("denny", liteav::TRTCVideoStreamTypeBig);
// Stop playing back the video images of all remote users
trtc_cloud_->stopAllRemoteView();
:::
</dx-codeblock>

#### 2. Set playback parameters (updateRemoteView and setRemoteRenderParams)

You can call the `updateRemoteView` API to change the view object during playback. This is useful for switching the video rendering control.
You can use `setRemoteRenderParams` to set the video image fill mode, rotation angle, and mirror mode.
- Fill mode: You can use the fill mode or fit mode. In both modes, the original image aspect ratio is not changed. The difference is whether black bars are displayed.
- Rotation angle: You can set the rotation angle to 0, 90, 180, or 270 degrees.
- Mirror mode: Indicates whether to flip the image horizontally.

<dx-codeblock>
::: Android  java
// Switch the primary stream image of `denny` to a small floating window (`miniFloatingView`)
mCloud.updateRemoteView("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG, miniFloatingView);

// Set the fill mode of the primary stream image of the remote user `denny` to fill, and disable mirror mode
TRTCCloudDef.TRTCRenderParams param = new TRTCCloudDef.TRTCRenderParams();
param.fillMode   = TRTCCloudDef.TRTC_VIDEO_RENDER_MODE_FILL;
param.mirrorType   = TRTCCloudDef.TRTC_VIDEO_MIRROR_TYPE_DISABLE;
mCloud.setRemoteRenderParams("denny", TRTCCloudDef.TRTC_VIDEO_STREAM_TYPE_BIG, param);
:::
::: iOS&Mac  ObjC
self.trtcCloud = [TRTCCloud sharedInstance];
// Switch the primary stream image of `denny` to a small floating window (`miniFloatingView`)
[self.trtcCloud updateRemoteView:miniFloatingView streamType:TRTCVideoStreamTypeBig forUser:@"denny"];
// Set the fill mode of the primary stream image of the remote user `denny` to fill, and disable mirror mode
TRTCRenderParams *param = [[TRTCRenderParams alloc] init];
param.fillMode     = TRTCVideoFillMode_Fill;
param.mirrorType   = TRTCVideoMirrorTypeDisable;
[self.trtcCloud setRemoteRenderParams:@"denny" streamType:TRTCVideoStreamTypeBig params:param];
:::
::: Windows  C++
// Switch the primary stream image of `denny` to another window (suppose the handle of the new window is `newView`)
trtc_cloud_->updateRemoteView("denny", liteav::TRTCVideoStreamTypeBig, (liteav::TXView)(newView));

// Set the fill mode for the primary stream image of the remote user `denny` to fill, and enable mirror mode
liteav::TRTCRenderParams param;
param.fillMode = TRTCVideoFillMode_Fill;
param.mirrorType = TRTCVideoMirrorType_Enable;
trtc_cloud_->setRemoteRenderParams("denny", TRTCVideoStreamTypeBig, param);
:::
</dx-codeblock>


[](id:step6)
### Step 6. Get the audio/video status of a remote user in the room

In steps 4 and 5, you can control the audio/video playback of remote users. However, if there isn't sufficient information, you won’t be able to know:
- What users are in the current room
- The camera and mic status of users in the room

To solve this problem, you need to listen for the following event callbacks from the SDK:
**Audio status change notification (onUserAudioAvailable)**
Listen for `onUserAudioAvailable(userId,boolean)` to be notified when a remote user turns their mic on/off.

**Video status change notification (onUserVideoAvailable)**
Listen for `onUserVideoAvailable(userId,boolean) to be notified when a remote user turns their camera on/off.
Listen for `onUserSubStreamAvailable(userId,boolean)` to be notified when a remote user enables/disables screen sharing.

**User room entry/exit notification (onRemoteUserEnter/LeaveRoom)**
When a remote user enters the current room, you can use `onRemoteUserEnterRoom(userId)` to get `userId` of the user. When a remote user exits the current room, you can use `onRemoteUserLeaveRoom(userId, reason)` to get `userId` of the user and the reason for the exit.
>! More accurately, `onRemoteUserEnter/LeaveRoom` is triggered only when an anchor enters/leaves the room. This prevents the problem of receiving frequent notifications of room entries/exits when there are a high number of audience members in the room.

With the event callbacks above, you can know the users in the room and whether they have turned on their cameras and mics. In the sample code below, `mCameraUserList`, `mMicrophoneUserList`, and `mUserList` are used to maintain the following information respectively:
- What users (anchors) are in the room
- Which users have turned on their cameras
- Which users have turned on their mics

<dx-codeblock>
::: Android  java
// Get the change of the video status of a remote user and update the list of users who have turned on their cameras (`mCameraUserList`)
@Override
public void onUserVideoAvailable(String userId, boolean available) {
    available?mCameraUserList.add(userId) : mCameraUserList.remove(userId);
}

// Get the change of the audio status of a remote user and update the list of users who have turned on their mics (`mMicrophoneUserList`)
@Override
public void onUserAudioAvailable(String userId, boolean available) {
    available?mMicrophoneUserList.add(userId) : mMicrophoneUserList.remove(userId);
}

// Get the room entry notification of a remote user and update the remote user list (`mUserList`)
@Override
public void onRemoteUserEnterRoom(String userId) {
    mUserList.add(userId);
}

// Get the room exit notification of a remote user and update the remote user list (mUserList)
@Override
public void onRemoteUserLeaveRoom(String userId, int reason) {
    mUserList.remove(userId);
}
:::
::: iOS&Mac  ObjC
// Get the change of the video status of a remote user and update the list of users who have turned on their cameras (`mCameraUserList`)
- (void)onUserVideoAvailable:(NSString *)userId available:(BOOL)available{
    if (available) {
        [mCameraUserList addObject:userId];
    } else {
        [mCameraUserList removeObject:userId];
    }
}

// Get the change of the audio status of a remote user and update the list of users who have turned on their mics (`mMicrophoneUserList`)
- (void)onUserAudioAvailable:(NSString *)userId available:(BOOL)available{
    if (available) {
        [mMicrophoneUserList addObject:userId];
    } else {
        [mMicrophoneUserList removeObject:userId];
    }
}

// Get the room entry notification of a remote user and update the remote user list (`mUserList`)
- (void)onRemoteUserEnterRoom:(NSString *)userId{
    [mUserList addObject:userId];
}

// Get the room exit notification of a remote user and update the remote user list (mUserList)
- (void)onRemoteUserLeaveRoom:(NSString *)userId reason:(NSInteger)reason{
    [mUserList removeObject:userId];
}
:::
::: Windows  C++
// Get the change of the video status of a remote user and update the list of users who have turned on their cameras (`mCameraUserList`)
void onUserVideoAvailable(const char* user_id, bool available) {
    available ? mCameraUserList.push_back(user_id) : mCameraUserList.remove(user_id);
}

// Get the change of the audio status of a remote user and update the list of users who have turned on their mics (`mMicrophoneUserList`)
void onUserAudioAvailable(const char* user_id, bool available) {
    available ? mMicrophoneUserList.push_back(user_id) : mMicrophoneUserList.remove(user_id);
}

// Get the room entry notification of a remote user and update the remote user list (`mUserList`)
void onRemoteUserEnterRoom(const char* user_id) {
    mUserList.push_back(user_id);
}

// Get the room exit notification of a remote user and update the remote user list (mUserList)
void onRemoteUserLeaveRoom(const char* user_id, int reason) {
    mUserList.remove(user_id);
}
:::
</dx-codeblock>


## Advanced Guide

### 1. What are the differences between different muting methods?
There are three muting methods which work in completely different ways:
- **Method 1. The player stops subscribing to the audio stream**
To stop playing back the audio of the remote user `denny`, you can call `muteRemoteAudio("denny", true)`, and the SDK will stop pulling audio data from `denny`. In this mode, less traffic is used. However, because the SDK needs to restart the audio data pull process to resume audio playback, switching from the muted to unmuted status is slow.

- **Method 2. Adjust the playback volume level to zero**
If you need to switch between the muted and unmuted status more quickly, you can use `setRemoteAudioVolume("denny", 0)`, which sets the playback volume level of the remote user `denny` to zero. Because this API doesn't involve network operations, it takes effect very quickly.

- **Method 3. The remote user turns off the mic**
All operations described in this document are performed in the player and take effect only for the local user. For example, if you call `muteRemoteAudio("denny", true)` to mute the remote user `denny`, other users in the room can still hear `denny`.
To completely disable the audio of `denny`, you need to change the way their audio is published. For more information, see [Publishing Audio/Video Streams](https://intl.cloud.tencent.com/document/product/647/47634).
