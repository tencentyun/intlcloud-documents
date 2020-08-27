## Reusing Existing UI 
The video splicer has complicated interaction logic, which means that the UI is also complicated; therefore, we recommend you reuse the UI source code in the SDK. The `videojoiner` directory contains the UI source code of the short video splicer.

- `TCVideoJoinerActivity` is used to implement the video splicing list as shown above, which supports drag-up/drag-down for order adjustment.
- `TCVideoJoinerPreviewActivity` is used to preview the spliced video.

## Implementing UI on Your Own
If you do not want to reuse the UI code in the SDK, you can implement the UI on your own as follows:

### 1. Select video files  
Implement the multi-file selection feature on your own.

### 2. Set the preview  
You need to create a `TXVideoJoiner` object for video splicing. Just like `TXVideoEditer`, the preview feature also requires the upper layer to provide the preview `FrameLayout`:

```
// Prepare the preview view        
TXVideoEditConstants.TXPreviewParam param = new TXVideoEditConstants.TXPreviewParam();
param.videoView = mVideoView;
param.renderMode = TXVideoEditConstants.PREVIEW_RENDER_MODE_FILL_EDGE;

// Create a `TXUGCJoiner` object and set the preview view
TXVideoJoiner mTXVideoJoiner = new TXVideoJoiner(this);
mTXVideoJoiner.setTXVideoPreviewListener(this);
mTXVideoJoiner.initWithPreview(param);
// Set the video file group `mVideoSourceList` for splicing, i.e., multiple files selected in step 1
mTXVideoJoiner.setVideoPathList(mVideoSourceList);
```
After setting the preview view and passing in the array of video files to be spliced, you can play back the preview. The splicing module provides some APIs for video playback preview:

- startPlay: starts the video.
- pausePlay: pauses the video.
- resumePlay: resumes the video.

### 3. Generate the final file
If the preview effect is satisfactory, you can call the generation API to generate the spliced file:
```
mTXVideoJoiner.setVideoJoinerListener(this);
mTXVideoJoiner.joinVideo(TXVideoEditConstants.VIDEO_COMPRESSED_540P, mVideoOutputPath);
```
Specify the file compression quality and output path during splicing, and the output progress and result will be returned as a callback through `TXVideoJoiner.TXVideoJoinerListener`.
