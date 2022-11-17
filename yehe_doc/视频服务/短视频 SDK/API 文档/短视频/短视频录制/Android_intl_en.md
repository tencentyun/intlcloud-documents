## TXUGCRecord


### Basic shooting APIs
| API | Description |
|-----|-----|
| [getInstance](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a1069b1a0b6fe60220c8c33234e92a21f) | Gets a shooting instance. |
| [setVideoRecordListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#acd229e0c77d3eea61dc0762557417478) | Sets the shooting callback. |
| [release](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a23b477d0e2d399f75d585d154c346591) | Releases resources.                              |
| [setVideoProcessListener](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a2a378860dee249f986c086b8dea9ffed) | Sets the custom image processing callback (not supported in UGSV Lite). |



### Shooting effect APIs

| API | Description |
|-----|-----|
| [setWatermark](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a51fe216c94456dcd7781830c3e4e26fd) | Sets a global watermark (not supported in UGSV Lite). |
| [getBeautyManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#ab6fd77465f53dab034c7704288b0d8bf) | Gets the beauty filter management object. |



### Camera and mic APIs

| API                                                          | Description                                                   |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| [startCameraSimplePreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#af7df0c081288d4fa899213cbe42ab09d) | Starts the camera preview (simplified parameters).                                 |
| [startCameraCustomPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a55f15e0faaee96f742f35201b920c5b4) | Starts the camera preview (custom parameters).                               |
| [setVideoResolution](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#abd1f86f7fe776c2734c9f4de45d1931a) | Sets the shooting resolution.                                           |
| [setVideoBitrate](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a6422a1f0e41e910f35aad752c9b3d023) | Sets the video bitrate for shooting.                                           |
| [stopCameraPreview](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a9b6bf385590ce4bb1a5b0de8f203f6ed) | Stops the camera preview.                                           |
| [switchCamera](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a5afaa0dd12faeb1232c986727b4dac1d) | Switches between the front and rear cameras.                                           |
| [setMicVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a64c284b39bc21caceb6dca801ad9d395) | Sets the mic volume.                                     |
| [toggleTorch](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#af311fa19051d64a5ad64fca96dbc2995) | Turns on/off the flashlight.                                  |
| [getMaxZoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#afa83806e4c432618f3b3eacc54693200) | Gets the maximum zoom factor. You can also use this API to check whether zooming is supported.  |
| [setZoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a4824a12ec5d48a73c1dd5330f0698942) | Sets the zoom factor.                                                 |
| [setFocusPosition](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a589fdf6466566526d49e8877599e12a2) | Sets the focus position manually.                                             |
| [setVideoRenderMode](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#afbe37accb0355ec912b74ed7a003ca09) | Sets the video rendering mode.                                         |



### Shooting APIs

| API                                                                                                              | Description                                                                                                                                                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#abd7692290a3855e606f4c2303ff2a19e) | Starts shooting. The SDK will automatically generate the video path and thumbnail, which are returned by [ITXVideoRecordListener](#itxvideorecordlistener). |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#ac10931870767702b8103da24a4336da3) | Starts shooting.                                                 |
| [startRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a91a872a1b48867bea52c12288ee860b1) | Starts shooting.                                                 |
| [stopRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a13313c5410c2a10a704b991f28141e6e) | Stops shooting.                                                 |
| [pauseRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#aab84e356a72a3df115c82efea02264de) | Pauses shooting.                                                 |
| [resumeRecord](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a6c51e097fc18358c065a602204239b48) | Resumes shooting.                                                 |
| [setAspectRatio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#ae5875c95109dcb60e21fde5efa86d157) | Sets the aspect ratio.                                                   |
| [setRecordSpeed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#ad0f3ba58555a1e212e2abd185d5e3a41) | Sets the shooting speed (not supported in UGSV Lite).                                    |
| [setMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#ae1cc2014b473efd1fc6002d1869cd3ab) | Sets whether to mute audio.                                                     |
| [setHomeOrientation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#ab6cf83f6fb86c30369ff3a49f65c3183) | Sets the orientation (in relation to the Home button).                                             |
| [setRenderRotation](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#aa36b38c81fc1a326fa4e7bed26e4efc6) | Sets the rotation for rendering.                                                |



### Background music APIs

| API                                                          | Description                                    |
| ------------------------------------------------------------ | ----------------------------------------- |
| [setReverb](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#aea6ef8fdb2142efc693064aa42f02586) | Sets the reverb effect (not supported in UGSV Lite).                 |
| [setVoiceChangerType](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a9ae874d5c32001ba2879691b012a35ac) | Sets the voice changing effect (not supported in UGSV Lite).                 |
| [setBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#adbd9b380aac0204e378b28d6bc461f01) | Sets the background music (not supported in UGSV Lite).         |
| [setBGMNofify](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a7232f0ee5d704217a637c794ea561b21) | Sets the music playback callback (not supported in UGSV Lite). |
| [playBGMFromTime](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a41cdb72a1b5952daa77cafc008c12013) | Plays the background music (not supported in UGSV Lite).             |
| [stopBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#adb0738baa0caf8971c629db775662e8e) | Stops the background music (not supported in UGSV Lite).         |
| [pauseBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#aa108fd51c5988a963f165933e1b7d8ee) | Pauses the background music (not supported in UGSV Lite).         |
| [resumeBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#af5a020dca59ebadffb99891ff5e1d642) | Resumes the background music (not supported in UGSV Lite).         |
| [seekBGM](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#abd479e0f220b6fb59d6c2f8a930148e6) | Sets the start and end time for the background music (not supported in UGSV Lite).    |
| [setBGMVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#aef3bca7adc0c23eff963471400ee5879) | Sets the volume of the background music (not supported in UGSV Lite).   |
| [getMusicDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a0bd597c5880c79cb7fa6631da933cc1c) | Gets the duration of the music file (not supported in UGSV Lite).         |



### Screenshot APIs

| API                                                          | Description                 |
| ------------------------------------------------------------ | -------------------- |
| [snapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a65c196156de46b640b80f8266bd3369a) | Sets the preprocessing callback. |



### Disused APIs

| API                                                          | Description                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------- |
| [setMotionTmpl](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#af85168f51d1951878e392eb029ff16cc) | Sets the animated effect (supported in UGSV Enterprise and Enterprise Pro). |
| [setMotionMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a95d1f517930285127b316f648c508efc) | Sets whether to mute an animated effect (supported in UGSV Enterprise and Enterprise Pro).           |
| [setGreenScreenFile](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a5e3398c309da55c1bba1b58028a4da16) | Sets the green screen (supported in UGSV Enterprise Pro).                        |
| [setFaceVLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a0d5e0b622666e0b302a6a51db6894bdd) | Sets the V shape effect (supported in UGSV Enterprise Pro).                             |
| [setFaceShortLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a028d164b127ad73d7b3dd4add0321c4b) | Sets the face length (supported in UGSV Enterprise Pro and Enterprise Pro EX).            |
| [setChinLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#afd1255e5cc581ee4228fc26313a24933) | Sets the chin length (supported in UGSV Enterprise Pro and Enterprise Pro EX).        |
| [setNoseSlimLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#aced93b26f34cefdc8097df9583abb8eb) | Sets the nose size (supported in UGSV Enterprise Pro and Enterprise Pro EX).        |
| [setEyeScaleLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#aae535870773f6e21317b393a5b8eff7c) | Sets the big eyes effect (supported in UGSV Enterprise Pro and Enterprise Pro EX).        |
| [setFaceScaleLevel](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a2e93f2b9f5fa784e9385599491e01c39) | Sets the slim face effect (supported in UGSV Enterprise Pro).                        |
| [setBeautyStyle](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a12bb7ad3513d079272a906d805956895) | Sets the beauty style.                                            |
| [setBeautyDepth](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#af16fc3112bae6dc212ec0cb2cbb0b4b1) | Sets the **beautification** and **brightening** strength.                         |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a2005812aae2e7ced819230d2c3fb297e) | Sets the color filter.                                    |
| [setFilter](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a506d6d253f4505a9ae4c613f2dde28c0) | Sets multiple filters.                                        |
| [setSpecialRatio](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a1f6b0c14db22ca60390b271ca4295cf5) | Sets the filter strength.                                        |

## TXUGCPartsManager

### Segment-based shooting APIs

| API                                                          | Description                     |
| ------------------------------------------------------------ | -------------------------- |
| [TXUGCPartsManager](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a44ea49449da296b0e7440e1d3ba95a74) | The video segment manager.             |
| [setPartsManagerObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#af68a981d78fb6b33a04b2f87775127cc) | Sets the callback for processing video segments.       |
| [removePartsManagerObserver](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a66ed8147742d77af95294a7016b974bf) | Sets the callback for deleting video segments.       |
| [addClipInfo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#ace3493c1e4b80f5eeecd78524242f1d3) | Adds a video segment to the end of the list.     |
| [insertPart](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#abfdfcf7157a69611a6c1dc41e876103b) | Inserts a video segment.               |
| [getDuration](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a08c13081c0665a4336a0f022c955fb69) | Gets the total duration of all the video segments.       |
| [getPartsPathList](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a0e065b1b0d990a75b572725855dd6e1e) | Gets the paths of all the video segments shot. |
| [deleteLastPart](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a553f582941c1c26527f785414b11f055) | Deletes the last video segment.           |
| [deletePart](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a914255b7b451e96a8c6d963d99113cce) | Deletes a specific video segment.               |
| [deleteAllParts](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#acda3a6b6d096a49fb105905bf7f4d33c) | Deletes all the video segments.               |



## VideoCustomProcessListener

### Custom video processing callback APIs

| API                                                                                                            | Description                                                                                                                                                                                     |
| ------------------------------------------------------------ | ---------------- |
| [onTextureCustomProcess](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a619017ddecf52cb94b4182331f475cb3) | The texture processing callback.  |
| [onDetectFacePoints](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#a292bf542a191747e94adaf610aca7ad6) | The facial keypoints.   |
| [onTextureDestroyed](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXUGCRecord__android.html#ac60f1dbbb1af39c666247c6438595de0) | The texture releasing callback. |



## ITXVideoRecordListener

### Preview callback APIs

| API                                                                                                            | Description                                                                                                                                                                                     |
| ------------------------------------------------------------ | ------------------ |
| [onRecordEvent](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXRecordCommon__android.html#a9e41a4daee4ee714b1348fac74131840) | A shooting event. |
| [onRecordProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXRecordCommon__android.html#ab3a5908127ab8c955ec6773a823cd921) | The shooting progress callback.     |
| [onRecordComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXRecordCommon__android.html#aecedd2ceb34c986eee915a31481ccc7e) | The shooting ended.     |



## ITXSnapshotListener

### Screenshot callback APIs

| API                                                                                                            | Description                                                                                                                                                                                     |
| ------------------------------------------------------------ | ------------ |
| [onSnapshot](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXRecordCommon__android.html#afbbd41ebf0f82d5b996608ba5fa72cb3) | The screenshot callback. |



## ITXBGMNotify

### Background music callback APIs

| API                                                          | Description                  |
| ------------------------------------------------------------ | ---------------------- |
| [onBGMStart](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXRecordCommon__android.html#a6c2f1aeb77a3020b4767738b7ef0064d) | The background music started. |
| [onBGMProgress](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXRecordCommon__android.html#a30ab555520fa5a478f633394b9cd4d14) | The music playback progress. |
| [onBGMComplete](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXRecordCommon__android.html#a444c6749e7cb77466940ec1de1c88546) | The background music ended. |



## TXRecordCommon

### Definitions of key types
| API | Description |
|-----|-----|
| [TXRecordResult ](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXRecordCommon__android.html#classcom_1_1tencent_1_1ugc_1_1TXRecordCommon_1_1TXRecordResult) | The shooting result.       |
| [TXUGCSimpleConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXRecordCommon__android.html#classcom_1_1tencent_1_1ugc_1_1TXRecordCommon_1_1TXUGCSimpleConfig) | Preset shooting parameters.   |
| [TXUGCCustomConfig](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXRecordCommon__android.html#classcom_1_1tencent_1_1ugc_1_1TXRecordCommon_1_1TXUGCCustomConfig) | Custom shooting parameters. |



## Error Codes

### Shooting result

| Message                                   | Code   | Description                                                         |
| -------------------------------------- | ---- | ------------------------------------------------------------ |
| RECORD_RESULT_OK                       | 0    | The shooting was **successful** or was **paused (stopped)**.             |
| RECORD_RESULT_OK_LESS_THAN_MINDURATION | 1    | The shooting was successful. The duration is shorter than the minimum duration allowed.                                 |
| RECORD_RESULT_OK_REACHED_MAXDURATION   | 2    | The shooting was successful. The duration is longer than the maximum duration allowed.                                 |
| RECORD_RESULT_FAILED                   | -1   | The shooting failed.                                                 |
| RECORD_RESULT_SUSPEND_FOR_NO_TASK      | -2   | An API was called to pause (stop) shooting, but there wasn’t a shooting task.                           |
| RECORD_RESULT_FILE_ERR                 | -3   | The file does not exist or its duration is 0. This is usually because the interval between when shooting is started, and when it is paused (stopped) is too short. This error does not need to be handled. |
| RECORD_RESULT_COMPOSE_SET_SRC_PATH_ERR | -4   | The source video path is invalid. Call `mTXUGCPartsManager.getPartsPathList()` to check whether the file is empty or its duration is 0. |
| RECORD_RESULT_COMPOSE_SET_DST_PATH_ERR | -5   | The target video path is invalid. Check whether the path is empty.             |
| RECORD_RESULT_COMPOSE_START_ERR        | -6   | Failed to generate the video because there is an ongoing task.                         |
| RECORD_RESULT_COMPOSE_CANCEL           | -7   | The video was canceled.                                                 |
| RECORD_RESULT_COMPOSE_VERIFY_FAIL      | -8   | Verification for video generation failed because **the file does not exist**, **the file duration is 0**, or **the video parameters are inconsistent**. |
| RECORD_RESULT_COMPOSE_INTERNAL_ERR     | -9   | The video failed to be generated due to an internal error.                                       |


[](id:error)
### Starting shooting

| Message                                         | Code   | Description                                                         |
| -------------------------------------------- | ---- | ------------------------------------------------------------ |
| START_RECORD_OK                              | 0    | Shooting started.                                                     |
| START_RECORD_ERR_IS_IN_RECORDING             | -1   | There was an ongoing task when a request was made to start shooting. |
| START_RECORD_ERR_VIDEO_PATH_IS_EMPTY         | -2   | The file path is empty when a request was made to start shooting.                                   |
| START_RECORD_ERR_API_IS_LOWER_THAN_18        | -3   | The version is earlier than v18.                                                  |
| START_RECORD_ERR_NOT_INIT                    | -4   | Initialization was not finished yet when a request was made to start shooting.                                     |
| START_RECORD_ERR_LICENCE_VERIFICATION_FAILED | -5   | License verification failed.                                             |



