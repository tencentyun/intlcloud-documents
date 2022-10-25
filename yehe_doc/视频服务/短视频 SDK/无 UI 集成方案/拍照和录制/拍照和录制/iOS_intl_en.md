## Overview
You can implement video shooting features including speed change, beautification, filters, audio effects, and background music. 

## Classes
The UGSV SDK offers different video shooting APIs.

| API File                | Description                                       |
| ----------------------- | ------------------------------------------ |
| `TXUGCRecord.h`         | Shooting videos                             |
| `TXUGCRecordListener.h` | Shooting callbacks                             |
| `TXUGCRecordEventDef.h` | Shooting events                         |
| `TXUGCRecordTypeDef.h`  | Definitions of basic parameters                               |
| `TXUGCPartsManager.h`   | Video segment management class, which is used for multi-segment shooting and segment deletion |

## Video Shooting Process
The process of shooting videos is as follows:
1. Configure shooting parameters
2. Enable preview
3. Set shooting effects
4. End shooting

Example
```objectivec
@interface VideoRecordViewController <TXUGCRecordListener> {
   UIView *_videoRecordView;
}

@implementation VideoRecordViewController
- (void)viewDidLoad {
   [super viewDidLoad];

   // Create a view for the camera preview
   _videoRecordView = [[UIView alloc] initWithFrame:self.view.bounds];
   [self.view addSubview:_videoRecordView];

   // 1. Configure shooting parameters
   TXUGCSimpleConfig * param = [[TXUGCSimpleConfig alloc] init];
   param.videoQuality = VIDEO_QUALITY_MEDIUM;

   // 2. Enable preview. Specify preview parameters and the view to display the preview.
   [[TXUGCRecord shareInstance] startCameraSimple:param preview:_videoRecordView];

   // 3. Set shooting effects. In the example below, a watermark is added.
   UIImage *watermarke = [UIImage imageNamed:@"watermarke"];
   [[TXUGCRecord shareInstance] setWaterMark:watermarke normalizationFrame:CGRectMake(0.01, 0.01, 0.1, 0)];
}

// 4. Start shooting
- （IBAction)onStartRecord:(id)sender {
   [TXUGCRecord shareInstance].recordDelegate = self;
   int result = [[TXUGCRecord shareInstance] startRecord];
   if(0 != result) {
        if(-3 == result) [self alert:@"Failed to start shooting." msg:@"Please check whether the camera permission is granted."];
        else if(-4 == result) [self alert:@"Failed to start shooting." msg:@"Please check whether the mic permission is granted."];
        else if(-5 == result) [self alert:@"Failed to start shooting." msg:@"License authentication failed."];
   } else {
      // Started shooting successfully
   }
}

// End shooting
- （IBAction)onStopRecord:(id)sender {
   [[TXUGCRecord shareInstance] stopRecord];
}

// Callback for ending shooting
-(void) onRecordComplete:(TXUGCRecordResult*)result
{
   if (result.retCode == UGC_RECORD_RESULT_OK) {
      // The video was shot successfully and was saved to `result.videoPath`.
   } else {
      // Handle errors. For the definitions of error codes, see `TXUGCRecordResultCode` in `TXUGCRecordTypeDef.h`.
   }
}

-(void)alert:(NSString *)title msg:(NSString *)msg
{
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:msg delegate:self cancelButtonTitle:@"Confirm" otherButtonTitles:nil, nil];
    [alert show];
}
@end
```

