## Feature Overview
Video editing includes features such as video clipping, time-based special effects (slow motion, reverse, and loop), special effect filters (dynamic light-wave, darkness and phantom, soul out, and cracked screen), filter styles (aesthetic, rosy, blues, etc.), music mix, animated stickers, static stickers, and bubble subtitles.

## Overview of Relevant Classes 

| Class Name | Feature  |
| ------------- | --------- |
| `TXVideoInfoReader.h`| Gets media information |
| `TXVideoEditer.h` | Edits video |

## Use Instructions
The following is the basic usage process of video editing:

1. Set the video path.
2. Add effects.
3. Generate a video and output it to a specified file.
4. Listen on the generation event.

#### Sample
```
// Here, `Common/UGC/VideoPreview` in the demo is used as the preview view
#import "VideoPreview.h"

@implementation EditViewController
{
   TXVideoEditer *editor;
   VideoPreview *_videoPreview;
}

- (void)viewDidLoad {
   [super viewDidLoad];
   _videoPreview = [[VideoPreview alloc] initWithFrame:self.view.bounds];
   [self.view addSubview:_videoPreview];
   // Edit preview parameters
   TXPreviewParam *param = [[TXPreviewParam alloc] init];
   param.videoView = _videoPreview.renderView;
   param.renderMode = PREVIEW_RENDER_MODE_FILL_EDGE;

   // 1. Initialize the editor. If you do not need preview, you can pass in `nil` or directly call the `init` method
   TXVideoEditer *editor = [[TXVideoEditer alloc] initWithPreview:param];

   // Set the source video path
   NString *path = [[NSBundle mainBundle] pathForResource:@"demo" ofType:@"mp4"]
   [editor setVideoPath: path];

   // Configure the delegation
   editor.generateDelegate = self;      // Set the callback delegation object of the generation event, which can be used to get the generation progress and result

   // 2. Process the video. Watermarking is used as an example here
   [editor setWaterMark:[UIImage imageNamed:@"water_mark"]
         normalizationFrame:CGRectMake(0,0,0.1,0)];
}

// 3. Generate the video. Response to a user click is used as an example here
- (IBAction)onGenerate:(id)sender {
   NSString *output = [NSTemporaryDirectory() stringByAppendingPathComponent:@"temp.mp4"];
   [editor generateVideo:VIDEO_COMPRESSED_720P videoOutputPath:output];                                                              
}

// 4. Get the generation progress
-(void) onGenerateProgress:(float)progress
{
}

// Get the generation result
-(void) onGenerateComplete:(TXGenerateResult *)result
{
   if (result.retCode == 0) {
      // Generated successfully
   } else {
      // Generation failed. For the specific cause, please see `result.descMsg`.
   }
}
@end
```

## Getting Video Information
The `getVideoInfo` method of `TXVideoInfoReader` can get certain basic information of a specified video file. The relevant APIs are as detailed below:
```objective-c
// Get the video file information
+ (TXVideoInfo *)getVideoInfo:(NSString *)videoPath;

/** Get the video file information
 * @param videoAsset   Video file attributes
 * @return   Video information
 */
+ (TXVideoInfo *)getVideoInfoWithAsset:(AVAsset *)videoAsset;
```
The returned `TXVideoInfo` is defined as follows:
```
/// Video information
@interface TXVideoInfo : NSObject
/// Image of the first video frame
@property (nonatomic, strong) UIImage*              coverImage;
/// Video duration in seconds
@property (nonatomic, assign) CGFloat               duration;
/// Video size in bytes
@property (nonatomic, assign) unsigned long long    fileSize;
/// Video frame rate in fps
@property (nonatomic, assign) float                 fps;      
/// Video bitrate in Kbps
@property (nonatomic, assign) int                   bitrate;
/// Audio sample rate
@property (nonatomic, assign) int                   audioSampleRate;
/// Video width
@property (nonatomic, assign) int                   width;
/// Video height
@property (nonatomic, assign) int                   height;
/// Video image rotation angle
@property (nonatomic, assign) int                   angle;
@end
```

