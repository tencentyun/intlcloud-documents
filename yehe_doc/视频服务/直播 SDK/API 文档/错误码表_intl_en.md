## onError

The SDK encountered a severe error (for example, invalid license or API call failure) that makes it impossible for stream publishing to continue.

>!Video encoding failure does not affect publishing. The SDK will handle the issue automatically to ensure successful encoding of subsequent frames.


| Error Code | Event | Description |
| -------------------  | -------- |  ------------------------ |
| 0 | V2TXLIVE_OK | No error |
| -1 | V2TXLIVE_ERROR_FAILED       | A common error not yet classified |
| -2 | V2TXLIVE_ERROR_INVALID_PARAMETER  | An invalid parameter was passed to the API. |
| -3 | V2TXLIVE_ERROR_REFUSED  | The API call was rejected.  |
| -4 | V2TXLIVE_ERROR_NOT_SUPPORTED| The API cannot be called.  |
| -5 | V2TXLIVE_ERROR_INVALID_LICENSE | Failed to call the API because the license is invalid. Note: Before calling `startLivePlay`, you need to call `V2TXLivePremier#setLicence` to configure the license (you only need to configure the license once). Otherwise, playback will fail (black screen). You can use a live stream publishing license, UGSV license, or video playback license to activate the playback feature. If you don’t have any of the licenses, you can [buy one](https://www.tencentcloud.com/document/product/1071/38546) or [apply for a trial license for free](https://console.tencentcloud.com/live/license). |
| -6 | V2TXLIVE_ERROR_REQUEST_TIMEOUT | The request timed out.  |
| -7 | V2TXLIVE_ERROR_SERVER_PROCESS_FAILED| The server denied the request.  |
| -8 | V2TXLIVE_ERROR_DISCONNECTED | The SDK was disconnected. |
| -2304 | V2TXLIVE_ERROR_NO_AVAILABLE_HEVC_DECODERS | Could not find an available HEVC decoder. This error code indicates that the current device does not support H.265 decoding. Please switch to H.264 for playback. |



## onWarning

Most warning events trigger protection or recovery logic that involves retries. In most cases, the problems can be fixed by the SDK itself. However, some warning events still need to be handled manually. Warnings serve the purpose of reminding you or your end users that an error occurred.

| Error Code | Event | Description |
| -------------------  | -------- |  ------------------------ |
| 1101 | V2TXLIVE_WARNING_NETWORK_BUSY   |  Bad network connection: Data upload blocked due to limited upstream bandwidth. |
| 2105 | V2TXLIVE_WARNING_VIDEO_BLOCK   |  Stuttering during video playback.  |
| -1301 | V2TXLIVE_WARNING_CAMERA_START_FAILED   |  Failed to turn the camera on.  |
| -1316 | V2TXLIVE_WARNING_CAMERA_OCCUPIED  | The camera is occupied. Try a different camera. |
| -1314 | V2TXLIVE_WARNING_CAMERA_NO_PERMISSION   | No access to the camera. This usually occurs on mobile devices and may be because the user denied the access. |
| -1302 | V2TXLIVE_WARNING_MICROPHONE_START_FAILED        |Failed to turn the mic on. |
| -1319 | V2TXLIVE_WARNING_MICROPHONE_OCCUPIED       | The mic is occupied. This occurs when, for example, the user is having a call on the mobile device. |
| -1317 | V2TXLIVE_WARNING_MICROPHONE_NO_PERMISSION  | No access to the mic. This usually occurs on mobile devices and may be because the user denied the access. |
| -1309 | V2TXLIVE_WARNING_SCREEN_CAPTURE_NOT_SUPPORTED   |  The system does not support screen sharing.  |
| -1308 | V2TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED |  Failed to start screen recording. If this occurs on a mobile device, it may be because the user denied the access.  |
| -7001 | V2TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED                 |  Screen recording was stopped by the system.  |
