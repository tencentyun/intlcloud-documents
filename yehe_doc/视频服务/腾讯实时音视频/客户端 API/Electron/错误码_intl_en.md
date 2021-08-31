## Error Codes

### Basic error codes

| Code | Value | Description |
|---|---|---|
|ERR_NULL|0|No error|

### Error codes for room entry
`TRTCCloud.enterRoom()` will trigger this type of error codes if cross-room co-anchoring fails. You can use the callback functions `TRTCCloudDelegate.onEnterRoom()` and `TRTCCloudDelegate.OnError()` to capture related notifications.

| Code | Value | Description |
|---|---|---|
|ERR_ROOM_ENTER_FAIL|-3301|Failed to enter the room|
|ERR_ENTER_ROOM_PARAM_NULL|-3316|Empty room entry parameter. Please check whether valid parameters are passed in to the `enterRoom:appScene:` API when it is called|
|ERR_SDK_APPID_INVALID|-3317|Incorrect room entry parameter `sdkAppId`|
|ERR_ROOM_ID_INVALID|-3318|Incorrect room entry parameter `roomId`|
|ERR_USER_ID_INVALID|-3319|Incorrect room entry parameter `userID`|
|ERR_USER_SIG_INVALID|-3320|Incorrect room entry parameter `userSig`|
|ERR_ROOM_REQUEST_ENTER_ROOM_TIMEOUT|-3308|The room entry request timed out. Please check the network|
|ERR_SERVER_INFO_SERVICE_SUSPENDED|-100013|Unavailable service. Please check whether the remained validity period in minutes in the package is greater than 0 and whether the Tencent Cloud account has overdue payment|


### Error codes for room exit

`TRTCCloud.exitRoom()` will trigger this type of error codes if cross-room co-anchoring fails. You can use the callback function `TRTCCloudDelegate.OnError()` to capture related notifications.

| Code | Value | Description |
|---|---|---|
|ERR_ROOM_REQUEST_QUIT_ROOM_TIMEOUT|-3325|The room exit request timed out|


### Error codes for devices (camera, mic, and speaker)

You can use the callback function `TRTCCloudDelegate.OnError()` to capture related notifications.

| Code | Value | Description |
|---|---|---|
|ERR_CAMERA_START_FAIL|-1301|Failed to enable the camera; for example, the configuration program (driver) of the camera on Windows or macOS was exceptional. In this case, please try to disable and then enable the camera again, restart the device, or update the configuration program|
|ERR_CAMERA_NOT_AUTHORIZED|-1314|The camera is not authorized. This error usually occurs on mobile devices and may be caused by permission denial by user|
|ERR_CAMERA_SET_PARAM_FAIL|-1315|Incorrect camera parameter settings (unsupported value or other causes)|
|ERR_CAMERA_OCCUPY|-1316|The camera is being used. Please try to enable another camera|
|ERR_MIC_START_FAIL|-1302|Failed to enable the mic; for example, the configuration program (driver) of the mic on Windows or macOS was exceptional. In this case, please try to disable and then enable the mic again, restart the device, or update the configuration program|
|ERR_MIC_NOT_AUTHORIZED|-1317|The mic is not authorized. This error usually occurs on mobile devices and may be caused by permission denial by user|
|ERR_MIC_SET_PARAM_FAIL|-1318|Failed to set mic parameters|
|ERR_MIC_OCCUPY|-1319|The mic is being used. For example, if the mobile device is on a call, the mic will fail to be enabled|
|ERR_MIC_STOP_FAIL|-1320|Failed to disable the mic|
|ERR_SPEAKER_START_FAIL|-1321|Failed to enable the speaker; for example, the configuration program (driver) of the speaker on Windows or macOS was exceptional. In this case, please try to disable and then enable the speaker again, restart the device, or update the configuration program|
|ERR_SPEAKER_SET_PARAM_FAIL|-1322|Failed to set the speaker parameters|
|ERR_SPEAKER_STOP_FAIL|-1323|Failed to disable the speaker|


### Error codes for screen sharing

You can use the callback function `TRTCCloudDelegate.OnError()` to capture related notifications.