## Preview
`TXUGCRecord` in `TXUGCRecord.h` is used to implement video shooting. The first step of shooting videos is using `startCameraSimplePreview` to enable preview. Because mic and camera permissions are required for preview, you need to configure pop-up windows to request the permissions.
### 1. Enable preview
```objectivec
TXUGCRecord *record = [TXUGCRecord sharedInstance];
record.recordDelegate = self; //Configure shooting callbacks. For details, see `TXUGCRecordListener`.

// Configure camera parameters and start preview
TXUGCSimpleConfig * param = [[TXUGCSimpleConfig alloc] init];
//param.videoQuality = TXRecordCommon.VIDEO_QUALITY_LOW;// 360p
//param.videoQuality = TXRecordCommon.VIDEO_QUALITY_MEDIUM;// 540p
param.videoQuality = TXRecordCommon.VIDEO_QUALITY_HIGH;  // 720p
param.frontCamera = YES;    // Use the front camera
param.minDuration = 5;// Set the minimum shooting duration to 5 seconds
param.maxDuration = 60;// Set the maximum shooting duration to 60 seconds
param.enableBFrame = YES; // Enable B frame encoding, which produces better video quality at the same bitrate

// Display the preview in `self.previewView`
[recorder startCameraSimple:param preview:self.previewView];

// Disable preview
[[TXUGCRecord shareInstance] stopCameraPreview];
```

### 2. Modify preview parameters

To modify preview parameters after the camera is turned on, refer to the code below:

```objectivec
// Change the shooting resolution to 540p
[recorder setVideoResolution: VIDEO_RESOLUTION_540_960];

// Change the video bitrate for shooting to 6500 Kbps
[recorder setVideoBitrate: 6500];

// Set the focal length to 3. 1 indicates the widest angle of view (original), and 5 indicates the narrowest angle of view (zoomed in).
[recorder setZoom: 3];

// Switch the camera. `Yes`: Front Camera; `No`: Rear camera.
[recorder switchCamera: NO];

// Turn on/off the flashlight. `Yes`: Turn on the flashlight; `No`: Turn off the flashlight.
[recorder toggleTorch: YES];

// Set the callback for custom processing
recorder.videoProcessDelegate = delegate;
```

## Shooting control
### Start, pause, and resume shooting
```objectivec
// Start shooting a video
[recorder startRecord];

// Start shooting. You can specify the path to save the video and the path of the thumbnail image.
[recorder startRecord:videoFilePath coverPath:coverPath];

// Start shooting. You can specify the paths to save the video and video segments, as well as the path of the thumbnail image.
[recorder startRecord:videoFilePath videoPartsFolder:videoPartFolder coverPath:coverPath];

// Pause shooting
[recorder pauseRecord];

// Resume shooting
[recorder resumeRecord];

// Ending shooting
[recorder stopRecord];
```

The shooting progress and result callbacks are implemented by `TXUGCRecordListener` (defined in `TXUGCRecordListener.h`).
- `onRecordProgress` is the shooting progress callback. The `millisecond` parameter indicates the recorded duration in milliseconds.
```objectivec
  @optional
   (void)onRecordProgress:(NSInteger)milliSecond;
```
- `onRecordComplete` is the shooting result callback. The `retCode` and `descMsg` fields in `TXRecordResult` indicate the error code and error message respectively. `videoPath` indicates the path of the video, and `coverImage` is the first frame of the video, which is used as the thumbnail.
```
  @optional
   (void)onRecordComplete:(TXUGCRecordResult*)result;
```
- `onRecordEvent` is the callback reserved for the shooting event and is not used currently.
```
  @optional
   (void)onRecordEvent:(NSDictionary*)evt;
```

## Shooting settings
### 1. Video
```objectivec
// Shoot in landscape mode
[recorder setHomeOrientation:VIDOE_HOME_ORIENTATION_RIGHT];

// Set orientation for preview
// The valid values for `rotation` are 0, 90, 180, and 270, which indicate the clockwise rotation angle.
// You must set the rotation before you call `startRecord` for the setting to take effect.
[recorder setRenderRotation:rotation];

// Set the aspect ratio
// VIDEO_ASPECT_RATIO_9_16: 9:16
// VIDEO_ASPECT_RATIO_3_4: 3:4
// VIDEO_ASPECT_RATIO_1_1: 1:1
// You must set the rotation before you call `startRecord` for the setting to take effect.
[recorder setAspectRatio:VIDEO_ASPECT_RATIO_9_16];
```
### 2. Speed
```objectivec
// Set the shooting speed
//    VIDEO_RECORD_SPEED_SLOWEST: Very slow
//   VIDEO_RECORD_SPEED_SLOW: Slow
//    VIDEO_RECORD_SPEED_NOMAL: Original
//    VIDEO_RECORD_SPEED_FAST: Fast
//    VIDEO_RECORD_SPEED_FASTEST: Very fast
[recorder setRecordSpeed:VIDEO_RECORD_SPEED_NOMAL];
```

