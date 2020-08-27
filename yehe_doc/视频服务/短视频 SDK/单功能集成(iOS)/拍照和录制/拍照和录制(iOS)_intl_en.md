## Feature Overview
Video shoot includes features such as adjustable-speed shoot, beauty filters, filters, sound effects, and background music configuration. 

## Overview of Used Classes
Tencent Cloud UGC SDK provides the following APIs to implement short video shoot as detailed below:

| API File | Feature |
| ----------------------- | ------------------------------------------ |
| `TXUGCRecord.h`         | Short video shoot                            |
| `TXUGCRecordListener.h` | Callback for short video shoot                             |
| `TXUGCRecordEventDef.h` | Event callback for short video shoot                         |
| `TXUGCRecordTypeDef.h`  | Basic parameter definition                               |
| `TXUGCPartsManager.h`   | Video segment management class, which is used to shoot multiple video segments and delete existing segments |

## Use Instructions
The following is the basic usage process of video shoot:
1. Configure the shoot parameters.
2. Start video image preview.
3. Set the shoot effects.
4. Complete shoot.

Sample code
```
@interface VideoRecordViewController <TXUGCRecordListener> {
   UIView *_videoRecordView;
}

@implementation VideoRecordViewController
- (void)viewDidLoad {
   [super viewDidLoad];

   // Create a view to display the camera preview
   _videoRecordView = [[UIView alloc] initWithFrame:self.view.bounds];
   [self.view addSubview:_videoRecordView];

   // 1. Configure the shoot parameters
   TXUGCSimpleConfig * param = [[TXUGCSimpleConfig alloc] init];
   param.videoQuality = VIDEO_QUALITY_MEDIUM;

   // 2. Start preview. Set the relevant parameters and the view where the preview is to be displayed
   [[TXUGCRecord shareInstance] startCameraSimple:param preview:_videoRecordView];

   // 3. Set the shoot effects. Watermarking is used here as an example
   UIImage *watermarke = [UIImage imageNamed:@"watermarke"];
   [[TXUGCRecord shareInstance] setWaterMark:watermarke normalizationFrame:CGRectMake(0.01, 0.01, 0.1, 0)];
}

// 4. Start shoot
- (IBAction)onStartRecord:(id)sender {
   [TXUGCRecord shareInstance].recordDelegate = self;
   int result = [[TXUGCRecord shareInstance] startRecord];
   if(0 != result) {
        if(-3 == result) [self alert:@"Failed to start shoot" msg:@"Please check whether the camera permission is granted"];
        else if(-4 == result) [self alert:@"Failed to start shoot" msg:@"Please check whether the mic permission is granted"];
        else if(-5 == result) [self alert:@"Failed to start shoot" msg:@"License verification failed"];
   } else {
      // Started successfully
   }
}

// End shoot
- (IBAction)onStopRecord:(id)sender {
   [[TXUGCRecord shareInstance] stopRecord];
}

// Callback for shoot completion
-(void) onRecordComplete:(TXUGCRecordResult*)result
{
   if (result.retCode == UGC_RECORD_RESULT_OK) {
      // The shoot is successful, and the video file is in `result.videoPath`
   } else {
      // Process the error. For the error code definition, please see the definition of `TXUGCRecordResultCode` in `TXUGCRecordTypeDef.h`.
   }
}

-(void)alert:(NSString *)title msg:(NSString *)msg
{
    UIAlertView *alert = [[UIAlertView alloc] initWithTitle:title message:msg delegate:self cancelButtonTitle:@"OK" otherButtonTitles:nil, nil];
    [alert show];
}
@end

```

