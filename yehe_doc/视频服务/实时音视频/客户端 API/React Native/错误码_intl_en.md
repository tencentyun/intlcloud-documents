## Error Codes
### Basic error codes

| Code | Value | Description |
|---|---|---|
|ERR_NULL|0|No error.|

### Error codes for room entry

`TRTCCloud.enterRoom()` triggers this type of error codes if room entry fails. You can use the callback APIs `TRTCCloudDelegate.onEnterRoom()` and `TRTCCloudDelegate.OnError()` to capture notifications about room entry errors.

| Code | Value | Description |
|---|---|---|
|ERR_ROOM_ENTER_FAIL|-3301|Failed to enter room.|
|ERR_ENTER_ROOM_PARAM_NULL|-3316|Empty room entry parameters. Please check whether valid parameters are passed in the `TRTCCloud.enterRoom():` API when it is called.|
|ERR_SDK_APPID_INVALID|-3317|Invalid `sdkAppId`. |
|ERR_ROOM_ID_INVALID|-3318|Invalid `roomId`.|
|ERR_USER_ID_INVALID|-3319|Invalid `userID`.|
|ERR_USER_SIG_INVALID|-3320|Invalid `userSig`.|
|ERR_ROOM_REQUEST_ENTER_ROOM_TIMEOUT|-3308|Room entry request timed out. Please check your network.|
|ERR_SERVER_INFO_SERVICE_SUSPENDED|-100013|Service unavailable. Please check whether there are remaining minutes in your packages and whether your Tencent Cloud account has overdue payment.|


### Error code for room exit

`TRTCCloud.exitRoom()` triggers this error code if room exit fails. You can use the callback API `TRTCCloudDelegate.OnError()` to capture notifications about the error.

| Code | Value | Description |
|---|---|---|
|ERR_ROOM_REQUEST_QUIT_ROOM_TIMEOUT|-3325|Room exit request timed out.|


### Error codes for devices (camera, mic, and speaker)

You can use the callback API `TRTCCloudDelegate.OnError()` to capture notifications about device errors.

| Code | Value | Description |
|---|---|---|
|ERR_CAMERA_START_FAIL|-1301|Failed to turn camera on. This error occurs when, for example, there is a problem with the camera configuration program (driver) on Windows or macOS. In this case, turn the camera off and on again, restart the camera, or update the configuration program.|
|ERR_CAMERA_NOT_AUTHORIZED|-1314|Camera not authorized. This error usually occurs on mobile devices and may be because users denied camera permission.|
|ERR_CAMERA_SET_PARAM_FAIL|-1315|Failed to set camera parameters (unsupported values or others).|
|ERR_CAMERA_OCCUPY|-1316|Camera occupied. Try using another camera. |
|ERR_MIC_START_FAIL|-1302|Failed to turn mic on. This error occurs when, for example, there is a problem with the mic configuration program (driver) on Windows or macOS. In this case, turn the mic off and on again, restart the mic, or update the configuration program.|
|ERR_MIC_NOT_AUTHORIZED|-1317|Mic not authorized. This error usually occurs on mobile devices and may be because users denied mic permission.|
|ERR_MIC_SET_PARAM_FAIL|-1318|Failed to set mic parameters.|
|ERR_MIC_OCCUPY|-1319|Mic occupied. This error occurs when, for example, the user is in a call on the mobile device, in which case TRTC will fail to turn the mic on.|
|ERR_MIC_STOP_FAIL|-1320|Failed to turn mic off.|
|ERR_SPEAKER_START_FAIL|-1321|Failed to turn speaker on. This error occurs when, for example, there is a problem with the speaker configuration program (driver) on Windows or macOS. In this case, turn the speaker off and on again, restart the speaker, or update the configuration program.|
|ERR_SPEAKER_SET_PARAM_FAIL|-1322|Failed to set speaker parameters.|
|ERR_SPEAKER_STOP_FAIL|-1323|Failed to turn speaker off.|


### Error codes for screen sharing

You can use the callback API `TRTCCloudDelegate.OnError()` to capture notifications about screen sharing errors.

