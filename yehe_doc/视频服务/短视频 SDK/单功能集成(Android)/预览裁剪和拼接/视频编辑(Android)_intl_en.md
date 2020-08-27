## Feature Overview
Video editing includes features such as video clipping, time-based special effects (slow motion, reverse, and loop), special effect filters (dynamic light-wave, darkness and phantom, soul out, and cracked screen), filter styles (aesthetic, rosy, blues, etc.), music mix, animated stickers, static stickers, and bubble subtitles.

## Overview of Relevant Classes 
| Class Name | Feature  |
| ------------- | --------- |
| `TXVideoInfoReader`| Gets media information |
| `TXVideoEditer` | Edits video |

## Use Instructions
The following is the basic usage process of video editing:

1. Set the video path.
2. Import the video.
3. Add effects.
4. Generate a video and output it to a specified file.
5. Listen on the generation event.
6. Release the resources.


## Getting Video Information
The **getVideoFileInfo** method of **TXVideoInfoReader** can get certain basic information of a specified video file. The relevant APIs are as detailed below:
```
/**
  * Get the video information
  * @param videoPath   Video file path
  * @return
  */
public TXVideoEditConstants.TXVideoInfo getVideoFileInfo(String videoPath);
```
The returned `TXVideoInfo` is defined as follows:

```
public final static class TXVideoInfo {
        public Bitmap coverImage;                                // Image of the first video frame
        public long duration;                                         // Video duration in milliseconds
        public long fileSize;                                          // Video size in bytes
        public float fps;                                                // Video frame rate in fps
        public int bitrate;                                              // Video bitrate in Kbps
        public int width;                                               // Video width
        public int height;                                               // Video height
        public int audioSampleRate;                              // Audio bitrate
 }
```
Below is a complete sample:
```
// `sourcePath` is the source video path
String sourcePath = Environment.getExternalStorageDirectory() + File.separator + "temp.mp4";
TXVideoEditConstants.TXVideoInfo info = TXVideoInfoReader.getInstance().getVideoFileInfo(sourcePath);
```
## Getting Thumbnail
The thumbnail APIs are mainly used to generate the preview thumbnails displayed on the video editing page, get the video cover, and perform other relevant operations.
### 1. Get the thumbnails evenly distributed along the video duration by number
#### Generating precise thumbnails after quick import
The following API will be called:
```
/**
  * Get the thumbnail list
  * @param count   Number of thumbnails
  * @param width   Thumbnail width
  * @param height   Thumbnail height
  * @param fast   Whether the thumbnails are keyframe images
  * @param listener   Thumbnail callback function
*/
public void getThumbnail(int count, int width, int height, boolean fast, TXThumbnailListener listener)
```

The `@param fast` parameter can be set to either of the following two modes:
>- Quick output: the thumbnails can be quickly output but do not precisely match the video points in time. You can use this mode by setting the parameter to `true`.
>- Precise output: the output thumbnails precisely match the video points in time, but the process is slower for videos with high resolution. You can use this mode by setting the parameter to `false`.

