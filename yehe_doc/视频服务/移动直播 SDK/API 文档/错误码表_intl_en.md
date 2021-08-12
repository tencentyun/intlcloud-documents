## PushEvent

### Normal events 

There is a notification event after each successful publishing. For example, the return code 1003 indicates that the system will start rendering camera images.

| Error Code | Event | Description |
| -------------------  | -------- |  ------------------------ |
| 1001 | PUSH_EVT_CONNECT_SUCC | Successfully connected to the CVM. |
| 1002 | PUSH_EVT_PUSH_BEGIN | Handshake with the server has been completed, everything is OK, and the SDK is ready to start upstream publishing. |
| 1003 | PUSH_EVT_OPEN_CAMERA_SUCC | Camera enabled successfully. The camera cannot be enabled if it is occupied or there is no access to the camera. |
| 1004 | PUSH_EVT_SCREEN_CAPTURE_SUCC | Screencap started successfully (for Android SDK). |
| 1005 | PUSH_EVT_CHANGE_RESOLUTION | Dynamic publishing resolution change. |
| 1006 | PUSH_EVT_CHANGE_BITRATE | Dynamic publishing bitrate change. |
| 1007 | PUSH_EVT_FIRST_FRAME_AVAILABLE | The first frame is captured. |
| 1008 | PUSH_EVT_START_VIDEO_ENCODER | The encoder is started. |
| 1009 | PUSH_EVT_CAMERA_REMOVED | The camera has been removed (for Windows SDK). |
| 1010 | PUSH_EVT_CAMERA_AVAILABLE | The camera is available again (for Windows SDK). |
| 1011 | PUSH_EVT_CAMERA_CLOSED | The camera is disabled (for Windows SDK). |
| 1012 | PUSH_EVT_SNAPSHOT_RESULT | Return code for screencap snapshot (for Windows SDK). |
| 1018 | PUSH_EVT_ROOM_IN | You are already in the WebRTC room. (Notification for successful room entry) |
| 1019 | PUSH_EVT_ROOM_OUT | You are not in the WebRTC room. (Notification for room entry failure or room exit) |
| 1020 | PUSH_EVT_ROOM_USERLIST | Deliver the WebRTC room member list (excluding the current user). |
| 1021 | PUSH_EVT_ROOM_NEED_REENTER | Switching Wi-Fi to 4G will trigger disconnection and reconnection, which requires you to re-enter the WebRTC room (pull the optimal server address). |

### Critical errors

If the SDK detects critical errors, publishing cannot continue. For example, a user disables the camera permission for the application, and the camera cannot be started as a result.

>!A video encoding failure does not affect publishing directly. The SDK will handle the failure automatically to ensure success of the subsequent video encoding.


| Error Code | Event | Description |
| --- | --- | --- |
| -1301 | PUSH_ERR_OPEN_CAMERA_FAIL | Failed to enable the camera. |
| -1302 | PUSH_ERR_OPEN_MIC_FAIL | Failed to enable the microphone. |
| -1303 | PUSH_ERR_VIDEO_ENCODE_FAIL | Video encoding failed. |
| -1304 | PUSH_ERR_AUDIO_ENCODE_FAIL | Audio encoding failed. |
| -1305 | PUSH_ERR_UNSUPPORTED_RESOLUTION | Unsupported video resolution. |
| -1306 | PUSH_ERR_UNSUPPORTED_SAMPLERATE | Unsupported audio sample rate. |
| -1307 | PUSH_ERR_NET_DISCONNECT | The network is disconnected and fails to be reconnected after three attempts, so the publishing needs to be restarted. |
| -1308 | PUSH_ERR_CAMERA_OCCUPY<br>PUSH_ERR_AUDIO_SYSTEM_NOT_WORK<br>PUSH_ERR_SCREEN_CAPTURE_START_FAILED | The camera is in use and you may try enabling a different camera (Windows). <br>System exception and recording failed (iOS). <br>Failed to start screencap, which is possibly rejected by the user (Android). |
| -1309 | PUSH_ERR_SCREEN_CAPTURE_UNSURPORT | Screencap failed due to unsupported Android OS version. Version 5.0 or above is required (for Android SDK). |

