This document describes how to implement basic duet features.

## Process Overview
 
1. Place two views on the page, one for playback, and the other for shoot.
2. Place a button and progress bar for shoot and progress display, respectively.
3. Stop shoot after the video in the same duration as that of the source video has been shot.
4. Compose the shot video with the source video side by side.
5. Preview the composed video.

## UI Construction

In `activity_video_record.xml` of the shoot page `TCVideoRecordActivity`, create two views: the left one is the shoot page, and the right one is the playback page.
![](https://main.qcloudimg.com/raw/692dc0e49f7d41f746c528c703cbc6b9.png)

## Sample Code

The duet feature mainly uses three other features: playback, shoot, and composition of the shot and source videos, which correspond to the `TXVideoEditer`, `TXUGCRecord`, and `TXVideoJoiner` SDK classes, respectively. You can also use `TXVodPlayer` for playback.

1. In the video list on the UGSV application homepage, select a video to enter the playback page `TCVodPlayerActivity`. Then, click "Duet" in the bottom-right corner.
The video will be first downloaded onto the local SD card, the video information such as audio sample rate and frame rate (in fps) will be obtained, and then the shoot page will be displayed.

2. Enter the shoot page `TCVideoRecordActivity` for duet. Please pay attention to the following:
 - The maximum length of the shoot progress bar should be the length of the source video progress bar.
 - The frame rates of the shot video and source video must be the same; otherwise, the audio and video may be out of sync.
 - The audio sample rates of the shot video and source video must be the same; otherwise, the audio and video may be out of sync.
 - The rendering mode set for shoot is fit mode, where the video image can be proportionally scaled at the aspect ratio of 9:16.
 - You need to set audio mute for shoot on Android; otherwise, the source and shot videos' audios will be mixed.
 
 ```
// Shoot page
mVideoView = mVideoViewFollowShotRecord;
// Played back video
mFollowShotVideoPath = intent.getStringExtra(TCConstants.VIDEO_EDITER_PATH);
mFollowShotVideoDuration = (int)(intent.getFloatExtra(TCConstants.VIDEO_RECORD_DURATION, 0) * 1000);
initPlayer();
// The maximum length of the shoot progress bar should be the length of the source video. The frame rate (`fps`) of the source video should also be used for the shot video
mMaxDuration = (int)mFollowShotVideoDuration;
mFollowShotVideoFps = intent.getIntExtra(TCConstants.RECORD_CONFIG_FPS, 20);
mFollowShotAudioSampleRateType = intent.getIntExtra(TCConstants.VIDEO_RECORD_AUDIO_SAMPLE_RATE_TYPE, TXRecordCommon.AUDIO_SAMPLERATE_48000);
// Initialize the duet API
mTXVideoJoiner = new TXVideoJoiner(this);
mTXVideoJoiner.setVideoJoinerListener(this);
```
```objc
// Initialize the player. Here, `TXVideoEditer` is used. You can also use `TXVodPlayer`
mTXVideoEditer = new TXVideoEditer(this);
mTXVideoEditer.setVideoPath(mFollowShotVideoPath);
TXVideoEditConstants.TXPreviewParam param = new TXVideoEditConstants.TXPreviewParam();
param.videoView = mVideoViewPlay;
param.renderMode = TXVideoEditConstants.PREVIEW_RENDER_MODE_FILL_EDGE;
mTXVideoEditer.initWithPreview(param);
```
```
customConfig.videoFps = mFollowShotVideoFps;
customConfig.audioSampleRate = mFollowShotAudioSampleRateType; // The audio sample rate of the shot video must be the same as that of the source video
customConfig.needEdit = false;
mTXCameraRecord.setVideoRenderMode(TXRecordCommon.VIDEO_RENDER_MODE_ADJUST_RESOLUTION); // Set the rendering mode to fit mode
mTXCameraRecord.setMute(true); // The duet audio played back by the speaker will not be recorded, because if it is recorded by mic, the source and shot videos' audios will be mixed
```

3. Start shoot. When the maximum shoot duration is reached, the `onRecordComplete` callback will be returned to proceed with the composition. Here, you need to specify the positions of the two videos in the result.
```
private void prepareToJoiner(){
    List<String> videoSourceList = new ArrayList<>();
    videoSourceList.add(mRecordVideoPath);
    videoSourceList.add(mFollowShotVideoPath);
    mTXVideoJoiner.setVideoPathList(videoSourceList);
    mFollowShotVideoOutputPath = getCustomVideoOutputPath("Follow_Shot_");
    // Proportionally scale the video on the right by the width and height of the shot video on the left
    int followVideoWidth;
    int followVideoHeight;
    if ((float) followVideoInfo.width / followVideoInfo.height >= (float)recordVideoInfo.width / recordVideoInfo.height) {
        followVideoWidth = recordVideoInfo.width;
        followVideoHeight = (int) ((float)recordVideoInfo.width * followVideoInfo.height / followVideoInfo.width);
    } else {
        followVideoWidth = (int) ((float)recordVideoInfo.height * followVideoInfo.width / followVideoInfo.height);
        followVideoHeight = recordVideoInfo.height;
    }

    TXVideoEditConstants.TXAbsoluteRect rect1 = new TXVideoEditConstants.TXAbsoluteRect();
    rect1.x = 0;                     // Top-left point position of the first video
    rect1.y = 0;
    rect1.width = recordVideoInfo.width;   // Width and height of the first video
    rect1.height = recordVideoInfo.height;

    TXVideoEditConstants.TXAbsoluteRect rect2 = new TXVideoEditConstants.TXAbsoluteRect();
    rect2.x = rect1.x + rect1.width; // Top-left point position of the second video
    rect2.y = (recordVideoInfo.height - followVideoHeight) / 2;
    rect2.width = followVideoWidth;  // Width and height of the second video
    rect2.height = followVideoHeight;

    List<TXVideoEditConstants.TXAbsoluteRect> list = new ArrayList<>();
    list.add(rect1);
    list.add(rect2);
    mTXVideoJoiner.setSplitScreenList(list, recordVideoInfo.width + followVideoWidth, recordVideoInfo.height); // The second and third parameters: width and height of the video composition canvas
    mTXVideoJoiner.splitJoinVideo(TXVideoEditConstants.VIDEO_COMPRESSED_540P, mFollowShotVideoOutputPath);
}
```

4. Listen on the composition callback. After `onJoinComplete`, redirect to the preview page for playback.
```
@Override
public void onJoinComplete(TXVideoEditConstants.TXJoinerResult result) {
    mCompleteProgressDialog.dismiss();
    if(result.retCode == TXVideoEditConstants.JOIN_RESULT_OK){
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                isReadyJoin = true;
                startEditerPreview(mFollowShotVideoOutputPath);
                if(mTXVideoEditer != null){
                    mTXVideoEditer.release();
                    mTXVideoEditer = null;
                }
            }
        });
    }else{
        runOnUiThread(new Runnable() {
            @Override
            public void run() {
                Toast.makeText(TCVideoRecordActivity.this, "Composition failed", Toast.LENGTH_SHORT).show();
            }
        });
    }
}
```
At this point, all basic duet features have been implemented. For the complete code, please see [Source Code of Full-Featured UGSV Application Demo](https://intl.cloud.tencent.com/document/product/1069/37914#.E5.85.A8.E5.8A.9F.E8.83.BD.E5.B0.8F.E8.A7.86.E9.A2.91-app.EF.BC.88demo.EF.BC.89.E6.BA.90.E4.BB.A3.E7.A0.81).
