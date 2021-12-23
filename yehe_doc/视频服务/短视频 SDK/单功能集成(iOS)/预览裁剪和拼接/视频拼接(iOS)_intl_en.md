## Reusing Existing UI
The video splicer has complicated interaction logic, which means that the UI is also complicated; therefore, we recommend you reuse the UI source code in the SDK. The `VideoJoiner` directory contains the UI source code of the short video splicer. 

- **VideoJoinerController**: it is used to implement the video splicing list as shown above, which supports drag-up/drag-down for order adjustment.
- **VideoJoinerCell**: it is used to splice all video segments in the list.
- **VideoEditPrevController**: it is used to preview the spliced video.

## Implementing UI on Your Own
If you do not want to reuse the UI code in the SDK, you can implement the UI on your own as follows:
 
### 1. Select video files
In the demo, the `QBImagePicker ` open-source library is used to implement the multi-file selection feature. The relevant code can be found in `MainViewController` of the demo.

### 2. Set the preview view
You need to create a `TXVideoJoiner` object for video splicing. Just like `TXUGCEditer`, the preview feature also requires the upper layer to provide the preview `UIView`:

```objective-c
// Prepare the preview view
TXPreviewParam *param = [[TXPreviewParam alloc] init];
param.videoView = _videoPreview.renderView;
param.renderMode = PREVIEW_RENDER_MODE_FILL_EDGE;

// Create a `TXVideoJoiner` object and set the preview view
TXVideoJoiner* _videoJoin = [[TXVideoJoiner alloc] initWithPreview:param];
_videoJoin.previewDelegate = _videoPreview;

// Set the video file group `_composeArray` for splicing, i.e., multiple files selected in step 1
[_videoJoin setVideoPathList:_composeArray];
```

After setting the preview view and passing in the array of video files to be spliced, you can play back the preview. The splicing module provides some APIs for video playback preview:

*  `startPlay`: starts the video.
*  `pausePlay`: pauses the video.
*  `resumePlay`: resumes the video.

### 3. Generate the final file
If the preview effect is satisfactory, you can call the generation API to generate the spliced file:
```objective-c
_videoJoin.joinerDelegate = self;
[_videoJoin joinVideo:VIDEO_COMPRESSED_540P videoOutputPath:_outFilePath];
```

Specify the file compression quality and output path during splicing, and the output progress and result will be returned as a callback through `joinerDelegate`.