## Getting Thumbnail
The thumbnail APIs are mainly used to generate the preview thumbnails displayed on the video editing page, get the video cover, and perform other relevant operations.
### 1. Get the thumbnails evenly distributed along the video duration by number

`getSampleImages` of `TXVideoInfoReader` can get the specified number of thumbnails at the same time intervals:
```
/** Get the list of thumbnails of the video
 * @param count   Number of the thumbnails to be obtained (at even sampling intervals)
 * @param maxSize   Maximum thumbnail dimensions. The dimensions of the generated thumbnails will not exceed the specified width and height.
 * @param videoAsset   Video file attributes
 * @param sampleProcess   Sampling progress
 */
+ (void)getSampleImages:(int)count
                maxSize:(CGSize)maxSize
             videoAsset:(AVAsset *)videoAsset
               progress:(sampleProcess)sampleProcess;
```
`VideoRangeSlider` in the SDK uses `getSampleImages` to get 10 thumbnails so as to construct a progress bar consisting of video preview images.

### 2. Get thumbnails according to the list of points in time
```
 /**
 * Get the thumbnails according to the list of points in time
 * @param asset   Video file object
 * @param times   List of points in time for getting thumbnails
 * @param maxSize   Thumbnail dimensions
 */
+ (UIImage *)getSampleImagesFromAsset:(AVAsset *)asset
                                times:(NSArray<NSNumber*> *)times
                              maxSize:(CGSize)maxSize
                             progress:(sampleProcess)sampleProcess;
```

## Editing and Previewing
Video editing supports two effect preview modes: **pinpoint preview** (the video image is frozen at a specified point in time) and **range preview** (a video segment within a specified time range (A–B) is looped). To use a preview mode, you need to bind a `UIView` to the SDK in order to display the video image.

### 1. Bind UIView
The `initWithPreview` function of `TXVideoEditer` is used to bind a `UIView` to the SDK for video image rendering. You can set whether to use the **fit** or **fill** mode by controlling `renderMode` of `TXPreviewParam`.

```   
   PREVIEW_RENDER_MODE_FILL_SCREEN - Fill mode, where the video image will cover the entire screen with no black bars present, but the video image may be cropped.     
   PREVIEW_RENDER_MODE_FILL_EDGE - Fit mode, where the video image will be complete but black bars will exist if the aspect ratio of the video is different from that of the screen.   
```

### 2. Use pinpoint preview
The `previewAtTime` function of `TXVideoEditer` is used to preview the video image at a specified point in time.
```
/** Render the video image at a specified point in time
 *  @param time   Preview frame time in seconds
 */
- (void)previewAtTime:(CGFloat)time;
```

### 3. Use range preview
The `startPlayFromTime` function of `TXVideoEditer` is used to loop a video segment within the time range of A–B.
```
/** Play back a video segment within a time range
 * @param startTime   Playback start time in seconds
 * @param endTime   Playback end time in seconds
 */
- (void)startPlayFromTime:(CGFloat)startTime
                   toTime:(CGFloat)endTime;
```
### 4. Pause and resume preview

```
/// Pause the video
- (void)pausePlay;

/// Resume the video
- (void)resumePlay;

/// Stop the video
- (void)stopPlay;
```

### 5. Add a beauty filter
You can add filter effects such as skin brightening, romantic, and fresh to the video. The demo provides multiple filters (with resources in `Common/Resource/Filter/FilterResource.bundle`) for your choice, and you can also set custom filters.  
You can set a filter as follows:
```
- (void) setFilter:(UIImage *)image;
```
Here, `image` is the filter mapping image. If `image` is set to `null`, the filter effect will be removed.

