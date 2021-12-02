## Overview
Video editing supports clipping, time effects (slow motion, reverse, loop), filters (rock light, dark dream, soul out, screen split), filter styles (artistic, rosy, blues, etc.), music mixing, animated stickers, static stickers, bubble subtitles, etc.

## Classes 
| Class                     | Description                                         |
| ------------- | --------- | 
| `TXVideoInfoReader`| Media information obtaining |
| `TXVideoEditer` | Video editing |

## Directions
Follow the steps below to edit your video: 

1. Choose the video path
2. Import your video
3. Apply effects
4. Generate a file of the editing result
5. Listen for the callback for video generation
6. Release the resources


## Getting Video Information
You can use **getVideoFileInfo** of **TXVideoInfoReader** to obtain some basic video information. Below is a request sample:
```
/**
  * Acquire video information
  * @param videoPath Video file path
  * @return
  */
public TXVideoEditConstants.TXVideoInfo getVideoFileInfo(String videoPath);
```
`TXVideoInfo` is returned and is defined as follows:

```
public final static class TXVideoInfo {
        public Bitmap coverImage;                                // First video frame
        public long duration;                                         // Video duration (ms)
        public long fileSize;                                          // Video file size (byte)
        public float fps;                                                // Video frame rate (fps)
        public int bitrate;                                              // Video bitrate (Kbps)
        public int width;                                               // Video width
        public int height;                                               // Video height
        public int audioSampleRate;                              // Audio bitrate
 }
```
Below is a complete sample:
```
//sourcePath Path of the video to edit
String sourcePath = Environment.getExternalStorageDirectory() + File.separator + "temp.mp4";
TXVideoEditConstants.TXVideoInfo info = TXVideoInfoReader.getInstance().getVideoFileInfo(sourcePath);
```
## Getting Thumbnails
The thumbnail obtaining API is used to generate thumbnail preview during video editing or get the cover of a video.
### 1. Get thumbnails by splitting a video evenly
#### Quick generation
Below is a request sample:
```
/**
  * Get the thumbnail list
  * @param count    Number of thumbnails to get
  * @param width    Thumbnail width
  * @param height   Thumbnail height
  * @param fast       Whether to get keyframes
  * @param listener Callback API for thumbnail generation
*/
public void getThumbnail(int count, int width, int height, boolean fast, TXThumbnailListener listener)
```

The @param fast parameter supports two modes:
-Quick generation: Pass in `true` to use this mode, under which thumbnails are generated relatively quickly, but they may not correspond exactly to video frames.
-Precise generation: Pass in `false` to use this mode, under which the thumbnails generated correspond exactly to video frames, but the generation may be slow if the resolution is high.

