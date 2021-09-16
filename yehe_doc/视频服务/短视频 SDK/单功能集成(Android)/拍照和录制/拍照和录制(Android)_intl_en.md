Video shoot includes features such as adjustable-speed shoot, beauty filters, filters, sound effects, and background music configuration. 

## Overview of Relevant Classes
| Class | Feature |
| ---------------------- | ---------------------------------------------- |
| TXUGCRecord            | Video shoot implementation |
| TXUGCPartsManager      | Video segment management class, which is used to shoot multiple video segments and delete existing segments     |
| ITXVideoRecordListener | Shoot callback                                       |
| TXRecordCommon         | Basic parameter definition, including video shoot callback and release callback APIs |

## Use Instructions
The following is the basic usage process of video shoot:
1. Configure the shoot parameters.
2. Start video image preview.
3. Set the shoot effects.
4. Complete shoot.

#### Code Example
```
// Create `TXCloudVideoView` for camera preview
mVideoView = (TXCloudVideoView) findViewById(R.id.video_view);
// 1. Configure the shoot parameters. The recommended configuration of `TXUGCSimpleConfig` is used here as an example
TXRecordCommon.TXUGCSimpleConfig param = new TXRecordCommon.TXUGCSimpleConfig();
param.videoQuality = TXRecordCommon.VIDEO_QUALITY_MEDIUM;
// 2. Start video image preview
mTXCameraRecord.startCameraSimplePreview(param, mVideoView);
// 3. Set the shoot effects. Watermarking is used here as an example
TXVideoEditConstants.TXRect rect = new TXVideoEditConstants.TXRect();
rect.x = 0.5f;
rect.y = 0.5f;
rect.width = 0.5f;
mTXCameraRecord.setWatermark(BitmapFactory.decodeResource(getResources(), R.drawable.watermark), rect);
// 4. Start shoot
int result = mTXCameraRecord.startRecord();
if (result != TXRecordCommon.START_RECORD_OK) {
            if (result == -4) {The video image has not been displayed yet} 
            else if (result == -3) {// The version is too low}
	    else if (result == -5) {// License verification failed] }
            }
else{// Started successfully}
// End shoot
mTXCameraRecord.stopRecord();
// Callback for shoot completion
public void onRecordComplete(TXRecordCommon.TXRecordResult result) {
	if (result.retCode >= 0 ) {
		// The shoot is successful, and the video file is in `result.videoPath`
	}else{
		// Process the error. For the error code definition, please see "Definition of error codes for shoot result callback" in `TXRecordCommon`.
	}
}
```

## Previewing Video Image
`TXUGCRecord` (in `TXUGCRecord.java`) is used for short video shoot. The preview feature needs to be implemented first, where the `startCameraSimplePreview` function is used to start preview. As camera and mic need to be enabled before the preview can be started, prompt windows for permission application may pop up at this point.

### 1. Start preview
```
TXUGCRecord mTXCameraRecord = TXUGCRecord.getInstance(this.getApplicationContext());
mTXCameraRecord.setVideoRecordListener(this);					// Set shoot callback
mVideoView = (TXCloudVideoView) findViewById(R.id.video_view);	// Prepare a view for camera image preview
TXRecordCommon.TXUGCSimpleConfig param = new TXRecordCommon.TXUGCSimpleConfig();
//param.videoQuality = TXRecordCommon.VIDEO_QUALITY_LOW;		// 360p
//param.videoQuality = TXRecordCommon.VIDEO_QUALITY_MEDIUM;		// 540p
param.videoQuality = TXRecordCommon.VIDEO_QUALITY_HIGH;		// 720p
param.isFront = true;           // Whether to use the front camera
param.minDuration = 5000;	// Minimum video shoot duration in milliseconds
param.maxDuration = 60000;	// Maximum video shoot duration in milliseconds
param.touchFocus = false; // false: autofocus; true: manual focus
mTXCameraRecord.startCameraSimplePreview(param,mVideoView);

// End video image preview
mTXCameraRecord.stopCameraPreview();
```
### 2. Adjust preview parameters
After starting the camera, you can adjust the preview parameters as follows:
``` 
// Switch the video shoot resolution to 540p
mTXCameraRecord.setVideoResolution(TXRecordCommon.VIDEO_RESOLUTION_540_960);

// Switch the video shoot bitrate to 6,500 Kbps
mTXCameraRecord.setVideoBitrate(6500);

// Get the maximum focal length supported by the camera
mTXCameraRecord.getMaxZoom();

// Set the focal length to 3. 1 indicates the furthest view (normal lens), and 5 indicates the nearest view (enlarging lens)
mTXCameraRecord.setZoom(3);

// Switch to the rear camera. true: switches to front camera; false: switches to rear camera
mTXCameraRecord.switchCamera(false);

// Enable the flash. true: enables; false: disables
mTXCameraRecord.toggleTorch(false);

// If `param.touchFocus` is `true`, manual focus will be used. You can use the following API to set the focus position
mTXCameraRecord.setFocusPosition(eventX, eventY);

// Set the callback for custom image processing
mTXCameraRecord.setVideoProcessListener(this);
```