| Code | Value | Description |
|---|---|---|
|ERR_SCREEN_CAPTURE_START_FAIL|-1308|Failed to start screen recording. If this error occurs on a mobile device, it may be because users denied screen recording permission; if it occurs on Windows or macOS, check whether the parameters of the screen recording API are set as required.|
|ERR_SCREEN_CAPTURE_UNSURPORT|-1309|Screen recording failed. If you use Android, make sure its version is 5.0 or above; if you use iOS, make sure its version is 11.0 or above.|
|ERR_SERVER_CENTER_NO_PRIVILEDGE_PUSH_SUB_VIDEO|-102015|No permission to send substream video images.|
|ERR_SERVER_CENTER_ANOTHER_USER_PUSH_SUB_VIDEO|-102016|Another user is sending substream video images.|
|ERR_SCREEN_CAPTURE_STOPPED|-7001|Screen recording stopped by the system.|


### Error codes for encoding and decoding

You can use the callback API `TRTCCloudDelegate.OnError()` to capture notifications about encoding errors.

| Code | Value | Description |
|---|---|---|
|ERR_VIDEO_ENCODE_FAIL|-1303|Failed to encode video frames. This error occurs when, for example, a user on iOS switches to another app, which may cause the system to release the hardware encoder. When the user switches back, this error may be thrown before the hardware encoder is restarted.|
| PUSH_ERR_UNSUPPORTED_RESOLUTION | -1305 | Unsupported video resolution. |
|ERR_AUDIO_ENCODE_FAIL|-1304|Failed to encode audio frames. This error occurs when, for example, the SDK could not process the custom audio data passed in.|
| PUSH_ERR_UNSUPPORTED_SAMPLERATE | -1306 | Unsupported audio sample rate. |


### Error codes for custom capturing

You can use the callback API `TRTCCloudDelegate.OnError()` to capture notifications about custom capturing errors.

| Code | Value | Description |
|---|---|---|
|ERR_PIXEL_FORMAT_UNSUPPORTED|-1327|Unsupported pixel format.|
|ERR_BUFFER_TYPE_UNSUPPORTED|-1328|Unsupported buffer type.|


### Error codes for CDN binding and stream mixing

You can use the callback APIs `TRTCCloudDelegate.onStartPublishing()` and `TRTCCloudDelegate.onSetMixTranscodingConfig()` to capture notifications about CDN binding and stream mixing errors.

| Code | Value | Description |
|---|---|---|
|ERR_PUBLISH_CDN_STREAM_REQUEST_TIME_OUT|-3321|Relayed push request timed out.|
|ERR_CLOUD_MIX_TRANSCODING_REQUEST_TIME_OUT|-3322|On-Cloud MixTranscoding request timed out.|
|ERR_PUBLISH_CDN_STREAM_SERVER_FAILED|-3323|Abnormal response packets for relayed push.|
|ERR_CLOUD_MIX_TRANSCODING_SERVER_FAILED|-3324|Abnormal response packets for On-Cloud MixTranscoding.|
|ERR_ROOM_REQUEST_START_PUBLISHING_TIMEOUT|-3333|Signaling of starting to push to Tencent Cloud’s live streaming CDN timed out.|
|ERR_ROOM_REQUEST_START_PUBLISHING_ERROR|-3334|Abnormal signaling of starting to push to Tencent Cloud’s live streaming CDN.|
|ERR_ROOM_REQUEST_STOP_PUBLISHING_TIMEOUT|-3335|Signaling of stopping pushing to Tencent Cloud’s live streaming CDN timed out.|
|ERR_ROOM_REQUEST_STOP_PUBLISHING_ERROR|-3336|Abnormal signaling of stopping pushing to Tencent Cloud’s live streaming CDN.|


### Error codes for cross-room co-anchoring

`TRTCCloud.ConnectOtherRoom()` triggers this type of error codes if cross-room co-anchoring fails. You can use the callback API `TRTCCloudDelegate.onConnectOtherRoom()` to capture notifications about co-anchoring errors.

