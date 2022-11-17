## TXVideoEditer


### Basic editing APIs
| API | Description |
|-----|-----|
| [TXVideoEditer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#ad0ab224b9b23eda9a60e91d7fe5f731f) | The `TXVideoEditer` constructor. |
| [setVideoPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a3d98ae0fe0b5d77c2fe74451be48d7e4) | Specifies the video path. This API works in v18 or later on Android. |
| [setCustomVideoProcessListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a5cc954ae1abd5e31bbee66f6fc108dd7) | Sets the custom image processing callback (not supported in UGSV Lite). |
| [release](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a23b477d0e2d399f75d585d154c346591) | Releases the resources after a video is processed or processing is canceled.                              |

### Effect APIs

| API | Description |
|-----|-----|
| [setSpecialRatio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a1f6b0c14db22ca60390b271ca4295cf5) | Sets the filter strength (not supported in UGSV Lite).                                        |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#ab32d5c2bd4ea611da429aa4975f62ec6) | Sets the filter (not supported in UGSV Lite). |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a260c2d11847a0f5bb04a1048297ab193) | Sets multiple filters (not supported in UGSV Lite).                                        |
| [setBeautyFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a583e0e9653f5653c0d77628cd1768e36) | Sets the beautification and brightening strength (not supported in UGSV Lite). |
| [startEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a5c7153a4f3b01939521c111443ea3c3e) | Sets the start time for an effect (not supported in UGSV Lite).        |
| [stopEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a973981f257551331bf1e64d7fad3ac30) | Sets the end time for an effect (not supported in UGSV Lite).        |
| [deleteLastEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a9efcaf6c76e2fe1be9e389185768df9d) | Removes the last effect applied (not supported in UGSV Lite). |
| [deleteAllEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a002990393f8440c3c0252ed1760c7e75) | Removes all effects (not supported in UGSV Lite).            |

### Video generation APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | ---------------------------- |
| [setCutFromTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a1a7871599c714ffa06d20ea73e1ba7b5) | Sets the start and end time for video clipping.             |
| [setVideoBitrate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a58d953494573c1bd8f578f627bd4a953) | Sets the output video bitrate.             |
| [setAudioBitrate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a626d2ee662300262aa327828ea1e5458) | Sets the output audio bitrate.           |
| [setVideoGenerateListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a58218ba6d4be9ebc79f9e4f81b266b4c) | Registers a listener for video generation.       |
| [generateVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#af3f16bcb21f26c608c980b91671e386e) | Generates a video according to the action list. |
| [cancel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a02d5fa6b14e221f3012a794b905be166) | Cancels generating the video.                 |

### Image transition APIs

| API                                                          | Description                            |
| ------------------------------------------------------------ | --------------------------------- |
| [setPictureList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#ae1305a003cc363651640cafd8dfa6f77) | Specifies the images that are to be converted to a video (not supported in UGSV Lite). |
| [setPictureTransition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a13ff854740fff3897a2ee87c58525400) | Sets the transition effects (not supported in UGSV Lite).  |

### Time effect APIs

| API                                                          | Description                            |
| ------------------------------------------------------------ | ------------------------------- |
| [setSpeedList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a4650c9432c973da02241c81bd2e9002f) | Sets the playback speed for multiple video segments (not supported in UGSV Lite). |
| [setRepeatPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#aa439a109f5f964b6acd2a8c25f5c85a4) | Loops multiple video segments (not supported in UGSV Lite). |
| [setReverse](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a54a93c42a69b8e2c782a9b9cd3cb5ae2) | Plays a video backwards (not supported in UGSV Lite).     |

### Preview APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | -------------------------------------------------- |
| [setTXVideoPreviewListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#aeb200b38997fa6433d552f1480ea67d7) | Registers a listener for video preview.                                   |
| [initWithPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a15115ae00bfecc5fb463eb9eb72ecdcc) | Initializes the view for video preview.                                    |
| [startPlayFromTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a41a3e3f4b9ebe7342a1ad69bc26b0ca2) | Plays a video for a specific time period.                              |
| [pausePlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#af3334d06804b1d47ea3ce5be35dee73e) | Pauses playback.                                           |
| [resumePlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a5ffa3b1cd2080af209af20b86905f22a) | Resumes playback.                                           |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a3d43f5cbda4c56e452cf74ec15d3d148) | Stops playback (releases the resources).                               |
| [previewAtTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#aa223120c3f2b83d3a0965958d86bbf6f) | Previews a frame.                                           |
| [refreshOneFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a9ae65ccf1ecda5e66f1a0ac0bd69eb30) | Refreshes a frame to show the image without ghosting. This is used for the subtitle editing view. |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a1ae55363f74a78d935d63ea7b44130a8) | Sets the rendering rotation (not supported in UGSV Lite).                   |

### Preprocessing APIs

| API                                                          | Description                 |
| ------------------------------------------------------------ | -------------------- |
| [setVideoProcessListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a73e2d92851802d47f78a7f7cd51a9375) | Sets the preprocessing callback. |
| [processVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#aa987a2d8cade3806e3ce06b50bf29761) | Preprocesses a video.         |

### Background music APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ----------------------------------------------------- |
| [setBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#adbd9b380aac0204e378b28d6bc461f01) | Sets the background music (not supported in UGSV Lite).         |
| [setBGMLoop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a2bc4d6ff7be4d3a5be9298894ba9104a) | Sets whether to loop the background music (not supported in UGSV Lite).                   |
| [setBGMAtVideoTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a1a01fa05e3cd6b5af4f47cae951b30c1) | Sets the time point of the video to start playing music (not supported in UGSV Lite). |
| [setBGMStartTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#abbfc8be3c30285988e9e0cffc1d09e8c) | Sets the start and end time of the background music (not supported in UGSV Lite).       |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a7fc2fe760afc4343afc033bb9da93a73) | Sets the volume of the background music (not supported in UGSV Lite).   |
| [setBGMFadeInOutDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#ad213b0abe0efee88eb4d7bcadf7a8747) | Sets fade-in and fade-out effects for the background music (not supported in UGSV Lite).                    |
| [setVideoVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a274f5905b1f86da8e59a9df89f4ab418) | Sets the audio volume of the video (not supported in UGSV Lite).                       |

### Sticker APIs (not supported in UGSV Lite)

| API                                                          | Description                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [setPasterList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a029ea97bf271404576da7448de2c165f) | Sets static stickers (not supported in UGSV Lite).         |
| [setAnimatedPasterList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a98a43a90684ce39cac00b26df2631316) | Sets animated stickers (not supported in UGSV Lite).         |
| [setSubtitleList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a95f8d9e278c5241bea021e62230abb02) | Sets speech bubbles (not supported in UGSV Lite). |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#abf5bb400f1d9d880e13ea59cd9eaadaa) | Adds a watermark. |
| [setTailWaterMark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a0d53a8b66fad82f05167ca4fbe7baee2) | Adds a watermark to the closing segment (not supported in UGSV Lite). |

### Watermark APIs

| API                                                          | Description                        |
| ------------------------------------------------------------ | --------------------------- |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#abf5bb400f1d9d880e13ea59cd9eaadaa) | Sets a global watermark (not supported in UGSV Lite). |
| [setTailWaterMark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a0d53a8b66fad82f05167ca4fbe7baee2) | Adds a watermark to the closing segment (not supported in UGSV Lite). |

### Thumbnail APIs

| API                                                          | Description                  |
| ------------------------------------------------------------ | ------------------------ |
| [getThumbnail](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#aa851032ffa74d6fd94f205eaf0597366) | Gets the thumbnail list.           |
| [getThumbnail](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a151333765a1e2c98ea32fe13ea0cb655) | Gets the thumbnail list.           |
| [setThumbnail](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#ade2a9534fa3075883c551ce0163170c1) | Sets the thumbnail output by preprocessing.   |
| [setThumbnailListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a5baec0d91487fe6238f7e42879611e12) | Sets the callback for thumbnail generation by preprocessing. |
| [getThumbnailCount](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a5693e8dcdff926c7b840f5e49e5e47e4) | Gets the number of thumbnails.           |

## TXVideoGenerateListener

### Editing callback APIs

| API                                                                                                       | Description                                                                                                                                                                            |
| ------------------------------------------------------------ | ------------------ |
| [onGenerateProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a07581798fba77eead03ff37c74065384) | The video generation progress. |
| [onGenerateComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#ae21c7177a91d25583ba6a0ad869093fe) | A video was generated.     |

## TXVideoPreviewListener

### Preview callback APIs

| API                                                          | Description                  |
| ------------------------------------------------------------ | ----------------------- |
| [onPreviewProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a35112d6d255e810bd6798ceefb5d5683) | The current preview time, in microseconds. |
| [onPreviewFinished](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#afecc9f5e883fc46fa1cb0bb138d3cb3b) | The preview ended.      |

## TXVideoPreviewListenerEx

### Preview callback APIs

| API                                                          | Description                  |
| ------------------------------------------------------------ | ------------------------ |
| [onPreviewError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a61b3cb359e53a90564a5de1280b91223) | An error occurred during video generation. |
| [onPreviewProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a35112d6d255e810bd6798ceefb5d5683) | The preview progress, in microseconds. |
| [onPreviewFinished](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#afecc9f5e883fc46fa1cb0bb138d3cb3b) | The preview ended.      |

## TXVideoProcessListener

### Preprocessing callback APIs

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| [onProcessProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#ac427df27a7b92aa07d84f17c9786fa1f) | The preprocessing progress. |
| [onProcessComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#ac3343cd2111bf3b946b83fbc7149565f) | The preprocessing was completed. |

## TXVideoCustomProcessListener

### Custom processing callback APIs

| API                                                                                                            | Description                                                                                                                                                                                     |
| ------------------------------------------------------------ | ---------------------------------------------- |
| [onTextureCustomProcess](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#af862bdc5a54f4097f9449bf4ef91d1d6) | The texture callback. You can process the video by yourself in this callback. |
| [onTextureDestroyed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#ac60f1dbbb1af39c666247c6438595de0) | The texture releasing callback. You can release the OpenGL resources in this callback. |

## TXThumbnailListener

### Thumbnail callback APIs

| API | Description |
| ------------------------------------------------------------ | -------------- |
| [onThumbnail](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__android.html#a2da29d316c2d34ab3977fe3f7686d5fa) | The thumbnail callback. |

## TXVideoEditConstants

### Definitions of editing key types
| API | Description |
|-----|-----|
| [TXVideoInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXVideoInfo) | The video information. |
| [TXPreviewParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXPreviewParam) | The preview parameters.               |
| [TXGenerateResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXGenerateResult) | The editing result.               |
| [TXPreviewError](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXPreviewError) | Preview errors.               |
| [TXJoinerResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXJoinerResult) | The generation result.               |
| [TXSubtitle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXSubtitle) | The subtitle information.                         |
| [TXPaster](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXPaster) | The static sticker information.                     |
| [TXAnimatedPaster](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXAnimatedPaster) | The animated sticker information.                     |
| [TXSpeed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXSpeed) | The speed changing information.                         |
| [TXRect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXRect) | The area to which the watermark is applied.                     |
| [TXThumbnail](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXThumbnail) | The thumbnail information.                       |
| [TXRepeat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXRepeat) | The looped segment.                     |
| [TXAbsoluteRect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditConstants__android.html#classcom_1_1tencent_1_1ugc_1_1TXVideoEditConstants_1_1TXAbsoluteRect) | The position and dimensions of each video. |


[](id:error)
## Error Codes

### Editing result

| Message                                         | Code   | Description                                                         |
| ------------------------------------------- | ---- | ------------------------------ |
| GENERATE_RESULT_OK                          | 0    | The video was generated successfully.                   |
| GENERATE_RESULT_FAILED                      | -1   | Failed to generate the video.                   |
| GENERATE_RESULT_LICENCE_VERIFICATION_FAILED | -5   | Failed to generate the video due to a license verification error. |

### Preview

| Message                                         | Code   | Description                                                         |
| ------------------------------- | ---- | ------------------ |
| PREVIEW_ERROR_VIDEO_DECODE_FAIL | -1   | Failed to preview the video due to a decoding error. |
