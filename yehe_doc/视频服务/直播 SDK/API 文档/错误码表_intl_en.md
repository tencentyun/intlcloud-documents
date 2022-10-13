## onError

The SDK encountered a severe error that makes it impossible for stream publishing to continue, for example, invalid license or API call failure.

>!Video encoding failure does not affect publishing. The SDK will handle the issue automatically to ensure successful encoding of subsequent frames.


| Error Code | Event | Description |
| -------------------  | -------- |  ------------------------ |
| 0 | V2TXLIVE_OK | No error |
| -1 | V2TXLIVE_ERROR_FAILED       | A common error not yet classified |
| -2 | V2TXLIVE_ERROR_INVALID_PARAMETER  | An invalid parameter was passed in during API calling. |
| -3 | V2TXLIVE_ERROR_REFUSED  | The API call was rejected.  |
| -4 | V2TXLIVE_ERROR_NOT_SUPPORTED| The API cannot be called.  |
| -5 | V2TXLIVE_ERROR_INVALID_LICENSE | Failed to call the API due to invalid license.  |
| -6 | V2TXLIVE_ERROR_REQUEST_TIMEOUT | The server request timed out.  |
| -7 | V2TXLIVE_ERROR_SERVER_PROCESS_FAILED| The server denied the request.  |
| -8 | V2TXLIVE_ERROR_DISCONNECTED | The SDK was disconnected. |



## onWarning

Most warning events trigger protection or recovery logic that involves retries, and in most cases the problems can be fixed by the SDK itself, but some warning events still need to be handled manually. Warnings serve the purpose of reminding you or your end users that an error occurred.

| Error Code | Event | Description |
| -------------------  | -------- |  ------------------------ |
| 1101 | V2TXLIVE_WARNING_NETWORK_BUSY   |  Bad network connection: data upload blocked due to limited upstream bandwidth. |
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