### 3. Audio
```objectivec
// Set the mic volume. This is used to control the volume of the mic when background music is mixed.
// Volume. The normal volume is 1. We recommend 0-2, but you can set it to a larger value if you want louder music.
[recorder setMicVolume:volume];

// Mute/Unmute. The `isMute` parameter specifies whether to mute audio. Audio is unmuted by default.
[recorder setMute:isMute];
```

## Picture taking

```objectivec
// Take a photo/Capture a frame from a video. This API works only if it is called after `startCameraSimplePreview` or `startCameraCustomPreview`.
[recorder snapshot:^(UIImage *image) {
    // `image` is the capturing result.
}];
```

## Effects

You can add various effects to your video during shooting.
### 1. Watermarks
```objectivec
// Add a global watermark
// normalizationFrame: The normalized position of the watermark in relation to the video. The SDK calculates the watermark height based on the aspect ratio.
// Suppose the video dimensions are 540 x 960, and `frame` is set to `(0.1，0.1，0.1, 0)`.
// The actual coordinates of the watermark would be:
// (540*0.1, 960*0.1, 540*0.1, 540*0.1*waterMarkImage.size.height / waterMarkImage.size.width)
[recorder setWaterMark:waterMarkImage normalizationFrame:frame)
```

### 2. Filters

```objectivec
// Set the filter style
// Set the color filter: Romantic, refreshing, elegant, pink, retro, and more
// filterImage: The color lookup table, which must be in PNG format.
// The color lookup table used in the demo is in `FilterResource.bundle`.
[recorder setFilter:filterImage];

 // Set the strength of filters. Value range: 0-1. Default: 0.5. The greater the value, the stronger the filter.
[recorder setSpecialRatio:ratio];

// Set a filter combination
// mLeftBitmap: The left filter
// leftIntensity: The strength of the left filter
// mRightBitmap: The right filter
// rightIntensity: The strength of the right filter
// leftRatio: The ratio of the width of the left picture to the video width
// You can use this API to implement "swipe to change filter".
[recorder setFilter:leftFilterImgage leftIntensity:leftIntensity rightFilter:rightFilterImgage rightIntensity:rightIntensity leftRatio:leftRatio];
```

### 3. Beauty filters
```objectivec
// Set the beauty filter style and strength and the strength of the skin brightening and blush effects
// beautyStyle:
// typedef NS_ENUM(NSInteger, TXVideoBeautyStyle) {
//    VIDOE_BEAUTY_STYLE_SMOOTH     = 0,    // Smooth
//    VIDOE_BEAUTY_STYLE_NATURE     = 1,    // Natural
// };
// The value range for the strength parameter is 0-9. `0` means to disable the filter. The greater the value, the stronger the filter.
[recorder setBeautyStyle:beautyStyle beautyLevel:beautyLevel whitenessLevel:whitenessLevel ruddinessLevel:ruddinessLevel];
```

## Advanced Features
[Multi-segment shooting](https://intl.cloud.tencent.com/document/product/1069/38008)
[Drafts](https://intl.cloud.tencent.com/document/product/1069/38009)
[Adding background music](https://intl.cloud.tencent.com/document/product/1069/38010)
[Voice changing and reverb](https://intl.cloud.tencent.com/document/product/1069/38011)
[Customizing video data](https://intl.cloud.tencent.com/document/product/1069/38038)