| Code | Value | Description |
|---|---|---|
|ERR_ROOM_REQUEST_CONN_ROOM_TIMEOUT|-3326|Co-anchoring request timed out.|
|ERR_ROOM_REQUEST_DISCONN_ROOM_TIMEOUT|-3327|Request to exit co-anchoring timed out.|
|ERR_ROOM_REQUEST_CONN_ROOM_INVALID_PARAM|-3328|Invalid parameter.|
|ERR_CONNECT_OTHER_ROOM_AS_AUDIENCE|-3330|You are in the role of audience and cannot initiate or end co-anchoring. You need to switch to the anchor role using `switchRole()`.|
|ERR_SERVER_CENTER_CONN_ROOM_NOT_SUPPORT|-102031|Cross-room co-anchoring not supported.|
|ERR_SERVER_CENTER_CONN_ROOM_REACH_MAX_NUM|-102032|Reached the upper limit of co-anchoring calls.|
|ERR_SERVER_CENTER_CONN_ROOM_REACH_MAX_RETRY_TIMES|-102033|Reached the upper limit of retries for cross-room co-anchoring.|
|ERR_SERVER_CENTER_CONN_ROOM_REQ_TIMEOUT|-102034|Cross-room co-anchoring request timed out.|
|ERR_SERVER_CENTER_CONN_ROOM_REQ|-102035|Incorrect format of cross-room co-anchoring request.|
|ERR_SERVER_CENTER_CONN_ROOM_NO_SIG|-102036|No signature for cross-room co-anchoring.|
|ERR_SERVER_CENTER_CONN_ROOM_DECRYPT_SIG|-102037|Failed to decrypt signature for cross-room co-anchoring.|
|ERR_SERVER_CENTER_CONN_ROOM_NO_KEY|-102038|Decryption key for cross-room co-anchoring signature not found.|
|ERR_SERVER_CENTER_CONN_ROOM_PARSE_SIG|-102039|Signature parsing error for cross-room co-anchoring.|
|ERR_SERVER_CENTER_CONN_ROOM_INVALID_SIG_TIME|-102040|Incorrect timestamp of cross-room co-anchoring signature.|
|ERR_SERVER_CENTER_CONN_ROOM_SIG_GROUPID|-102041|Incorrect cross-room co-anchoring signature.|
|ERR_SERVER_CENTER_CONN_ROOM_NOT_CONNED|-102042|No co-anchoring in this room.|
|ERR_SERVER_CENTER_CONN_ROOM_USER_NOT_CONNED|-102043|The user did not initiate co-anchoring.|
|ERR_SERVER_CENTER_CONN_ROOM_FAILED|-102044|Failed to start cross-room co-anchoring.|
|ERR_SERVER_CENTER_CONN_ROOM_CANCEL_FAILED|-102045|Failed to cancel cross-room co-anchoring.|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_ROOM_NOT_EXIST|-102046|Room being connected for co-anchoring does not exist.|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_REACH_MAX_ROOM|-102047|The room being connected reached the upper limit of co-anchoring calls.|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_NOT_EXIST|-102048|The user being called for co-anchoring does not exist.|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_DELETED|-102049|The user being called for co-anchoring was deleted.|
|ERR_SERVER_CENTER_CONN_ROOM_CONNED_USER_FULL|-102050|All resources of the user being called for co-anchoring are occupied.|
|ERR_SERVER_CENTER_CONN_ROOM_INVALID_SEQ|-102051|Sequence number for co-anchoring not in sequential order.|


## Warning Codes

Warning codes do not require your special attention. You can choose whether to prompt the user depending on the situation.