## Capturing
After enabling the camera preview, you can use the photo capturing feature.

``` 
// Photo capturing, which will take effect if called after `startCameraSimplePreview` or `startCameraCustomPreview`
mTXCameraRecord.snapshot(new TXRecordCommon.ITXSnapshotListener() {
                @Override
                public void onSnapshot(Bitmap bmp) {
                    // Save or display the photo
                }
            });
```

## Controlling Shoot Process
The shoot can be started, paused, and resumed as follows:
``` 
// Start shoot
mTXCameraRecord.startRecord();

// Start shoot. You can specify the addresses for the output video file and cover
mTXCameraRecord.startRecord(videoFilePath, coverPath);

// Start shoot. You can specify the addresses for the output video file, video segment storage, and cover
mTXCameraRecord.startRecord(videoFilePath, videoPartFolder, coverPath);

// Pause shoot
mTXCameraRecord.pauseRecord();

// Resume shoot
mTXCameraRecord.resumeRecord();

// End shoot
mTXCameraRecord.stopRecord();
```
The shoot process and result will be returned through the `TXRecordCommon.ITXVideoRecordListener` API (defined in `TXRecordCommon.java`):

- `onRecordProgress` returns the shoot progress, and the `millisecond` parameter indicates the shoot duration in milliseconds.
``` 
@optional
void onRecordProgress(long milliSecond);
```

- `onRecordComplete` returns the shoot result, the `retCode` and `descMsg` fields of `TXRecordResult` indicate the error code and error message, respectively, `videoPath` indicates the path of the shot short video file, and `coverImage` indicates the short video's first-frame image that is automatically captured and will be used in video release.
```    
@optional
void onRecordComplete(TXRecordResult result);
```

- `onRecordEvent` is the shoot event callback, which contains the event ID and event-related parameters in the format of (key,value).
```    
@optional
void onRecordEvent(final int event, final Bundle param);
```

## Setting Shoot Attributes
### Set the video image

``` 
// Set the landscape or portrait mode for shoot
mTXCameraRecord.setHomeOrientation(TXLiveConstants.VIDEO_ANGLE_HOME_RIGHT);

// Set the video preview direction
// TXLiveConstants.RENDER_ROTATION_0 (normal portrait) 
// TXLiveConstants.RENDER_ROTATION_90 (rotated 90 degrees leftwards) 
// TXLiveConstants.RENDER_ROTATION_180 (rotated 180 degrees leftwards) 
// TXLiveConstants.RENDER_ROTATION_270 (rotated 270 degrees leftwards) 
// Note: it needs to be set before `startRecord` and will not take effect if set during shoot
mTXCameraRecord.setRenderRotation(TXLiveConstants.RENDER_ROTATION_PORTRAIT);

// Set the aspect ratio for shoot
// TXRecordCommon.VIDEO_ASPECT_RATIO_9_16   The aspect ratio is 9:16
// TXRecordCommon.VIDEO_ASPECT_RATIO_3_4   The aspect ratio is 3:4
// TXRecordCommon.VIDEO_ASPECT_RATIO_1_1   The aspect ratio is 1:1
// Note: it needs to be set before `startRecord` and will not take effect if set during shoot
mTXCameraRecord.setAspectRatio(TXRecordCommon.VIDEO_ASPECT_RATIO_9_16);
```

### Set the speed
``` 
// Set the video shoot speed
// TXRecordCommon.RECORD_SPEED_SLOWEST (ultra-slow) 
// TXRecordCommon.RECORD_SPEED_SLOW (slow) 
// TXRecordCommon.RECORD_SPEED_NORMAL (standard) 
// TXRecordCommon.RECORD_SPEED_FAST (fast) 
// TXRecordCommon.RECORD_SPEED_FASTEST (ultra-fast) 
mTXCameraRecord.setRecordSpeed(TXRecordCommon.VIDEO_RECORD_SPEED_NORMAL);
```
### Set the audio