Below is a complete sample:
```
mTXVideoEditer.getThumbnail(TCVideoEditerWrapper.mThumbnailCount, 100, 100, false, mThumbnailListener);

private TXVideoEditer.TXThumbnailListener mThumbnailListener = new TXVideoEditer.TXThumbnailListener() {
    @Override
        public void onThumbnail(int index, long timeMs, final Bitmap bitmap) {
            Log.i(TAG, "onThumbnail: index = " + index + ",timeMs:" + timeMs);
        // Insert the thumbnails into the image control
        }
    };
```
#### Precise generation
See [Importing Video](#p1) below.

### 2. Get thumbnails according to the time list
```
List<Long> list = new ArrayList<>();
list.add(10000L);
list.add(12000L);
list.add(13000L);
list.add(14000L);
list.add(15000L);

TXVideoEditer txVideoEditer = new TXVideoEditer(TCVideoPreviewActivity.this);
txVideoEditer.setVideoPath(mVideoPath);
txVideoEditer.setThumbnailListener(new TXVideoEditer.TXThumbnailListener() {
       @Override
       public void onThumbnail(int index, long timeMs, Bitmap bitmap) {
           Log.i(TAG, "bitmap:" + bitmap + ",timeMs:" + timeMs);
           saveBitmap(bitmap, timeMs);
       }
});
txVideoEditer.getThumbnailList(list, 200, 200);
```
>!
>- If a time point in the list is larger than the total video duration, the last video frame will be returned.
>- Time points in the list are measured in milliseconds.

## Importing Video
### 1. Quick import
This mode supports preview during editing. You can trim a video, play a video in slow motion, apply filters, change the filter style, mix music, and add animated/static stickers and bubble subtitles, among others. It does not support video looping or reversing.

[](id:p1)
### 2. Complete import
This mode supports all video editing features, including the time effects looping and reversing. Videos are pre-processed in this mode.
In this mode, you can locate any time point of a video and view the corresponding video frame. Thumbnails that correspond exactly to video frames are also generated during pre-processing.

The steps of complete import and the APIs used during the process are as follows:
1.Configure precise generation of thumbnails
```
/**
  * Configure the thumbnails generated during pre-processing
  */
public void setThumbnail(TXVideoEditConstants.TXThumbnail thumbnail)
```
2. Configure the callback for thumbnail generation
```
/**
  * Configure the callback for thumbnail generation during pre-processing
  * @param listener
  */
public void setThumbnailListener(TXThumbnailListener listener)
```
>! We recommend you do not specify thumbnail width or height as scaling by the SDK is more efficient.
3. Configure the callback for video pre-processing
```
/**
  * Configure the callback for video pre-processing
  * @param listener
  */
public void setVideoProcessListener(TXVideoProcessListener listener)
```
4. Pre-process videos
```
public void processVideo();
```

Below is a complete sample:
```
int thumbnailCount = 10;  //Number of thumbnails to generate
TXVideoEditConstants.TXThumbnail thumbnail = new TXVideoEditConstants.TXThumbnail();
thumbnail.count = thumbnailCount;
thumbnail.width = 100;   // Thumbnail width
thumbnail.height = 100;  // Thumbnail height
mTXVideoEditer.setThumbnail(thumbnail);                               // Configure the thumbnails generated during pre-processing
mTXVideoEditer.setThumbnailListener(mThumbnailListener); //  Configure the callback for thumbnail generation

mTXVideoEditer.setVideoProcessListener(this);                       // Configure the callback of video pre-processing progress
mTXVideoEditer.processVideo();                                               // Pre-process videos
```

## Preview
You can preview a video during editing in two modes. Time-point preview shows the frame of a certain time point, while time-range preview plays a video segment between two time points on loop (A<=>B). You need to bind the SDK with a UIView to display video images.

### 1. Configure preview layout
```
public void initWithPreview(TXVideoEditConstants.TXPreviewParam param)
```
Two video rendering modes are supported, which are defined in the constant `TXVideoEditConstants`.
```
public final static int PREVIEW_RENDER_MODE_FILL_SCREEN = 1;   // Aspect fill. The image is stretched to fill the entire screen, and the excess parts are cropped.
public final static int PREVIEW_RENDER_MODE_FILL_EDGE = 2;        // Aspect fit. The image is kept intact, and there may be black bars if the aspect ratio does not match.
```
### 2. Time-point preview
You can locate any time point of a video imported in the [complete import](#p1) mode.
```
public void previewAtTime(long timeMs);
```
### 3. Time-range preview
You can use `startPlayFromTime` of `TXVideoEditer` to play a video segment between two time points (A<=>B).
```
// Play a segment of a video from `startTime` to `endTime`
public void startPlayFromTime(long startTime, long endTime);
```
### 4. Pause and resume preview
```
// Pause preview
public void pausePlay();


// Resume preview
public void resumePlay();


// Stop preview
public void stopPlay();
```

### 5. Add beauty filter
You can apply filter effects such as skin brightening, romantic, and refreshing to your video. The demo offers 16 filters. You can also customize filters.

The method to set filter is:
```
void setFilter(Bitmap bmp)
```
A bitmap is a mapping of the filter image. Setting `bmp` to null means to remove the filter effect.

```
void setSpecialRatio(float specialRatio)
```
You can use this API to set the filter strength on a scale of 0.0 to 1.0.

```
void setFilter(Bitmap leftBitmap, float leftIntensity, Bitmap rightBitmap, float rightIntensity, float leftRatio)
```
You can use this API to apply different filters to the left and right sections of your video. `leftBitmap` represents the left filter and `leftIntensity` the strength of the left filter. `rightBitmap` represents the right filter and `rightIntensity` the strength of the right filter. `leftRatio` indicates the ratio (0.0-1.0) of the image section the left filter is applied to. If `leftBitmap` or `rightBitmap` is set to null, the filter effect for the corresponding section will be removed.

### 6. Watermark
#### 1. Add a global watermark
You can add a watermark to a specified position of a video.

The method to add a watermark is as follows:
```
public void setWaterMark(Bitmap waterMark, TXVideoEditConstants.TXRect rect);
```
`waterMark` represents the watermark image. `rect` is the normalized frame of the watermark image in relation to the video image. The value range of `x`, `y`, `width`, and `height` is 0 to 1.

Demo:
```
TXVideoEditConstants.TXRect rect = new TXVideoEditConstants.TXRect();
rect.x = 0.5f;
rect.y = 0.5f;
rect.width = 0.5f;
mTXVideoEditer.setWaterMark(mWaterMarkLogo, rect);
```
#### 2. Add an ending watermark
You can add a watermark to the end of a video at the specified location.
The method to add an ending watermark is as follows:

```
setTailWaterMark(Bitmap tailWaterMark, TXVideoEditConstants.TXRect txRect, int duration);
```

`tailWterMark` represents the watermark image. `txRect` is the normalized frame of the watermark image in relation to the video image, and the value range of `x`, `y`, and `width` in `txRect` is from 0 to 1. `duration` indicates for how long (s) the watermark is displayed.
Demo: add an ending watermark to the center of a video and show the watermark for 3 seconds
```
Bitmap tailWaterMarkBitmap = BitmapFactory.decodeResource(getResources(), R.drawable.tcloud_logo);
TXVideoEditConstants.TXRect txRect = new TXVideoEditConstants.TXRect();
txRect.x = (mTXVideoInfo.width - tailWaterMarkBitmap.getWidth()) / (2f * mTXVideoInfo.width);
txRect.y = (mTXVideoInfo.height - tailWaterMarkBitmap.getHeight()) / (2f * mTXVideoInfo.height);
txRect.width = tailWaterMarkBitmap.getWidth() / (float) mTXVideoInfo.width;
mTXVideoEditer.setTailWaterMark(tailWaterMarkBitmap, txRect, 3);
```

## Compression and Clipping
### Setting video bitrate
You can specify a custom value, preferably between 600 and 12000 (Kbps), for video bitrate. The SDK will prioritize the bitrate set during video compression. Do not set the bitrate too high or too low. The former drives up the size of video files, and the latter results in blurry videos.
```
public void setVideoBitrate(int videoBitrate);
```

### Clipping video
Set the start and end time for clipping
```
/**
  * Specify the time range for video clipping
  * @param startTime Start time (ms) for clipping
  * @param endTime   End time (ms) for clipping
  */
public void setCutFromTime(long startTime, long endTime)


// ...
// Generate the video file
public void generateVideo(int videoCompressed, String videoOutputPath)
```

The constants of `videoCompressed` in `TXVideoEditConstants` are as follows:
```
VIDEO_COMPRESSED_360P – Compress to 360p (360 × 640)
VIDEO_COMPRESSED_480P – Compress to 480p (640 × 480)
VIDEO_COMPRESSED_540P – Compress to 540p (960 × 540)
VIDEO_COMPRESSED_720P – Compress to 720p (1280 × 720)
```
If the resolution of the original video is lower than the configured constant, the original resolution will be used.
If the resolution of the original video is higher than the configured constant, the video will be compressed to the configured resolution.

## Releasing Resources
When you no longer use the `mTXVideoEditer` object, be sure to call **release()** to release it.

## Advanced Features
- [TikTok-like Special Effects](https://intl.cloud.tencent.com/document/product/1069/38029)
- [Adding Background Music](https://intl.cloud.tencent.com/document/product/1069/38022)
- [Stickers and Subtitles](https://intl.cloud.tencent.com/document/product/1069/38033)
- [Image Transition Special Effects](https://intl.cloud.tencent.com/document/product/1069/38037)