| Code | Value | Description |
|---|---|---|
|ERR_SCREEN_CAPTURE_START_FAIL|-1308|Failed to start screencapturing. If this error occurs on a mobile device, it may be caused by permission denial by user; if on Windows or macOS, please check whether parameters of the screencapturing API meet the requirements|
|ERR_SCREEN_CAPTURE_UNSURPORT|-1309|Screencapturing failed. Please use Android v5.0 or above if the device is on Android or use iOS v11.0 or above if the device is on iOS|
|ERR_SERVER_CENTER_NO_PRIVILEDGE_PUSH_SUB_VIDEO|-102015|No permission to upstream secondary channel|
|ERR_SERVER_CENTER_ANOTHER_USER_PUSH_SUB_VIDEO|-102016|Other users are upstreaming secondary channel|
|ERR_SCREEN_CAPTURE_STOPPED|-7001|Screecapturing was stopped by the system|


### Error code for encoding and decoding

You can use the callback function `TRTCCloudDelegate.OnError()` to capture related notifications.

| Code | Value | Description |
|---|---|---|
|ERR_VIDEO_ENCODE_FAIL|-1303|Failed to encode video frames; for example, when a user switches from an iOS device to another device, the hardware encoder may be released by the system; and after the user switches back, this error may be thrown before the hardware encoder is restarted|
|ERR_UNSUPPORTED_RESOLUTION|-1305|Unsupported video resolution|
|ERR_AUDIO_ENCODE_FAIL|-1304|Failed to encode audio frames; for example, the SDK could not process the custom audio data passed in|
|ERR_UNSUPPORTED_SAMPLERATE|-1306|Unsupported audio sample rate|


### Error codes for custom capture

You can use the callback function `TRTCCloudDelegate.OnError()` to capture related notifications.

| Code | Value | Description |
|---|---|---|
|ERR_PIXEL_FORMAT_UNSUPPORTED|-1327|Unsupported pixel format|
|ERR_BUFFER_TYPE_UNSUPPORTED|-1328|Unsupported buffer type|


### Error codes for CDN binding and mixtranscoding

You can use the callback functions `TRTCCloudDelegate.onStartPublishing()` and `TRTCCloudDelegate.onSetMixTranscodingConfig()` to capture related notifications.

| Code | Value | Description |
|---|---|---|
|ERR_PUBLISH_CDN_STREAM_REQUEST_TIME_OUT|-3321|The relayed push request timed out|
|ERR_CLOUD_MIX_TRANSCODING_REQUEST_TIME_OUT|-3322|The On-Cloud MixTranscoding request timed out|
|ERR_PUBLISH_CDN_STREAM_SERVER_FAILED|-3323|The returned packet of relayed push is exceptional|
|ERR_CLOUD_MIX_TRANSCODING_SERVER_FAILED|-3324|The returned packet of On-Cloud MixTranscoding is exceptional|
|ERR_ROOM_REQUEST_START_PUBLISHING_TIMEOUT|-3333|Signaling timed out when starting pushing to Tencent Cloud LVB CDN |
|ERR_ROOM_REQUEST_START_PUBLISHING_ERROR|-3334|Signaling was exceptional when starting pushing to Tencent Cloud LVB CDN |
|ERR_ROOM_REQUEST_STOP_PUBLISHING_TIMEOUT|-3335|Signaling timed out when stopping pushing to Tencent Cloud LVB CDN |
|ERR_ROOM_REQUEST_STOP_PUBLISHING_ERROR|-3336|Signaling was exceptional when stopping pushing to Tencent Cloud LVB CDN |


### Error codes for cross-room co-anchoring

`TRTCCloud.ConnectOtherRoom()` will trigger this type of error codes if cross-room co-anchoring fails. You can use the callback function `TRTCCloudDelegate.onConnectOtherRoom()` to capture related notifications.