Below is a complete sample:
```
mTXVideoEditer.getThumbnail(TCVideoEditerWrapper.mThumbnailCount, 100, 100, false, mThumbnailListener);

private TXVideoEditer.TXThumbnailListener mThumbnailListener = new TXVideoEditer.TXThumbnailListener() {
 	@Override
        public void onThumbnail(int index, long timeMs, final Bitmap bitmap) {
        	Log.i(TAG, "onThumbnail: index = " + index + ",timeMs:" + timeMs);
		// Place the thumbnails onto the image control
        }
    };
```
#### Getting thumbnails after full-featured import
For more information, please see [Importing Video](#p1).

### 2. Get thumbnails according to the list of points in time
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
>- A point in time in `List` cannot exceed the total video duration; otherwise, the last-frame image will be returned for it.
>- The set points in time should be in milliseconds (ms).

## Importing Video
### 1. Quick import
Quick video import allows you to directly preview video editing effects and supports features such as video clipping, time-based special effect (slow motion), special effect filters, filter styles, music mix, animated stickers, static stickers, and bubble subtitles, but does not support certain time-based special effects (loop and reverse).

### <span id ="p1"></span> 2. Full-featured import
Full-featured import supports all features, including the loop and reverse time-based special effects, but it requires video preprocessing.
After full-featured import, each point in time in a video can be precisely sought, and the corresponding image will be displayed. The video thumbnail at any selected precise point in time can be generated during preprocessing.

Full-featured import consists of the following steps and needs to call the following APIs:
1. Set the precise output thumbnails.
```
/**
  * Set the thumbnails to be output by preprocessing
  */
public void setThumbnail(TXVideoEditConstants.TXThumbnail thumbnail)
```
2. Set the callback for thumbnail output.
```
/**
  * Set the callback for thumbnail output by preprocessing
  * @param listener
  */
public void setThumbnailListener(TXThumbnailListener listener)
```
>!We recommend you restrain from setting the thumbnail width and height to the video width and height for higher zooming efficiency in the SDK.
3. Set the callback API for video preprocessing.
```
/**
  * Set the callback for video preprocessing
  * @param listener
  */
public void setVideoProcessListener(TXVideoProcessListener listener)
```
4. Preprocess the video.
```
public void processVideo();
```

Below is a complete sample:
```
int thumbnailCount = 10;  // Number of thumbnails to be generated by video duration
TXVideoEditConstants.TXThumbnail thumbnail = new TXVideoEditConstants.TXThumbnail();
thumbnail.count = thumbnailCount;
thumbnail.width = 100;   // Output thumbnail width
thumbnail.height = 100;  // Output thumbnail height
mTXVideoEditer.setThumbnail(thumbnail);                               // Set the thumbnails to be generated by preprocessing
mTXVideoEditer.setThumbnailListener(mThumbnailListener); // Set the thumbnail callback

mTXVideoEditer.setVideoProcessListener(this);                       // Callback for video preprocessing progress
mTXVideoEditer.processVideo();                                               // Preprocess the video
```

## Editing and Previewing
Video editing supports two effect preview modes: pinpoint preview (the video image is frozen at a specified point in time) and range preview (a video segment within a specified time range (A–B) is looped). To use a preview mode, you need to bind a `UIView` to the SDK in order to display the video image.

### 1. Set the Layout for preview playback
```
public void initWithPreview(TXVideoEditConstants.TXPreviewParam param)
```
When setting the preview `Layout`, you can set two video image rendering modes, which are defined in the `TXVideoEditConstants` constant:
```
public final static int PREVIEW_RENDER_MODE_FILL_SCREEN = 1;   // Fill mode, where the video image will cover the entire screen with no black bars present, but the video image may be cropped
public final static int PREVIEW_RENDER_MODE_FILL_EDGE = 2;        // Fit mode, where the video image will be complete but black bars will exist if the aspect ratio of the video is different from that of the screen
```
### 2. Use pinpoint preview
After [full-featured import](#p1), the video image at each point in time in the video can be previewed precisely.
```
public void previewAtTime(long timeMs);
```
### 3. Use range preview
The `startPlayFromTime` function of `TXVideoEditer` is used to loop a video segment within the time range of A–B.
```
// Play back a video segment between `startTime` and `endTime`
public void startPlayFromTime(long startTime, long endTime);
```
### 4. Pause and resume preview
```
// Pause the video
public void pausePlay();

// Resume the video
public void resumePlay();

// Stop the video
public void stopPlay();
```

### 5. Add a beauty filter
You can add filter effects such as skin brightening, romantic, and fresh to the video. The demo provides 16 filters for your choice, and you can also set custom filters.

You can set a filter as follows:
```
void setFilter(Bitmap bmp)
```
Here, `Bitmap` is the filter mapping image. If `bmp` is set to `null`, the filter effect will be removed.

```
void setSpecialRatio(float specialRatio)
```
This API can adjust the filter level, which generally ranges from 0.0 to 1.0.

```
void setFilter(Bitmap leftBitmap, float leftIntensity, Bitmap rightBitmap, float rightIntensity, float leftRatio)
```
This API can implement filter mix, i.e., different filters can be added on the left and right, respectively. `leftBitmap` indicates the left filter, `leftIntensity` the level of the left filter, `rightBitmap` the right filter, `rightIntensity` the level of the right filter, and `leftRatio` the ratio of the dimensions of the left filter, which generally ranges from 0.0–1.0. If `leftBitmap` or `rightBitmap` is `null`, the filter effect on the corresponding side will be removed.

### 6. Add a watermark
#### 1. Set a global watermark
You can set a watermark image for the video and specify the image position.

You can set a watermark as follows:
```
public void setWaterMark(Bitmap waterMark, TXVideoEditConstants.TXRect rect);
```
Here, `waterMark` indicates the watermark image, and `rect` is a normalized `frame` value relative to the video image. The values of `x`, `y`, `width`, and `height` in `frame` all range from 0 to 1.

Demo:
```
TXVideoEditConstants.TXRect rect = new TXVideoEditConstants.TXRect();
rect.x = 0.5f;
rect.y = 0.5f;
rect.width = 0.5f;
mTXVideoEditer.setWaterMark(mWaterMarkLogo, rect);
```
#### 2. Set a post-roll watermark
You can set a post-roll watermark for the video and specify the watermark position.
You can set a post-roll watermark as follows:

```
setTailWaterMark(Bitmap tailWaterMark, TXVideoEditConstants.TXRect txRect, int duration);
```

Here, `tailWaterMark` indicates the post-roll watermark image, and `txRect` is a normalized value relative to the video image. The values of `x`, `y`, and `width` in `txRect` all range from 0 to 1. `duration` indicates the watermark duration in seconds.
Demo: set a post-roll watermark that can be displayed for 3 seconds in the middle of the video image
```
Bitmap tailWaterMarkBitmap = BitmapFactory.decodeResource(getResources(), R.drawable.tcloud_logo);
TXVideoEditConstants.TXRect txRect = new TXVideoEditConstants.TXRect();
txRect.x = (mTXVideoInfo.width - tailWaterMarkBitmap.getWidth()) / (2f * mTXVideoInfo.width);
txRect.y = (mTXVideoInfo.height - tailWaterMarkBitmap.getHeight()) / (2f * mTXVideoInfo.height);
txRect.width = tailWaterMarkBitmap.getWidth() / (float) mTXVideoInfo.width;
mTXVideoEditer.setTailWaterMark(tailWaterMarkBitmap, txRect, 3);
```

## Compressing and Clipping
### Setting video bitrate
Currently, the video bitrate can be customized. We recommend you set a bitrate between 600 and 12,000 Kbps. If the bitrate is set, it will be selected preferably when the SDK compresses videos. Please set an appropriate bitrate. If it is too high, the video size will be too large; if it is too low, the video image will be blurry.
```
public void setVideoBitrate(int videoBitrate);
```

### Clipping video
Set the start and end time for video clipping.
```
/**
  * Set the video clipping range
  * @param startTime   Start time for video clipping in milliseconds
  * @param endTime   End time for video clipping in milliseconds
  */
public void setCutFromTime(long startTime, long endTime)

// ...
// Generate the final video file
public void generateVideo(int videoCompressed, String videoOutputPath)
```

Valid constants of the `videoCompressed` parameter in `TXVideoEditConstants` include:
```
VIDEO_COMPRESSED_360P   Compress the video to 360p resolution (360x640)
VIDEO_COMPRESSED_480P   Compress the video to 480p resolution (640x480)
VIDEO_COMPRESSED_540P   Compress the video to 540p resolution (960x540)
VIDEO_COMPRESSED_720P —— Compress the video to 720p resolution (1280x720)
```
If the resolution of the source video is lower than that set in the constant, the original resolution will be used.
If the resolution of the source video is greater than that set in the constant, the set resolution will be used for video compression.

## Releasing Resource
If you no longer use the `mTXVideoEditer` object, you must call **release()** to release it.

## Advanced Features
- [TikTok-like special effects](https://intl.cloud.tencent.com/document/product/1069/38029)
- [Setting background music](https://intl.cloud.tencent.com/document/product/1069/38022)
- [Stickers and subtitles](https://intl.cloud.tencent.com/document/product/1069/38033)
- [Editing image](https://intl.cloud.tencent.com/document/product/1069/38037)
