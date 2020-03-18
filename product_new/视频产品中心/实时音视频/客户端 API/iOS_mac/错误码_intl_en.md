

## 1. Error Codes (Severe)

Enumeration name: TXLiteAVError

| Code | Value | Description |
|---|---|---|
|ERR_NULL|0|No error|
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
|ERR_VIDEO_ENCODE_FAIL|-1303|Failed to encode video frames; for example, when a user switches from an iOS device to another device, the hardware encoder may be released by the system; and after the user switches back, this error may be thrown before the hardware encoder is restarted|
|ERR_AUDIO_ENCODE_FAIL|-1304|Failed to encode audio frames; for example, the SDK could not process the custom audio data passed in|
|ERR_UNSUPPORTED_RESOLUTION|-1305|Unsupported video resolution|
|ERR_UNSUPPORTED_SAMPLERATE|-1306|Unsupported audio sample rate|
|ERR_RTMP_PUSH_NET_DISCONNECT|-1307|LVB error. The network was disconnected during push and could not be restored after multiple retries|
|ERR_SCREEN_CAPTURE_START_FAIL|-1308|Failed to start screencapturing. If this error occurs on a mobile device, it may be caused by permission denial by user; if on Windows or macOS, please check whether parameters of the screencapturing API meet the requirements|
|ERR_SCREEN_CAPTURE_UNSURPORT|-1309|Screencapturing failed. Please use Android v5.0 or above if the device is on Android|
|ERR_RTMP_PUSH_INVALID_ADDRESS|-1313|LVB error. The push address is invalid; for example, it is not an RTMP address|
|ERR_RTMP_PUSH_NET_ALLADDRESS_FAIL|-1324|LVB error. Connection to the push server failed (all IPs would have failed if intelligent routing was supported)|
|ERR_RTMP_PUSH_NO_NETWORK|-1325|LVB error. The network is unavailable. Please check whether the Wi-Fi, cellular, or wired network is normal|
|ERR_RTMP_PUSH_SERVER_REFUSE|-1326|LVB error. The server denied the connection request. This may be because the push address was occupied, `TXSecret` failed to pass the verification or expired, or the account was in arrears|
|ERR_PIXEL_FORMAT_UNSUPPORTED|-1327|Unsupported pixel format|
|ERR_BUFFER_TYPE_UNSUPPORTED|-1328|Unsupported buffer type|
|ERR_PLAY_LIVE_STREAM_NET_DISCONNECT|-2301|LVB error. The network was disconnected and could not be connected again after multiple retries. The user can temporarily stop troubleshooting or restart LVB to make more connection retries|
|ERR_GET_RTMP_ACC_URL_FAIL|-2302|LVB error. Failed to get the accelerated pull address|
|ERR_FILE_NOT_FOUND|-2303|The file to be played back does not exist|
|ERR_HEVC_DECODE_FAIL|-2304|Failed to decode with H.265|
|ERR_VOD_DECRYPT_FAIL|-2305|LVB error. Audio/video stream decryption failed|
|ERR_GET_VODFILE_MEDIAINFO_FAIL|-2306|LVB error. Failed to get the VOD file information|
|ERR_PLAY_LIVE_STREAM_SWITCH_FAIL|-2307|LVB error. Stream switch failed (this feature is used to play back videos of different dimensions)|
|ERR_PLAY_LIVE_STREAM_SERVER_REFUSE|-2308|LVB error. The server denied the connection request|
|ERR_RTMP_ACC_FETCH_STREAM_FAIL|-2309|LVB error. RTMPACC low-latency pull failed and could not be recovered after multiple retries|
|ERR_ROOM_ENTER_FAIL|-3301|Failed to enter the room|
|ERR_ROOM_HEARTBEAT_FAIL|-3302|Heartbeat failed. The client periodically sends data packets to the server to tell it that the client is alive. This error is usually caused by packet sending timeout|
|ERR_ROOM_REQUEST_IP_FAIL|-3303|Failed to pull the access server address|
|ERR_ROOM_CONNECT_FAIL|-3304|Failed to connect to the access server|
|ERR_ROOM_REQUEST_AVSEAT_FAIL|-3305|Failed to request the video slot|
|ERR_ROOM_REQUEST_TOKEN_HTTPS_TIMEOUT|-3306|The request for token over HTTPS timed out. Please check whether the network is normal and the network firewall allows HTTPS access to official.opensso.tencent-cloud.com:443|
|ERR_ROOM_REQUEST_IP_TIMEOUT|-3307|The request for IP and signature timed out. Please check whether the network is normal and the network firewall allows UDP access to the following IP and domain name: query.tencent-cloud.com:8000, 162.14.23.140:8000, 162.14.7.49:8000|
|ERR_ROOM_REQUEST_ENTER_ROOM_TIMEOUT|-3308|The room entry request timed out. Please check the network|
|ERR_ROOM_REQUEST_VIDEO_FLAG_TIMEOUT|-3309|The request for video slot timed out|
|ERR_ROOM_REQUEST_VIDEO_DATA_ROOM_TIMEOUT|-3310|The request for video data timed out|
|ERR_ROOM_REQUEST_CHANGE_ABILITY_TIMEOUT|-3311|The request for modifying a video capability item timed out|
|ERR_ROOM_REQUEST_STATUS_REPORT_TIMEOUT|-3312|The request for status report timed out|
|ERR_ROOM_REQUEST_CLOSE_VIDEO_TIMEOUT|-3313|The request for closing a video timed out|
|ERR_ROOM_REQUEST_SET_RECEIVE_TIMEOUT|-3314|The request for receiving a video item timed out|
|ERR_ROOM_REQUEST_TOKEN_INVALID_PARAMETER|-3315|Invalid token request parameter. Please check whether `TRTCParams.userSig` is correctly set|
|ERR_ENTER_ROOM_PARAM_NULL|-3316|Empty room entry parameter. Please check whether valid parameters are passed in to the `enterRoom:appScene:` API when it is called|
|ERR_SDK_APPID_INVALID|-3317|Incorrect room entry parameter `sdkAppId`|
|ERR_ROOM_ID_INVALID|-3318|Incorrect room entry parameter `roomId`|
|ERR_USER_ID_INVALID|-3319|Incorrect room entry parameter `userID`|
|ERR_USER_SIG_INVALID|-3320|Incorrect room entry parameter `userSig`|
|ERR_PUBLISH_CDN_STREAM_REQUEST_TIME_OUT|-3321|The relayed push request timed out|
|ERR_CLOUD_MIX_TRANSCODING_REQUEST_TIME_OUT|-3322|The On-Cloud MixTranscoding request timed out|
|ERR_PUBLISH_CDN_STREAM_RESPON_ERROR|-3323|The returned packet of relayed push is exceptional|
|ERR_CLOUD_MIX_TRANSCODING_RESPON_ERROR|-3324|The returned packet of On-Cloud MixTranscoding is exceptional|
|ERR_ROOM_REQUEST_QUIT_ROOM_TIMEOUT|-3325|The room exit request timed out|
|ERR_ROOM_REQUEST_CONN_ROOM_TIMEOUT|-3326|The co-anchoring request timed out|
|ERR_ROOM_REQUEST_DISCONN_ROOM_TIMEOUT|-3327|The request for exiting co-anchoring timed out|
|ERR_ROOM_REQUEST_CONN_ROOM_INVALID_PARAM|-3328|Invalid parameter|
|ERR_ROOM_REQUEST_AES_TOKEN_RETURN_ERROR|-3329|After `AES TOKEN` was requested, the content returned by the server was empty|
|ERR_CONNECT_OTHER_ROOM_AS_AUDIENCE|-3330|The current role is viewer, and cross-room co-anchoring cannot be requested or stopped|
|ERR_ACCIP_LIST_EMPTY|-3331|The list returned after the access server IP was requested was empty|
|ERR_ROOM_REQUEST_SEND_JSON_CMD_TIMEOUT|-3332|The request for sending a JSON signal timed out|
|ERR_SERVER_INFO_UNPACKING_ERROR|-100000|Error with server decompression. The request data may have been tampered with|
|ERR_SERVER_INFO_TOKEN_ERROR|-100001|Incorrect `TOKEN`|
|ERR_SERVER_INFO_ALLOCATE_ACCESS_FAILED|-100002|An error occurred when allocating an access server|
|ERR_SERVER_INFO_GENERATE_SIGN_FAILED|-100003|An error occurred when generating a signature|
|ERR_SERVER_INFO_TOKEN_TIMEOUT|-100004|HTTPS token timed out|
|ERR_SERVER_INFO_INVALID_COMMAND|-100005|Invalid command word|
|ERR_SERVER_INFO_PRIVILEGE_FLAG_ERROR|-100006|Failed to verify the permission bit|
|ERR_SERVER_INFO_GENERATE_KEN_ERROR|-100007|An error occurred when generating an encryption key during an HTTPS request|
|ERR_SERVER_INFO_GENERATE_TOKEN_ERROR|-100008|An error occurred when generating a token during an HTTPS request|
|ERR_SERVER_INFO_DATABASE|-100009|Failed to query the database (room-related storage information)|
|ERR_SERVER_INFO_BAD_ROOMID|-100010|Incorrect room number|
|ERR_SERVER_INFO_BAD_SCENE_OR_ROLE|-100011|Incorrect scenario or role|
|ERR_SERVER_INFO_ROOMID_EXCHANGE_FAILED|-100012|An error occurred when converting a room number|
|ERR_SERVER_INFO_SERVICE_SUSPENDED|-100013|Unavailable service. Please check the following: <li>Whether the remained validity period in minutes in the package is greater than 0 <li>Whether the Tencent Cloud account is in arrears|
|ERR_SERVER_INFO_STRGROUP_HAS_INVALID_CHARS|-100014|Invalid room number|
|ERR_SERVER_INFO_LACK_SDKAPPID|-100015|Invalid `SDKAppid`|
|ERR_SERVER_INFO_INVALID|-100016|Invalid request. Failed to allocate an access server|
|ERR_SERVER_INFO_ECDH_GET_KEY|-100017|Failed to generate a public key|
|ERR_SERVER_INFO_ECDH_GET_TINYID|-100018| `userSig` verification failed. Please check whether `TRTCParams.userSig` is correctly set|
|ERR_SERVER_ACC_TOKEN_TIMEOUT|-101000|Token expired|
|ERR_SERVER_ACC_SIGN_ERROR|-101001|Incorrect signature|
|ERR_SERVER_ACC_SIGN_TIMEOUT|-101002|Signature timed out|
|ERR_SERVER_ACC_ROOM_NOT_EXIST|-101003|The room does not exist|
|ERR_SERVER_ACC_ROOMID|-101004|Incorrect backend room ID `roomId`|
|ERR_SERVER_ACC_LOCATIONID|-101005|Incorrect backend user location ID `locationId`|
|ERR_SERVER_CENTER_SYSTEM_ERROR|-102000|Backend error|
|ERR_SERVER_CENTER_INVALID_ROOMID|-102001|Invalid room ID|
|ERR_SERVER_CENTER_CREATE_ROOM_FAILED|-102002|Failed to create a room|
|ERR_SERVER_CENTER_SIGN_ERROR|-102003|Incorrect signature|
|ERR_SERVER_CENTER_SIGN_TIMEOUT|-102004|Signature expired|
|ERR_SERVER_CENTER_ROOM_NOT_EXIST|-102005|The room does not exist|
|ERR_SERVER_CENTER_ADD_USER_FAILED|-102006|Failed to add a user to the room|
|ERR_SERVER_CENTER_FIND_USER_FAILED|-102007|Failed to find the user|
|ERR_SERVER_CENTER_SWITCH_TERMINATION_FREQUENTLY|-102008|Device switch too frequent|
|ERR_SERVER_CENTER_LOCATION_NOT_EXIST|-102009|Incorrect `locationid`|
|ERR_SERVER_CENTER_NO_PRIVILEDGE_CREATE_ROOM|-102010|No permission to create room|
|ERR_SERVER_CENTER_NO_PRIVILEDGE_ENTER_ROOM|-102011|No permission to enter room|
|ERR_SERVER_CENTER_INVALID_PARAMETER_SUB_VIDEO|-102012|The video bit is occupied by the secondary channel. Request type parameter of the application for secondary channel is incorrect|
|ERR_SERVER_CENTER_NO_PRIVILEDGE_PUSH_VIDEO|-102013|No permission to enable video|
|ERR_SERVER_CENTER_ROUTE_TABLE_ERROR|-102014|No idle route table|
|ERR_SERVER_CENTER_NO_PRIVILEDGE_PUSH_SUB_VIDEO|-102015|No permission to upstream secondary channel|
|ERR_SERVER_CENTER_ANOTHER_USER_PUSH_SUB_VIDEO|-102016|Other users are upstreaming secondary channel|
|ERR_SERVER_CENTER_NOT_PUSH_SUB_VIDEO|-102017|The current user is not upstreaming secondary channel|
|ERR_SERVER_CENTER_USER_WAS_DELETED|-102018|The user has been deleted|
|ERR_SERVER_CENTER_NO_PRIVILEDGE_REQUEST_VIDEO|-102019|No permission to request video|
|ERR_SERVER_CENTER_INVALID_PARAMETER|-102023|Incorrect room entry parameter `bussInfo`|
|ERR_SERVER_CENTER_I_FRAME_UNKNOW_TYPE|-102024|Unknown `opType` for the I frame request|
|ERR_SERVER_CENTER_I_FRAME_INVALID_PACKET|-102025|Incorrect format of the I frame request packet|
|ERR_SERVER_CENTER_I_FRAME_DEST_USER_NOT_EXIST|-102026|The target user of the I frame request does not exist|
|ERR_SERVER_CENTER_I_FRAME_ROOM_TOO_BIG|-102027|Too many users request the I frame in the room|
|ERR_SERVER_CENTER_I_FRAME_RPS_INVALID_PARAMETER|-102028|Incorrect I frame request parameter|
|ERR_SERVER_CENTER_INVALID_ROOM_ID|-102029|Invalid room number|
|ERR_SERVER_CENTER_ROOM_ID_TOO_LONG|-102030|Room number exceeded the length limit|
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
|ERR_SERVER_CENTER_ROOM_FULL|-102052|The room is full|
|ERR_SERVER_CENTER_DECODE_JSON_FAIL|-102053| Failed to parse the JSON string|
|ERR_SERVER_CENTER_UNKNOWN_SUB_CMD|-102054|Undefined command word|
|ERR_SERVER_CENTER_INVALID_ROLE|-102055|Undefined role|
|ERR_SERVER_CENTER_REACH_PROXY_MAX|-102056|The number of proxy servers has exceeded the upper limit|
|ERR_SERVER_CENTER_RECORDID_STORE|-102057|Failed to save the custom `recordId`|
|ERR_SERVER_CENTER_PB_SERIALIZE|-102058|Error with `Protobuf` serialization|
|ERR_SERVER_SSO_SIG_EXPIRED|-70001|`sig` has expired. Please try to generate a signature again. If the signature expires immediately after generation, please check whether the validity period is too short or 0|
|ERR_SERVER_SSO_SIG_VERIFICATION_FAILED_1|-70003|`sig` verification failed. Please check whether the content of `sig` has been truncated for reasons such as insufficient buffer length|
|ERR_SERVER_SSO_SIG_VERIFICATION_FAILED_2|-70004|`sig` verification failed. Please check whether the content of `sig` has been truncated for reasons such as insufficient buffer length|
|ERR_SERVER_SSO_SIG_VERIFICATION_FAILED_3|-70005|`sig` verification failed. You can use a tool to check whether the generated `sig` is correct|
|ERR_SERVER_SSO_SIG_VERIFICATION_FAILED_4|-70006|`sig` verification failed. You can use a tool to check whether the generated `sig` is correct|
|ERR_SERVER_SSO_SIG_VERIFICATION_FAILED_5|-70007|`sig` verification failed. You can use a tool to check whether the generated `sig` is correct|
|ERR_SERVER_SSO_SIG_VERIFICATION_FAILED_6|-70008|`sig` verification failed. You can use a tool to check whether the generated `sig` is correct|
|ERR_SERVER_SSO_SIG_VERIFICATION_FAILED_7|-70009|`sig` verification with the business public key failed. Please check whether the private key used by the generated `usersig` matches `sdkAppId`|
|ERR_SERVER_SSO_SIG_VERIFICATION_FAILED_8|-70010|`sig` verification failed. You can use a tool to check whether the generated `sig` is correct|
|ERR_SERVER_SSO_SIG_VERIFICATION_ID_NOT_MATCH|-70013|`identifier` in `sig` is different from that in the request. Please check whether the `identifier` set in login is the same as that in `sig`|
|ERR_SERVER_SSO_APPID_NOT_MATCH|-70014|`sdkAppId` in `sig` is different from that in the request. Please check whether the `sdkAppId` set in login is the same as that in `sig`|
|ERR_SERVER_SSO_VERIFICATION_EXPIRED|-70017|Internal verification of third-party credential timed out. Please try again|
|ERR_SERVER_SSO_VERIFICATION_FAILED|-70018|Internal verification of third-party credential timed out. Please try again|
|ERR_SERVER_SSO_APPID_NOT_FOUND|-70020|`sdkAppId` was not found. Please check whether this parameter has been configured in Tencent Cloud|
|ERR_SERVER_SSO_ACCOUNT_IN_BLACKLIST|-70051|Blacklisted account|
|ERR_SERVER_SSO_SIG_INVALID|-70052|Invalid `usersig`. Please generate a new one and try again|
|ERR_SERVER_SSO_LIMITED_BY_SECURITY|-70114|Restricted due to security reasons|
|ERR_SERVER_SSO_INVALID_LOGIN_STATUS|-70221|Invalid login status. Please use `usersig` to authenticate again|
|ERR_SERVER_SSO_APPID_ERROR|-70252|Incorrect `sdkAppId`|
|ERR_SERVER_SSO_TICKET_VERIFICATION_FAILED|-70346|Credential verification failed. Please check whether the parameters are correctly set|
|ERR_SERVER_SSO_TICKET_EXPIRED|-70347|Credential verification failed due to expiration|
|ERR_SERVER_SSO_ACCOUNT_EXCEED_PURCHASES|-70398|The number of accounts has exceeded the upper limit|
|ERR_SERVER_SSO_INTERNAL_ERROR|-70500|Internal server error. Please try again|