## Previewing Video Image
`TXUGCRecord` (in `TXUGCRecord.h`) is used for short video shoot. The preview feature needs to be implemented first, where the `startCameraSimplePreview` function is used to start preview. As camera and mic need to be enabled before the preview can be started, prompt windows for permission application may pop up at this point.
### 1. Start preview
```objc
TXUGCRecord *record = [TXUGCRecord sharedInstance];
record.recordDelegate = self; // Set the shoot callback. For the callback method, please see `TXUGCRecordListener`

// Configure the camera and start preview
TXUGCSimpleConfig * param = [[TXUGCSimpleConfig alloc] init];
//param.videoQuality = TXRecordCommon.VIDEO_QUALITY_LOW;		// 360p
//param.videoQuality = TXRecordCommon.VIDEO_QUALITY_MEDIUM;		// 540p
param.videoQuality = TXRecordCommon.VIDEO_QUALITY_HIGH;		  // 720p
param.frontCamera = YES;    // Use the front camera
param.minDuration = 5;	// Set the minimum video shoot duration to 5s
param.maxDuration = 60;	// Set the maximum video shoot duration to 60s
param.enableBFrame = YES; // Enable B frame to improve the image quality at the same bitrate

// Display the camera preview image in `self.previewView`
[recorder startCameraSimple:param preview:self.previewView];

// End video image preview
[[TXUGCRecord shareInstance] stopCameraPreview];

```

### 2. Adjust preview parameters

After starting the camera, you can modify the parameters as follows:
```objc
// Switch the video shoot resolution to 540p
[recorder setVideoResolution: VIDEO_RESOLUTION_540_960];

// Switch the video shoot bitrate to 6,500 Kbps
[recorder setVideoBitrate: 6500];

// Set the focal length to 3. 1 indicates the furthest view (normal lens), and 5 indicates the nearest view (enlarging lens)
[recorder setZoom: 3];

// Switch to the rear camera. YES: switches to front camera; NO: switches to rear camera
[recorder switchCamera: NO];

// Enable the flash. YES: enables; NO: disables
[recorder toggleTorch: YES];

// Set the callback for custom image processing
recorder.videoProcessDelegate = delegate;
```
## Controlling Shoot Process
### Starting, pausing, and resuming shoot
```
// Start shoot
[recorder startRecord];

// Start shoot. You can specify the addresses for the output video file and cover
[recorder startRecord:videoFilePath coverPath:coverPath];

// Start shoot. You can specify the addresses for the output video file, video segment storage, and cover
[recorder startRecord:videoFilePath videoPartsFolder:videoPartFolder coverPath:coverPath];

// Pause shoot
[recorder pauseRecord];

// Resume shoot
[recorder resumeRecord];

// End shoot
[recorder stopRecord];
```

The shoot process and result will be called back through the `TXUGCRecordListener` protocol (defined in `TXUGCRecordListener.h`):

- `onRecordProgress` returns the shoot progress, and the `millisecond` parameter indicates the shoot duration in milliseconds.
```
  @optional
   (void)onRecordProgress:(NSInteger)milliSecond;
```

- `onRecordComplete` returns the shoot result, the `retCode` and `descMsg` fields of `TXRecordResult` indicate the error code and error message, respectively, `videoPath` indicates the path of the shot short video file, and `coverImage` indicates the short video's first-frame image that is automatically captured and will be used in video release.
```
  @optional
   (void)onRecordComplete:(TXUGCRecordResult*)result;
```

- `onRecordEvent` is an API reserved for shoot event callback and is not used currently.
```
  @optional
   (void)onRecordEvent:(NSDictionary*)evt;
```

## Setting Shoot Attributes
### 1. Set the video image
```objc
// Set the landscape or portrait mode for shoot
[recorder setHomeOrientation:VIDOE_HOME_ORIENTATION_RIGHT];

// Set the video preview direction
// rotation: degree for the video preview image to rotate rightwards. Valid values: 0, 90, 180, 270 (other values are invalid)
// Note: it needs to be set before `startRecord` and will not take effect if set during shoot
[recorder setRenderRotation:rotation];

// Set the aspect ratio for shoot
// VIDEO_ASPECT_RATIO_9_16   The aspect ratio is 9:16
// VIDEO_ASPECT_RATIO_3_4   The aspect ratio is 3:4
// VIDEO_ASPECT_RATIO_1_1   The aspect ratio is 1:1
// Note: it needs to be set before `startRecord` and will not take effect if set during shoot
[recorder setAspectRatio:VIDEO_ASPECT_RATIO_9_16];
```
### 2. Set the speed
```
// Set the video shoot speed
//    VIDEO_RECORD_SPEED_SLOWEST,   Ultra-slow
//   VIDEO_RECORD_SPEED_SLOW,   Slow
//    VIDEO_RECORD_SPEED_NOMAL,   Normal
//    VIDEO_RECORD_SPEED_FAST,   Fast
//    VIDEO_RECORD_SPEED_FASTEST,   Ultra-fast
[recorder setRecordSpeed:VIDEO_RECORD_SPEED_NOMAL];
```