| Code | Value | Description |
|---|---|---|
|ERR_ROOM_REQUEST_CONN_ROOM_TIMEOUT|-3326|The co-anchoring request timed out|
|ERR_ROOM_REQUEST_DISCONN_ROOM_TIMEOUT|-3327|The request for exiting co-anchoring timed out|
|ERR_ROOM_REQUEST_CONN_ROOM_INVALID_PARAM|-3328|Invalid parameter|
|ERR_CONNECT_OTHER_ROOM_AS_AUDIENCE|-3330|The current role is viewer, and cross-room co-anchoring cannot be requested or stopped. `switchRole()` needs to be used to switch the role to anchor first |
|ERR_SERVER_CENTER_CONN_ROOM_NOT_SUPPORT|-102031|Cross-room co-anchoring unsupported|
|ERR_SERVER_CENTER_CONN_ROOM_REACH_MAX_NUM|-102032|The number of co-anchoring calls has reached the upper limit|
|ERR_SERVER_CENTER_CONN_ROOM_REACH_MAX_RETRY_TIMES|-102033|The number of retries for cross-room co-anchoring has reached the upper limit|
|ERR_SERVER_CENTER_CONN_ROOM_REQ_TIMEOUT|-102034|The request for cross-room co-anchoring timed out|
|ERR_SERVER_CENTER_CONN_ROOM_REQ|-102035|Incorrect format of the cross-room co-anchoring request|
|ERR_SERVER_CENTER_CONN_ROOM_NO_SIG|-102036|No signature for cross-room co-anchoring|
|ERR_SERVER_CENTER_CONN_ROOM_DECRYPT_SIG|-102037|Failed to decrypt the signature for cross-room co-anchoring|
|ERR_SERVER_CENTER_CONN_ROOM_NO_KEY|-102038|The key for decrypting the cross-room co-anchoring signature was not found|
|ERR_SERVER_CENTER_CONN_ROOM_PARSE_SIG|-102039|An error occurred when parsing a signature for cross-room co-anchoring|
|ERR_SERVER_CENTER_CONN_ROOM_INVALID_SIG_TIME|-102040|Incorrect timestamp of the cross-room co-anchoring signature|
|ERR_SERVER_CENTER_CONN_ROOM_SIG_GROUPID|-102041|Incorrect cross-room co-anchoring signature|
|ERR_SERVER_CENTER_CONN_ROOM_NOT_CONNED|-102042|No co-anchoring in this room|
|ERR_SERVER_CENTER_CONN_ROOM_USER_NOT_CONNED|-102043|The user did not initiate co-anchoring|
|ERR_SERVER_CENTER_CONN_ROOM_FAILED|-102044|Cross-room co-anchoring failed|
|ERR_SERVER_CENTER_CONN_ROOM_CANCEL_FAILED|-102045|Failed to cancel cross-room co-anchoring|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_ROOM_NOT_EXIST|-102046|The room to be called in co-anchoring does not exist|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_REACH_MAX_ROOM|-102047|The number of rooms that can join co-anchoring has reached the upper limit|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_NOT_EXIST|-102048|The user to be called in co-anchoring does not exist|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_DELETED|-102049|The user to be called in co-anchoring was deleted|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_FULL|-102050|The number of users that can join co-anchoring has reached the upper limit|
|ERR_SERVER_CENTER_CONN_ROOM_INVALID_SEQ|-102051|Disordered co-anchoring request numbers|


## Warning Codes

Warning codes do not require your special attention, and you can choose whether to prompt the current user accordingly.

| Code | Value | Description |
|---|---|---|
|WARNING_HW_ENCODER_START_FAIL|1103|An error occurred while enabling the hardware encoder, and the software encoder was automatically switch to |
|WARNING_VIDEO_ENCODER_SW_TO_HW|1107|The current CPU utilization is too high to meet software encoding needs, and the hardware encoder was automatically switch to |
|WARNING_INSUFFICIENT_CAPTURE_FPS|1108|Insufficient frame rate for video capture through camera. This error may occur in Android mobile devices with an in-built beauty filter algorithm|
|WARNING_SW_ENCODER_START_FAIL|1109|Failed to enable the software encoder|
|WARNING_REDUCE_CAPTURE_RESOLUTION|1110|Camera resolution was lowered to meet the balance between current frame rate and performance|
|WARNING_VIDEO_FRAME_DECODE_FAIL|2101|Failed to decode the current video frame|
|WARNING_AUDIO_FRAME_DECODE_FAIL|2102|Failed to decode the current audio frame|
|WARNING_VIDEO_PLAY_LAG|2105|Video playback lagged |
|WARNING_HW_DECODER_START_FAIL|2106|Failed to enable the hardware decoder, and the software decoder was used|
|WARNING_VIDEO_DECODER_HW_TO_SW|2108|The hardware decoder failed to decode the first I frame of the current stream, and the SDK automatically switched to the software decoder|
|WARNING_SW_DECODER_START_FAIL|2109|Failed to enable the software decoder|
|WARNING_VIDEO_RENDER_FAIL|2110|Failed to render video|
|WARNING_START_CAPTURE_IGNORED|4000|Video capture has started|
|WARNING_AUDIO_RECORDING_WRITE_FAIL|7001|Failed to write the recorded audio to a file|
|WARNING_ROOM_DISCONNECT|5101|Network connection was closed|
|WARNING_IGNORE_UPSTREAM_FOR_AUDIENCE|6001|The current role is viewer, so upstream audio/video data is ignored|