## 2. Error Codes (Warning)

Enumeration name: TXLiteAVWarning

| Code | Value | Description |
|---|---|---|
|WARNING_NET_BUSY|1101|Unstable network condition: the upstream bandwidth is too low, and data upload is restricted|
|WARNING_RTMP_SERVER_RECONNECT|1102|LVB error. The network was disconnected, and automatic reconnection was performed (which will be canceled if failing for 3 times in a row)|
|WARNING_HW_ENCODER_START_FAIL|1103|Failed to enable the hardware encoder, and the software encoder was used|
|WARNING_VIDEO_ENCODER_SW_TO_HW|1107|The video encoder was automatically switched from software encoder to hardware encoder. This is generally caused by excessive CPU utilization|
|WARNING_INSUFFICIENT_CAPTURE_FPS|1108|Insufficient frame rate for video capture through camera. This error may occur in Android mobile devices with an in-built beauty filter algorithm|
|WARNING_SW_ENCODER_START_FAIL|1109|Failed to enable the software encoder|
|WARNING_REDUCE_CAPTURE_RESOLUTION|1110|Camera resolution was lowered to meet the balance between current frame rate and performance|
|WARNING_VIDEO_FRAME_DECODE_FAIL|2101|Failed to decode the current video frame|
|WARNING_AUDIO_FRAME_DECODE_FAIL|2102|Failed to decode the current audio frame|
|WARNING_LIVE_STREAM_SERVER_RECONNECT|2103|LVB error. The network was disconnected, and automatic reconnection was performed (which will be canceled if failing for 3 times in a row)|
|WARNING_RECV_DATA_LAG|2104|Unstable transmission of packets from the network. This may be caused by insufficient downstream bandwidth or uneven outbound stream from the anchor|
|WARNING_VIDEO_PLAY_LAG|2105|Video playback lagged (intuitively felt by user)|
|WARNING_HW_DECODER_START_FAIL|2106|Failed to enable the hardware decoder, and the software decoder was used|
|WARNING_VIDEO_DECODER_HW_TO_SW|2108|The hardware decoder failed to decode the first I frame of the current stream, and the SDK automatically switched to the software decoder|
|WARNING_SW_DECODER_START_FAIL|2109|Failed to enable the software decoder|
|WARNING_VIDEO_RENDER_FAIL|2110|Failed to render video|
|WARNING_RTMP_DNS_FAIL|3001|LVB error. DNS resolution failed|
|WARNING_RTMP_SEVER_CONN_FAIL|3002|LVB error. Server connection failed|
|WARNING_RTMP_SHAKE_FAIL|3003|LVB error. Handshake with the RTMP server failed|
|WARNING_RTMP_SERVER_BREAK_CONNECT|3004|LVB error. The server actively closed the connection|
|WARNING_RTMP_READ_WRITE_FAIL|3005|LVB error. RTMP read/write failed, and connection will be closed|
|WARNING_RTMP_WRITE_FAIL|3006|LVB error. RTMP write failed (SDK internal error code, which will not be thrown out)|
|WARNING_RTMP_READ_FAIL|3007|LVB error. RTMP read failed (SDK internal error code, which will not be thrown out)|
|WARNING_RTMP_NO_DATA|3008|LVB error. If no data is sent in 30s, the server will actively close the connection|
|WARNING_PLAY_LIVE_STREAM_INFO_CONNECT_FAIL|3009|LVB error. Failed to call "connect" to connect to the server (SDK internal error code, which will not be thrown out)|
|WARNING_NO_STEAM_SOURCE_FAIL|3010|LVB error. Connection failed since there was no video in the stream address (SDK internal error code, which will not be thrown out)|
|WARNING_ROOM_DISCONNECT|5101|Network connection was closed|
|WARNING_ROOM_RECONNECT|5102|Network disconnected. Automatic reconnection has been enabled|
|WARNING_ROOM_NET_BUSY|5103|Unstable network condition: the upstream bandwidth is too low, and data upload is restricted|
|WARNING_IGNORE_UPSTREAM_FOR_AUDIENCE|6001|The current role is viewer, so upstream audio/video data is ignored|
|WARNING_AUDIO_RECORDING_WRITE_FAIL|7001|Failed to write the recorded audio to a file|