### Warning events 

Most warning events will trigger the protection or recovery logic that involves retries, and in most cases the problems can be recovered by the SDK itself. Certain warning events need to be handled by developers.

- **WARNING_NET_BUSY: **If the host has poor network connections, the user can be notified through UI.

- **WARNING_SERVER_DISCONNECT: **The publishing request is rejected by the backend. This is usually caused by miscalculated txSecret in the publishing address, or because the publishing address is occupied by others (a publishing URL can only have one publishing end at a time).

| Error Code | Event | Description |
| -------------------  | -------- |  -----------------------|
| 1101 | PUSH_WARNING_NET_BUSY | The upstream network is poor. It is recommended to remind users to improve the current network environment. |
| 1102 | PUSH_WARNING_RECONNECT | The network is disconnected and auto reconnection has started (auto reconnection will be stopped after three failed attempts). |
| 1103 | PUSH_WARNING_HW_ACCELERATION_FAIL | Failed to start hardware encoding. The SDK automatically switches to software encoding. |
| 1104 | PUSH_WARNING_VIDEO_ENCODE_FAIL | Video encoding failed. Non-fatal error. The encoder will be restarted internally. |
| 1107 | PUSH_WARNING_VIDEO_ENCODE_SW_SWITCH_HW | Automatically switch to hardware encoding due to machine performance issues (for Android SDK). |
| 3001 | PUSH_WARNING_DNS_FAIL | DNS resolution failed, and the retry process is triggered. |
| 3002 | PUSH_WARNING_SEVER_CONN_FAIL | Failed to connect to the server, and the retry process is triggered. |
| 3003 | PUSH_WARNING_SHAKE_FAIL | Server handshake failed, and the retry process is triggered. |
| 3004 | PUSH_WARNING_SERVER_DISCONNECT | The RTMP server is actively disconnected. Check the validity of the publishing address or the validity period of hotlink protection. |
| 3005 | PUSH_WARNING_READ_WRITE_FAIL | RTMP read/write failed. Disconnecting. |


## PlayEvent

### Key events

| Error Code | Event | Description |
| --- | --- | --- |
| 2001 | PLAY_EVT_CONNECT_SUCC | Connected to the server. |
| 2002 | PLAY_EVT_RTMP_STREAM_BEGIN | Connected to the server and started playback. |
| 2003 | PLAY_EVT_RCV_FIRST_I_FRAME | Render the first video packet (IDR). |
| 2004 | PLAY_EVT_PLAY_BEGIN | Video playback starts. |
| 2005 | PLAY_EVT_PLAY_PROGRESS | Video playback progress (for VOD). |
| 2006 | PLAY_EVT_PLAY_END | Video playback ends. |
| 2007 | PLAY_EVT_PLAY_LOADING | Video playback loading. |
| 2008 | PLAY_EVT_START_VIDEO_DECODER | Decoder starts. |
| 2009 | PLAY_EVT_CHANGE_RESOLUTION | Video resolution changes. |
| 2010 | PLAY_EVT_GET_PLAYINFO_SUCC<br>PLAY_EVT_SNAPSHOT_RESULT | VOD file information obtained successfully (Android, iOS). <br>The error code of screencap snapshot (Windows). |
| 2011 | PLAY_EVT_CHANGE_ROTATION | MP4 video rotation angle (Android, iOS). |
| 2012 | PLAY_EVT_GET_MESSAGE | Used to receive messages inserted into the audio/video stream. |
| 2013 | PLAY_EVT_PREPARED | Video loading is completed (Android, iOS). |
| 2014 | PLAY_EVT_VOD_LOADING_END | Loading ends (Android, iOS). |
| -2301 | PLAY_ERR_NET_DISCONNECT | The network is disconnected and fails to be reconnected after three attempts, so the publishing needs to be restarted. |
| -2302 | PLAY_ERR_GET_RTMP_ACC_URL_FAIL | Failed to get the accelerated playback address. The possible cause is that the accelerated playback address passed in to `liveplayer` does not contain `txTime` and `txSecret` or that the signature calculation is incorrect. If this error occurs, `liveplayer` stops pulling the accelerated stream and pulls the video stream from the CDN instead, resulting in high delay. <br>Note: only RTMP playback addresses support low-delay acceleration. |
| -2303 | PLAY_ERR_FILE_NOT_FOUND | No playback file exists (Android, iOS). |
| -2304 | PLAY_ERR_HEVC_DECODE_FAIL | H.265 decoding failed (Android, iOS). |
| -2305 | PLAY_ERR_HLS_KEY | Failed to get the HLS decoding key (Android, iOS). |
| -2306 | PLAY_ERR_GET_PLAYINFO_FAIL | Failed to get VOD file information (Android, iOS). |