| Code | Value | Description |
|---|---|---|
|WARNING_HW_ENCODER_START_FAIL|1103|Failed to start hardware encoder. The SDK automatically switched to software encoder.|
|WARNING_VIDEO_ENCODER_SW_TO_HW|1107|Insufficient CPU for software encoder. The SDK automatically switched to hardware encoder.|
|WARNING_INSUFFICIENT_CAPTURE_FPS|1108|Insufficient frame rate of video captured by camera. This error may occur on Android devices with built-in beauty filter algorithms.|
|WARNING_SW_ENCODER_START_FAIL|1109|Failed to start software encoder.|
|WARNING_REDUCE_CAPTURE_RESOLUTION|1110|Camera resolution reduced for balance between frame rate and performance.|
|WARNING_CAMERA_DEVICE_EMPTY|1111|No camera detected.|
|WARNING_CAMERA_NOT_AUTHORIZED|1112|User did not grant the application camera access.|
|WARNING_MICROPHONE_DEVICE_EMPTY|1201|No mic detected.|
|WARNING_SPEAKER_DEVICE_EMPTY|1202|No available speaker detected.|
|WARNING_MICROPHONE_NOT_AUTHORIZED|1203|User did not grant the application mic access.|
|WARNING_MICROPHONE_DEVICE_ABNORMAL|1204|No audio capturing device available (for example, because the device is occupied).|
|WARNING_SPEAKER_DEVICE_ABNORMAL|1205|No audio playback device available (for example, because the device is occupied).|
|WARNING_VIDEO_FRAME_DECODE_FAIL|2101|Failed to decode current video frame.|
|WARNING_AUDIO_FRAME_DECODE_FAIL|2102|Failed to decode current audio frame.|
|WARNING_VIDEO_PLAY_LAG|2105|Video playback stuttering.|
|WARNING_HW_DECODER_START_FAIL|2106|Failed to start hardware decoder. Software decoder is used instead.|
|WARNING_VIDEO_DECODER_HW_TO_SW|2108|Hardware decoder failed to decode first I-frame of current stream. The SDK automatically switched to software decoder.|
|WARNING_SW_DECODER_START_FAIL|2109|Failed to start software decoder.|
|WARNING_VIDEO_RENDER_FAIL|2110|Failed to render video.|
|WARNING_START_CAPTURE_IGNORED|4000|Video capturing already started. Request ignored.|
|WARNING_AUDIO_RECORDING_WRITE_FAIL|7001|Failed to write recorded audio to file.|
|WARNING_ROOM_DISCONNECT|5101|Network disconnected.|
|WARNING_IGNORE_UPSTREAM_FOR_AUDIENCE|6001|You are in the role of audience. The request to send audio/video data is ignored.|
|WARNING_NET_BUSY|1101|Bad network connection: data upload blocked due to limited upstream bandwidth.|
|WARNING_RTMP_SERVER_RECONNECT|1102|Push error. The network is disconnected and trying to reconnect (max. attempts: 3).|
|WARNING_LIVE_STREAM_SERVER_RECONNECT|2103|Pull error. The network is disconnected and trying to reconnect (max. attempts: 3).|
|WARNING_RECV_DATA_LAG|2104|Unstable incoming packets. This may be caused by insufficient downstream bandwidth or unstable streams from the anchor.|
|WARNING_RTMP_DNS_FAIL|3001|Live streaming error. DNS resolution failed.|
|WARNING_RTMP_SEVER_CONN_FAIL|3002|Live streaming error. Failed to connect to server.|
|WARNING_RTMP_SHAKE_FAIL|3003|Live streaming error. Handshake with RTMP server failed.|
|WARNING_RTMP_SERVER_BREAK_CONNECT|3004|Live streaming error. Connection dropped by server.|
|WARNING_RTMP_READ_WRITE_FAIL|3005|Live streaming error. RTMP read/write failed. Disconnecting.|
|WARNING_RTMP_WRITE_FAIL|3006|Live streaming error. RTMP write failed. This is an internal error code of the SDK and is not thrown.|
|WARNING_RTMP_READ_FAIL|3007|Live streaming error. RTMP read failed. This is an internal error code of the SDK and is not thrown.|
|WARNING_RTMP_NO_DATA|3008|Live streaming error. Server disconnected as no data is sent for over 30 seconds.|
|WARNING_PLAY_LIVE_STREAM_INFO_CONNECT_FAIL|3009|Live streaming error. Failed to call `connect` to connect to server. This is an internal error code of the SDK and is not thrown.|
|WARNING_NO_STEAM_SOURCE_FAIL|3010|Live streaming error. Connection failed as there was no video in the stream address. This is an internal error code of the SDK and is not thrown.|
|WARNING_ROOM_RECONNECT|5102|Network disconnected. Reconnecting.|
|WARNING_ROOM_NET_BUSY|5103|Bad network connection: data upload blocked due to limited upstream bandwidth.|
    
