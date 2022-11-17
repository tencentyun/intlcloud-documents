## TXVideoEditer

### Constructor API

| API | Description |
| :----------------- | -------------- |
| [initWithPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a3c1008d9861aec98ac2f1e70f801c2c8) | The default initialization method. |

### Video/Image setting APIs

| API                                                 | Description                                                                                                                   |
| :----------------- | ------------ |
| [setVideoPath](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#af98d827c56a0a50893afb1ef358ef36c) | Specifies the video path.          |
| [setVideoAsset](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a481fdf89e37b523f53bafe15e2ab3a3b) | Sets AVAsset.          |
| [setPictureList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#ab4a88a0f32702ee4c732d873d8804ac1) | Specifies the images that are to be converted to a video (not supported in UGSV Lite). |
| [setPictureTransition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a7a934af28bb7059f9f1e03252cd7aa71) | Sets the transition effects (not supported in UGSV Lite). |



### Preview APIs

| API | Description |
| :----------------- | ---------------------- |
| [previewAtTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#ac179878f3f6c91d17bb60624a5029d56) | Renders the image at a specific time point of the video. |
| [startPlayFromTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a0a2615f86cacd81305abb2395d7f81d7) | Plays a video for a specific time period.                              |
| [pausePlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#af3334d06804b1d47ea3ce5be35dee73e) | Pauses playback.                                           |
| [resumePlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a5ffa3b1cd2080af209af20b86905f22a) | Resumes playback.                                           |
| [stopPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a3d43f5cbda4c56e452cf74ec15d3d148) | Stops playback (releases the resources).                               |



### Effect APIs

| API                                                                                                            | Description                                                                                                                                                                                     |
| :----------------- | ------------------ |
| [setBeautyFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#afe970c160baf293e9729455317518339) | Sets the beautification and brightening strength (0-9). |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a05ed2f02c5b5514d7342ab50d4052d59) | Sets the filter.            |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a44d7f0da7adb1aa2f62a3afd6d7c4b1c) | Sets two filters.                |
| [setSpecialRatio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a6de9ce92116926fe9b53016151d55784) | Sets the filter strength.                                        |
| [setReverse](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a3101209b2c2f5acb2dfffbcb126dd650) | Plays a video backwards (not supported in UGSV Lite).     |
| [setRepeatPlay](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a43b71deca5d9f529a12fa08cfcd71860) | Loops video segments (not supported in UGSV Lite). |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#aedfa7b798e073a450c2b2fbb5063955c) | Sets the rendering rotation (not supported in UGSV Lite).                   |
| [setSpeedList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a920e34fb4cd1a3818a400e02ae1c39f0) | Sets the playback speed (not supported in UGSV Lite). |
| [startEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#af6ef3fab8f2d5871c2b63571daf0f6a8) | Starts an effect (not supported in UGSV Lite).        |
| [stopEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a23fd51ba880b96b3d00fa4c5c50a0cd0) | Stops an effect (not supported in UGSV Lite).       |
| [deleteLastEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a9efcaf6c76e2fe1be9e389185768df9d) | Removes the last effect applied (not supported in UGSV Lite). |
| [deleteAllEffect](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a002990393f8440c3c0252ed1760c7e75) | Removes all effects (not supported in UGSV Lite).            |



### Sticker APIs (not supported in UGSV Lite)

| API                                                                                                            | Description                                                                                                                                                                                     |
| :----------------- | ---------------- |
| [setSubtitleList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a61765dfd460768954def11cb8f615d0f) | Sets speech bubbles (not supported in UGSV Lite). |
| [setPasterList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a66ea4fd1f8f4170d2551ace9d7ef7e07) | Sets static stickers (not supported in UGSV Lite).         |
| [setAnimatedPasterList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a979a0d339aef335525f1a7c92b6ab930) | Sets animated stickers (not supported in UGSV Lite).         |



### Background music APIs

| API                                                                                                            | Description                                                                                                                                                                                     |
| :----------------- | ------------------------------ |
| [setBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a59a3956d1bdeb12a0701d48c5e85259a) | Sets the background music (not supported in UGSV Lite).                   |
| [setBGMAsset](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a89357b40d1c45c47a1e1ecee47d45476) | Sets the background music (not supported in UGSV Lite).         |
| [setBGMStartTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a26de512c64562ba0d2eeccdde7c6c9e5) | Sets the start and end time of the background music (not supported in UGSV Lite).       |
| [setBGMLoop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#af04ec84d6367837b6a3ec009d42f3dc1) | Sets whether to loop the background music (not supported in UGSV Lite).         |
| [setBGMAtVideoTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#aef28b77ad3642c0a608887a94b155b31) | Sets the time point of the video to start playing music (not supported in UGSV Lite). |
| [setVideoVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a113de64447f37f924a8493e2cc2216ed) | Sets the audio volume of the video (not supported in UGSV Lite).                       |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a9a8155eedd2621ab628f4e503f1e8d72) | Sets the volume of the background music (not supported in UGSV Lite).   |
| [setBGMFadeInDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a23e629dc5ddffaaadb994e3e9095986d) | Sets fade-in and fade-out effects for the background music (not supported in UGSV Lite).                    |



### Watermark APIs

| API                                                                                                            | Description                                                                                                                                                                                     |
| :----------------- | -------- |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a7ee69499e0ca3bd9a7c996505725c384) | Sets a global watermark (not supported in UGSV Lite). |
| [setTailWaterMark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditer__ios.html#a023510027d5c1238f61004b4309432ee) | Adds a watermark to the closing segment (not supported in UGSV Lite). |



## TXVideoPreviewListener

### Preview callback APIs

| API                                                                                                            | Description                                                                                                                                                                                     |
| :----------------- | ------------------------- |
| [onPreviewProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerListener__ios.html#a80858908a27f740310ba970700624e78) | The current preview time of the video, in seconds. |
| [onPreviewFinished](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerListener__ios.html#afecc9f5e883fc46fa1cb0bb138d3cb3b) | The preview ended.      |



## TXVideoCustomProcessListener

### Custom processing callback APIs

| API                                                                                                            | Description                                                                                                                                                                                     |
| :----------------- | ------------------------- |
| [onPreProcessTexture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerListener__ios.html#a291f788c080dc4fb941ff5a955e249de) | The texture callback. You can process the video by yourself in this callback. |
| [onTextureDestoryed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerListener__ios.html#a837386fa6d1b5614758950415132ba54) | The texture releasing callback. You can release the OpenGL resources in this callback. |



## TXVideoGenerateListener

### Editing callback APIs

| API | Description |
| :----------------- | ------------------ |
| [onGenerateProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerListener__ios.html#aba8d22bff87bcf57b5983943ed8e80b2) | The video generation progress. |
| [onGenerateComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerListener__ios.html#ad8b78c0c81565b6ad4b4b3cff084f21c) | A video was generated.     |



## TXVideoJoinerListener

### Video generation and splicing callback APIs

| API | Description |
| :----------------- | ------------------ |
| [onJoinProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerListener__ios.html#a36b82d985b2b1b4061d85011775ab990) | The video generation progress. |
| [onJoinComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerListener__ios.html#a697a4af42d55870db7e6e44f496b0c05) | A video was generated.     |



## TXVideoEditerTypeDef

### Definitions of editing key types

| API | Description |
| :----------------- | -------------- |
| [TXVideoInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#interfaceTXVideoInfo) | The video information.       |
| [TXPreviewParam](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#interfaceTXPreviewParam) | The preview parameters. |
| [TXGenerateResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#interfaceTXGenerateResult) | The editing result. |
| [TXJoinerResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#interfaceTXJoinerResult) | The video generation result. |
| [TXSubtitle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#interfaceTXSubtitle) | The subtitle information.           |
| [TXPaster](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#interfaceTXPaster) | The static sticker information.       |
| [TXAnimatedPaster](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#interfaceTXAnimatedPaster) | The animated sticker information.       |
| [TXSpeed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#interfaceTXSpeed) | The speed changing information.           |
| [TXRepeat](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#interfaceTXRepeat) | The looped segment.       |



### Enumerated types

| API | Description |
| :----------------- | ---------------------- |
| [TXPreviewRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#gae22e497eeef02bd2932af70216cfe734) | Preview fill modes.         |
| [TXSpeedLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#ga1ba0fcb4536220e2f5bafdd02204f924) | Speed change options.         |
| [TXEffectType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#gabb3a6a2a2d5ffadaf15516689f79023a) | Effect types.           |
| [TXTransitionType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#gad971f27e135976a5e02cbcf4683a881c) | Transition effects.       |
| [TXGenerateResultCode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#gae52fdbff9ec4fc124e28000780dab967) | Error codes for video generation. |
| [TXJoinerResultCode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#ga773a8be62fe93b8e06824136e06778fe) | Error codes for video splicing. |
| [TXVideoCompressed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVideoEditerTypeDef__ios.html#a8ea073944cdda7933d033d1aa74d77d7) | Compression ratios.         |


[](id:error)
## Error Codes

### Video generation

| Message                                         | Code   | Description                                                         |
| :--------------------- | ---- | --------- |
| GENERATE_RESULT_OK                          | 0    | The video was generated successfully.                   |
| GENERATE_RESULT_FAILED                      | -1   | Failed to generate the video.                   |
| GENERATE_RESULT_CANCEL              | -2   | The video was canceled.           |
| GENERATE_RESULT_LICENCE_VERIFICATION_FAILED | -5   | Failed to generate the video due to a license verification error. |



### Video splicing

| Message                                         | Code   | Description                                                         |
| -------------------- | ---- | ---------------- |
| JOINER_RESULT_OK                  | 0    | The splicing was successful.         |
| JOINER_RESULT_FAILED              | -1   | The splicing failed.         |
| JOINER_RESULT_LICENCE_VERIFICATION_FAILED | -5   | License verification failed. |