``` 
// Set the mic volume level. It is used to adjust the mic volume level when background music is played back
// Volume level. 1 indicates the normal volume level. The recommended value range is 0–2. If you want to increase the volume level, you can set a higher value
mTXCameraRecord.setMicVolume(volume);
// Set whether the shoot is muted in the `isMute` parameter. The shoot is unmuted by default
mTXCameraRecord.setMute(isMute);
```

## Setting Effects
During video shoot, you can set various special effects for the shot video.
### Watermark
``` 
// Set a global watermark
// TXRect: normalized value of watermark relative to video image. The SDK will automatically calculate the `height` according to the watermark aspect ratio
// Suppose the video image dimensions are (540, 960), and three parameters in `TXRect` are all set to 0.1
// Then, the actual pixel coordinates of the watermark are (540 * 0.1, 960 * 0.1, 540 * 0.1)
// 540 * 0.1 * watermarkBitmap.height / watermarkBitmap.width）
mTXCameraRecord.setWatermark(watermarkBitmap, txRect)
```
### Filter
``` 
// Set the color filter to Romantic, Fresh, Aesthetic, Rosy, Vintage, etc.
// filterBitmap: color lookup table used for filter. Note: it must be in .png format
// The filter color lookup table used by the demo is in the `RTMPAndroidDemo/app/src/main/res/drawable-xxhdpi/` directory
mTXCameraRecord.setFilter(filterBitmap);

// Set the filter mix effect
// mLeftBitmap   Filter on the left
// leftIntensity   Level of the filter on the left
// mRightBitmap   Filter on the right
// rightIntensity   Level of the filter on the right
// leftRadio   Ratio of the dimensions of the image on the left
// You can use this API to implement the effect of switching filters by swipe. For more information, please see the demo
mTXCameraRecord.setFilter(mLeftBitmap, leftIntensity, mRightBitmap, rightIntensity, leftRatio);

// It is used to set the filter effect level. Value range: 0–1. The greater the value, the more obvious the effect. Default value: 0.5
mTXCameraRecord.setSpecialRatio(0.5);
```

### Beauty filter

``` 
// Set the beauty filter type
mTXCameraRecord.setBeautyStyle(style);

// Set the eye enlarging effect level. Recommended value range: 0–9. If you want a more obvious effect, you can set a greater value
mTXCameraRecord.setEyeScaleLevel(eyeScaleLevel);

// Set the face slimming effect level. Recommended value range: 0–9. If you want a more obvious effect, you can set a greater value
mTXCameraRecord.setFaceScaleLevel(faceScaleLevel);

// Set the chin slimming effect level. Recommended value range: 0–9. If you want a more obvious effect, you can set a greater value
mTXCameraRecord.setFaceVLevel(level);

// Set the chin lengthening/shortening effect level. Recommended value range: 0–9. If you want a more obvious effect, you can set a greater value
mTXCameraRecord.setChinLevel(scale);

// Set the face shortening effect level. Recommended value range: 0–9. If you want a more obvious effect, you can set a greater value
mTXCameraRecord.setFaceShortLevel(level);

// Set the nose narrowing effect level. Recommended value range: 0–9. If you want a more obvious effect, you can set a greater value
mTXCameraRecord.setNoseSlimLevel(scale);

// Set the green screen keying file. It can be in formats supported by Android, such as .jpg and .png for images and .mp4 and .3gp for videos, and can be looped
mTXCameraRecord.setGreenScreenFile(path, isLoop);

// Set `motionTmplPath`, which is the path of the animated effect file of the animated sticker. An empty string ("") indicates to cancel the animated effect
mTXCameraRecord.setMotionTmp(motionTmplPath);

// Set whether to mute the animated sticker. true: mutes; false: unmutes
mTXCameraRecord.setMotionMute(true);
```

## Getting License Information
UGSV license verification is added in the new version of the SDK. If the verification fails, you can use the following API to query the specific information in the license:

``` 
TXUGCBase.getInstance().getLicenceInfo(Context context);
```

## Advanced Features

[Multi-segment shoot](https://intl.cloud.tencent.com/document/product/1069/38020)
[Shoot drafts](https://intl.cloud.tencent.com/document/product/1069/38021)
[Adding background music](https://intl.cloud.tencent.com/document/product/1069/38022)
[Voice changing and reverb](https://intl.cloud.tencent.com/document/product/1069/38023)
[Customizing video data](https://intl.cloud.tencent.com/document/product/1069/38039)

