## TXUGCRecord

### Instantiation API

| API                                                                                                            | Description                                                                                                                                                                                     |
| ------------------------------------------------------------ | ------ |
| [shareInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#abd7245daa19d4334a17b2011263f4958) | Gets an instance. |



### Camera and mic APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------- |
| [startCameraSimple](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a915a26f27fd043c9c3c4e52f9dd05f3f) | Starts the camera preview.                                |
| [startCameraCustom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#ac8ee6db04ab5058797f1b3f68a56160b) | Starts the camera preview.                                |
| [setVideoResolution](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a01023a47d639aca64ae8f0ae16f3ce86) | Changes the shooting resolution. For this API to work, it must be called after `startCamera`. |
| [setVideoRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#af15edcca37fcca57c047bbefa4ca8b9d) | Sets the rendering mode. For this API to work, it must be called after `startCamera`.   |
| [setVideoBitrate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a3f296f3b19e1d30e749b9b27302a50db) | Changes the shooting bitrate.                            |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a9777fe95f7830746c1ba6b10446c37a0) | Sets the camera factor. For this API to work, it must be called after `startCamera`.          |
| [switchCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a8dedd99f945a42c1845313605c50aa61) | Switches between the front and rear cameras. For this API to work, it must be called after `startCamera`.    |
| [toggleTorch](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#aef955cde2331f108b22ef7125171b10d) | Turns on/off the flashlight. For this API to work, it must be called after `startCamera`.        |
| [stopCameraPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a9b6bf385590ce4bb1a5b0de8f203f6ed) | Stops the camera preview.                                |



### Shooting APIs

| API                                                          | Description                                                   |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| [setHomeOrientation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a96ce818b22e3f6db5ecd9b24323af851) | Sets the orientation for shooting.                                           |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#aedfa7b798e073a450c2b2fbb5063955c) | Sets the rotation for rendering.                                         |
| [setAspectRatio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a3268359a2df3834bbdac805f6f1fa3f4) | Sets the aspect ratio.                                                   |
| [setRecordSpeed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#afbafab57dedcc9b91f70bbbce36373a3) | Sets the shooting speed (not supported in UGSV Lite).                                    |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a944c4afc32d8e8ce35a8077b0b55c2e8) | Sets whether to mute audio.                                                     |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#abd7692290a3855e606f4c2303ff2a19e) | Starts shooting. The SDK will automatically generate the video path.               |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#addfa5c2d0d1a99844326d90acd4ba1c9) | Starts shooting.                                                 |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a6e3477949172b4232911799aac6595f1) | Starts shooting.                                                 |
| [pauseRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#aab84e356a72a3df115c82efea02264de) | Pauses shooting.                                                 |
| [pauseRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#ad3526e128777c1b0b93362659d4b26fb) | Pauses shooting.                                                 |
| [resumeRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a6c51e097fc18358c065a602204239b48) | Resumes shooting.                                                 |
| [stopRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a13313c5410c2a10a704b991f28141e6e) | Stops shooting.                                                 |
| [pauseAudioSession](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#ad9af84ae142b3fc65cbf5d8c01bfdc7e) | Pauses the audio session. If you use a different player for preview, make sure you call this API before the preview. |
| [resumeAudioSession](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a9cbec9edda8cf105bba9655567a76c65) | Restarts the audio session of the SDK.                             |



### Shooting effect APIs

| API                                                          | Description                            |
| ------------------------------------------------------------ | -------------------------------- |
| [setWaterMark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a7ee69499e0ca3bd9a7c996505725c384) | Sets a global watermark (not supported in UGSV Lite). |
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a4fb05ae6b5face276ace62558731280a) | Gets the beauty filter management object. |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a789cc2301e3eae49185365a86e885eb1) | Sets the **beautification** and **brightening** strength.                         |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a1202f69d0af6c4fd2b022c61da4dd5b0) | Sets the color filter.             |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a44d7f0da7adb1aa2f62a3afd6d7c4b1c) | Sets two filters (not supported in UGSV Lite). |
| [setSpecialRatio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a6de9ce92116926fe9b53016151d55784) | Sets the filter strength.                                        |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#ae0e4341ef565cc5ba28101574179cd56) | Sets the strength of the big eyes effect.                     |
| [setFaceScaleLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a52ad635b237ccb1eef53a4ed9e650035) | Sets the strength of the slim face effect. |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a1bf6dd0f5a5c6c013323d31f60d494e2) | Sets the V shape effect.                        |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a145d4ed3d5790a449a9884d282420216) | Sets the chin length.               |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#ac11082c88aba749acd7cd2c7a7caa953) | Sets the face length.                         |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#ae94b107a9c476337585906c79b42ee95) | Sets the nose size.                         |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#ab4682edfc605ba06e24fd7b3e758ce5d) | Sets the green screen.                     |
| [selectMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#ad050ac06c70810665b5c22b77dc20048) | Sets the animated effect.                         |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#aa6689d734b9f46cb84a848b7e8f39cbd) | Sets whether to mute an animated effect.                     |



### Background music APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | --------------------------------------------------- |
| [setBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#ae77bca45c2b3a024b605143ad28d756e) | Sets the background music (not supported in UGSV Lite).         |
| [setBGMAsset](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a8c0020b6c543c7beb378c71ac691d912) | Sets the background music (not supported in UGSV Lite).         |
| [setBGMLoop](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#af04ec84d6367837b6a3ec009d42f3dc1) | Sets whether to loop the background music (not supported in UGSV Lite).         |
| [playBGMFromTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#abbd412ef428ecf60dbb94b7b72b4c60e) | Plays the background music (not supported in UGSV Lite).             |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a93a996c467709cb520c5805b672c00cd) | Stops the background music (not supported in UGSV Lite).         |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a096218ccb76707c37e2f586548b9375a) | Pauses the background music (not supported in UGSV Lite).         |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a072b30b60405a8f0df71b1f587c6af06) | Resumes the background music (not supported in UGSV Lite).         |
| [setMicVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#aa53f05d91770488ead49d7f2f95ee803) | Sets the mic volume. |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a3d063f395b28d58c0da4f82765f919da) | Sets the volume of the background music. |
| [setReverbType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#aa89352df472e2fa4c61e0d2a4ba66a34) | Sets the reverb effect. (not supported in UGSV Lite). |
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#ab48b224e092bcec85da330d9ecec4ef6) | Sets the voice changing effect (not supported in UGSV Lite).                 |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__ios.html#a8a2c854e45ee9d741d098a6857edc019) | Takes a screenshot/photo (not supported in UGSV Lite). For this API to work, it must be called after `startCamera`. |



## TXUGCRecordListener

### Shooting callbacks

| API                                                          | Description |
| ------------------------------------------------------------ | ------------------------------ |
| [onRecordProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordListener__ios.html#a5dd24e391f925ae8da1547374f25b695) | The shooting progress.                 |
| [onRecordComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordListener__ios.html#a8766c15db94cea6b7f0ff0d304503dc5) | The shooting ended.                 |
| [onRecordEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordListener__ios.html#aa628297da5b9b7cdb197104097b23834) | A shooting event (not in use yet). |



## TXUGCRecordTypeDef

### Definitions of key types

| API                                             | Description                                                         |
| ------------------------------------------------------------ | ------------ |
| [TXUGCSimpleConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#a1426a86a294de269e792ba146e4afa37) | Shooting parameters. |
| [TXUGCCustomConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#a82925315129ec31125cdb42b75f25974) | Shooting parameter.   |
| [TXUGCRecordResult](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#a3446e8347fa1ec3725df691eb485400b) | The shooting result.     |



### Enumerated types

| API | Description |
| ------------------------------------------------------------ | ---------------- |
| [TXVideoQuality](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#ga0b1160a1d1f238eb36ea51792c18aa3e) | Video quality options. |
| [TXVideoResolution](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#ga5a9bcf750e56b71fe39d60cfcd19e49f) | Resolution.   |
| [TXVideoRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#ga97fb98a2c5613b65bb6886f4c84d5f7f) | Rendering modes. |
| [TXVideoAspectRatio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#gaacb6108218d9b544c66d0e026695e607) | Aspect ratios. |
| [TXVideoRecordSpeed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#ga05c27784a9a0eff768dc7fc003902d4a) | Shooting speeds.     |
| [TXVideoHomeOrientation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#ga0ee2b3bbccfc5dabcd157b98555bec80) | Orientation modes.   |
| [TXVideoEncodeMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#ga78ccacb3bb8b9291cfc91838d4b97897) | Codecs.         |
| [TXVideoReverbType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#gafae9cd4ee113028dd1aa9ad61610baae) | Reverb effects.         |
| [TXVideoVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#gabbc238c80be048e48c0453dd297fd297) | Voice changing effects.         |
| [TXVideoBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#ga135391ff71d01b1b480cdc121c65f715) | Beauty styles.         |
| [TXAudioSampleRate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#gae746c57de845784f17c465dcd08b077f) | Audio sample rates.       |
| [TXUGCRecordResultCode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecordTypeDef__ios.html#ga59aed832d7c79e175e84f5f543c8e45e) | Error codes for the shooting result.   |


[](id:error)
## Error Codes

### Shooting result

| Message                                         | Code   | Description                                                         |
| ---------------------------------------- | ---- | ------------------------------------------------------------ |
| UGC_RECORD_RESULT_OK                     | 0    | The shooting was successful (ended by the user), and a video will be generated.                |
| UGC_RECORD_RESULT_OK_INTERRUPT           | 1    | The shooting was successful (interrupted by an alarm, a call, or switching of the app to the background), and a video will be generated. |
| UGC_RECORD_RESULT_OK_UNREACH_MINDURATION | 2    | The shooting was successful (the duration was shorter than the minimum duration allowed), and a video will be generated.     |
| UGC_RECORD_RESULT_OK_BEYOND_MAXDURATION  | 3    | The shooting was successful (the duration was longer than the maximum duration allowed), and a video will be generated.       |
| UGC_RECORD_RESULT_FAILED                 | 1001 | The shooting failed. No video will be generated.                                   |