Demo:
```
TXVideoEditer     *_ugcEdit;
NSString * path = [[NSBundle mainBundle] pathForResource:@"FilterResource" ofType:@"bundle"];
path = [path stringByAppendingPathComponent:@"langman.png"];
UIImage* image = [UIImage imageWithContentsOfFile:path];
[_ugcEdit setFilter:image];
```
### 6. Set a watermark
#### 1. Set a global watermark
You can set a watermark image for the video and specify the image position.
You can set a watermark as follows:  
```
- (void) setWaterMark:(UIImage *)waterMark  normalizationFrame:(CGRect)normalizationFrame;
```  
Here, `waterMark` indicates the watermark image, and `normalizationFrame` is a normalized `frame` value relative to the video image. The values of `x`, `y`, `width`, and `height` in `frame` all range from 0 to 1.

Demo:
```
UIImage *image = [UIImage imageNamed:@"watermark"];  
[_ugcEdit setWaterMark:image normalizationFrame:CGRectMake(0, 0, 0.3 , 0.3 * image.size.height / image.size.width)];// The watermark width is 30% of the video width, and the height is proportionally scaled according to the width
```
#### 2. Set a post-roll watermark
You can set a post-roll watermark for the video and specify the watermark position.
You can set a post-roll watermark as follows:  

```
- (void) setTailWaterMark:(UIImage *)tailWaterMark normalizationFrame:(CGRect)normalizationFrame 
                          duration:(CGFloat)duration;
```  
Here, `tailWaterMark` indicates the post-roll watermark image, and `normalizationFrame` is a normalized frame relative to the video image. The values of `x`, `y`, `width`, and `height` in `frame` all range from 0 to 1. `duration` indicates the watermark duration in seconds.
Demo: set a post-roll watermark that can be displayed for 1 second in the middle of the video image

```
UIImage *tailWaterimage = [UIImage imageNamed:@"tcloud_logo"];
float w = 0.15;
float x = (1.0 - w) / 2.0;
float width = w * videoMsg.width;
float height = width * tailWaterimage.size.height / tailWaterimage.size.width;
float y = (videoMsg.height - height) / 2 / videoMsg.height;
[_ugcEdit setTailWaterMark:tailWaterimage normalizationFrame:CGRectMake(x,y,w,0) duration:1];   

```

## Compressing and Clipping
### Setting video bitrate
```
/**
 * Set the video bitrate
 * @param bitrate   Video bitrate in Kbps
 *                 If the bitrate is set, it will be selected preferably when the SDK compresses videos. Please set an appropriate bitrate. If it is too low, the video image will be blurry; if it is too high, the video size will be too large
 *                 We recommend you set it to a value between 600 and 12000. If this API is not called, the SDK will automatically calculate the bitrate based on the compression quality
 */
- (void) setVideoBitrate:(int)bitrate;
```

### Clipping video
Video editing operations all follow the same principle: set the operation commands first and use `generateVideo` to run all commands in sequence, which can prevent unnecessary quality loss caused by multiple compression operations on the same video.

```objective-c
TXVideoEditer* _ugcEdit = [[TXVideoEditer alloc] initWithPreview:param];
// Set the clipping start and end time
[_ugcEdit setCutFromTime:_videoRangeSlider.leftPos toTime:_videoRangeSlider.rightPos];
// ...
// Generate the final video file
_ugcEdit.generateDelegate = self;
[_ugcEdit generateVideo:VIDEO_COMPRESSED_540P videoOutputPath:_videoOutputPath];
```
Specify the file compression quality and output path during output, and the output progress and result will be returned as a callback through `generateDelegate`.

## Advanced Features

- [TikTok-like special effects](https://intl.cloud.tencent.com/document/product/1069/38028)
- [Setting background music](https://intl.cloud.tencent.com/document/product/1069/38010)
- [Stickers and subtitles](https://intl.cloud.tencent.com/document/product/1069/38032)
- [Editing image](https://intl.cloud.tencent.com/document/product/1069/38036)