>! 
>- **Determine whether the live streaming is over: **Due to the varying implementation principles of different standards, usually no end events (error code 2006) are returned for many live streams. Instead, when a host stops publishing, the SDK will soon find that data stream pull fails (WARNING_RECONNECT) and attempt to retry until the PLAY_ERR_NET_DISCONNECT event is thrown after three failed attempts. Therefore, determination needs to be made for both the error codes 2006 and -2301, and the determination result is used as the event to determine the end of live streaming.
>- **Do not hide the playback image after receiving PLAY_LOADING**, because the time length between PLAY_LOADING and PLAY_BEGIN is uncertain (it may be 5 seconds or 5 milliseconds). Some customers consider hiding the playback image upon LOADING and displaying the image upon BEGIN, which will cause serious image flashing (especially in live streaming scenarios). It is recommended to place a translucent loading animation on top of the video playback image.

### Warning events

Internal warnings are not irrecoverable errors. When warning events occur, the SDK will initiate appropriate recovery measures. The purpose of warning is mainly to inform developers or end users of the events.

| Error Code | Event | Description |
| -------------------  | -------- |  ------------------------ |
| 2101 | PLAY_WARNING_VIDEO_DECODE_FAIL | Failed to decode the current video frame. |
| 2102 | PLAY_WARNING_AUDIO_DECODE_FAIL | Failed to decode the current audio frame. |
| 2103 | PLAY_WARNING_RECONNECT | Network disconnected and auto reconnection has started (the PLAY_ERR_NET_DISCONNECT event will be thrown after three failed attempts). |
| 2104 | PLAY_WARNING_RECV_DATA_LAG | The video stream is not stable. This may be caused by bad network connection. |
| 2105 | PLAY_WARNING_VIDEO_PLAY_LAG | Lagging occurred during the current video playback. |
| 2106 | PLAY_WARNING_HW_ACCELERATION_FAIL | Failed to start hardware decoding. Software decoding is used instead. |
| 2107 | PLAY_WARNING_VIDEO_DISCONTINUITY | Current video frames are discontinuous. Certain frames may be dropped. The image may be blurry. |
| 2108 | PLAY_WARNING_FIRST_IDR_HW_DECODE_FAIL | Hardware decoding of the first frame of the current stream failed. The SDK switched to software decoding automatically. |
| 3001 | PLAY_WARNING_DNS_FAIL | DNS resolution failed (thrown only when the playback URL starts with "rtmp://"). |
| 3002 | PLAY_WARNING_SEVER_CONN_FAIL | Server connection failed (thrown only when the playback URL starts with "rtmp://"). |
| 3003 | PLAY_WARNING_SHAKE_FAIL | Server handshake failed (thrown only when the playback URL starts with "rtmp://"). |
| 3004 | PLAY_WARNING_SERVER_DISCONNECT | The RTMP server is actively disconnected. |
   