### 3. Set the audio
```
// Set the mic volume level. It is used to adjust the mic volume level when background music is played back
// Volume level. 1 indicates the normal volume level. The recommended value range is 0–2. If you want to increase the volume level, you can set a higher value
[recorder setMicVolume:volume];

// Set whether the shoot is muted in the `isMute` parameter. The shoot is unmuted by default
[recorder setMute:isMute];
```

## Capturing

```objc
// Photo capturing, which will take effect if called after `startCameraSimplePreview` or `startCameraCustomPreview`
[recorder snapshot:^(UIImage *image) {
    // `image` is the capturing result
}];
```

## Setting Effects

During video shoot, you can set various special effects for the shot video.
### 1. Watermark
```objc
// Set a global watermark
// normalizationFrame: normalized value of watermark relative to video image. The SDK will automatically calculate the `height` according to the watermark aspect ratio
// Suppose the video image dimensions are (540, 960), and `frame` is set to (0.1, 0.1, 0.1, 0)
// Then, the actual pixel coordinates of the watermark are:
// (540*0.1, 960*0.1, 540*0.1, 540*0.1*waterMarkImage.size.height / waterMarkImage.size.width)
[recorder setWaterMark:waterMarkImage normalizationFrame:frame)
```

### 2. Filter
```
// Set the style filter
// Set the color filter to Romantic, Fresh, Aesthetic, Rosy, Vintage, etc.
// filterImage: color lookup table used for filter. Note: it must be in .png format
// The filter color lookup table used by the demo is in `FilterResource.bundle`
[recorder setFilter:filterImage];

 // It is used to set the filter effect level. Value range: 0–1. The greater the value, the more obvious the effect. Default value: 0.5
[recorder setSpecialRatio:ratio];

// Set the filter mix effect
// mLeftBitmap   Filter on the left
// leftIntensity   Level of the filter on the left
// mRightBitmap   Filter on the right
// rightIntensity   Level of the filter on the right
// leftRadio   Ratio of the dimensions of the image on the left
// You can use this API to implement the effect of switching filters by swipe. For more information, please see the demo
[recorder setFilter:leftFilterImgage leftIntensity:leftIntensity rightFilter:rightFilterImgage rightIntensity:rightIntensity leftRatio:leftRatio];
```

### 3. Beauty filter
```
// Set the levels of the beauty, brightening, and rosy skin filters and the beauty filter style
// `beautyStyle` is defined as follows:
// typedef NS_ENUM(NSInteger, TXVideoBeautyStyle) {
//    VIDOE_BEAUTY_STYLE_SMOOTH     = 0,    // Smooth
//    VIDOE_BEAUTY_STYLE_NATURE     = 1,    // Natural
//    VIDOE_BEAUTY_STYLE_PITU       = 2,    // Pitu beauty filter, which can be used only in Enterprise Edition
// };
// Value range: 0–9; 0 indicates that the filter is disabled, and the greater the value, the more obvious the effect
[recorder setBeautyStyle:beautyStyle beautyLevel:beautyLevel whitenessLevel:whitenessLevel ruddinessLevel:ruddinessLevel];
```

## Advanced Features
[Multi-segment shoot](https://intl.cloud.tencent.com/document/product/1069/38008)
[Shoot drafts](https://intl.cloud.tencent.com/document/product/1069/38009)
[Adding background Music](https://intl.cloud.tencent.com/document/product/1069/38010)
[Voice changing and reverb](https://intl.cloud.tencent.com/document/product/1069/38011)
[Customizing video data](https://intl.cloud.tencent.com/document/product/1069/38038)
