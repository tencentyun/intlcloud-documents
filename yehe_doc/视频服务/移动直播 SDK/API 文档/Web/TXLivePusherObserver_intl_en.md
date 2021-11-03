Callbacks for publishing, including publisher status, statistics, warnings, and errors
  
### onError

Callback for error. This callback is triggered when the publisher encounters an error.

```typescript
onError(code: number, msg: string, extraInfo: Object): void;
```

**Parameters**

- `code`: error code. For details, please see [Error codes for publishing](#errocode).
- `msg`: error message
- `extraInfo`: extra information. This parameter is not used currently.

---

### onWarning

Callback for warning.

```typescript
onWarning(code: number, msg: string, extraInfo: Object): void;
```

**Parameters**

- `code`: error code. For details, please see [Error codes for publishing](#errocode).
- `msg`: error message
- `extraInfo`: extra information. This parameter is not used currently.

**Note**

For the error information returned for failure to turn the camera or mic on or record the screen, please see [getUserMedia exceptions](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia#%E5%BC%82%E5%B8%B8) and [getDisplayMedia exceptions](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getDisplayMedia#%E5%BC%82%E5%B8%B8).

---

### onCaptureFirstAudioFrame

Callback for capturing the first audio frame.

```typescript
onCaptureFirstAudioFrame(): void;
```

---

### onCaptureFirstVideoFrame

Callback for capturing the first video frame.

```typescript
onCaptureFirstVideoFrame(): void;
```

---

### onPushStatusUpdate

Callback of the publisher’s connection status.

```typescript
onPushStatusUpdate(status: number, msg: string, extraInfo: Object): void;
```

**Parameters**

- `status`: connection status code. For details, please see [Status codes for publishing](#pushstate).
- `msg`: connection status message
- `extraInfo`: extra information. This parameter is not used currently.

---

### onStatisticsUpdate

Callback of publisher statistics, primarily WebRTC-related statistics, which may vary from browser to browser.

```typescript
onStatisticsUpdate(statistics: Object): void;
```

**Parameters**

`statistics`: publishing statistics. For details, please see [Publishing statistics](#pushdate).

---

[](id:errocode)

### Error codes for publishing

Below are the error codes returned by [onError](#onerror) and [onWarning](#onwarning):

| Enumerated Value                                     | Code  | Description                       |
| ------------------------------------------ | ----- | -------------------------- |
| TXLIVE_ERROR_WEBRTC_FAILED                 | -1    | Failed to call a WebRTC API.        |
| TXLIVE_ERROR_REQUEST_FAILED                | -2    | Error when requesting the server to publish streams.   |
| TXLIVE_WARNING_CAMERA_START_FAILED         | -1001 |  Failed to turn the camera on.  |
| TXLIVE_WARNING_MICROPHONE_START_FAILED     | -1002 | Failed to turn the mic on. |
| TXLIVE_WARNING_SCREEN_CAPTURE_START_FAILED | -1003 | Failed to record the screen.           |
| TXLIVE_WARNING_MEDIA_FILE_START_FAILED     | -1004 | Failed to open a local media file.        |
| TXLIVE_WARNING_CAMERA_INTERRUPTED     | -1005 | Capturing from the camera was interrupted (because the device was disconnected or the user denied the access).       |
| TXLIVE_WARNING_MICROPHONE_INTERRUPTED     | -1006 | Capturing from the mic was interrupted (because the device was disconnected or the user denied the access).       |
| TXLIVE_WARNING_SCREEN_CAPTURE_INTERRUPTED     | -1007 | Screen recording was interrupted (because the user clicked Chrome’s built-in stop-sharing button).      |

---

[](id:pushstate)

### Status codes for publishing

Below are the status codes returned by [onPushStatusUpdate](#onpushstatusppdate):

| Enumerated Value                                     | Code  | Description                       |
| ---------------------------------- | ---- | ---------------- |
| TXLIVE_PUSH_STATUS_DISCONNECTED    | 0    | Disconnected from the server. |
| TXLIVE_PUSH_STATUS_CONNECTING      | 1    | Connecting to the server.   |
| TXLIVE_PUSH_STATUS_CONNECT_SUCCESS | 2    | Connected to the server.   |
| TXLIVE_PUSH_STATUS_RECONNECTING    | 3    | Reconnecting to the server.     |

---

[](id:pushdate)

### Publishing statistics

The [onStatisticsUpdate](#onstatisticsupdate) callback API keeps you up to date on WebRTC-related statistics during publishing. The SDK collects data once every second, and the structure of the object it returns is as follows:

| Parameter     | Description       |
| --------------- | --------------------------------------------------- |
| timestamp       | Timestamp of data collection, i.e., seconds that have elapsed since 00:00:00 UTC, 1 January 1970 till the time of data collection |
| [video](#video) | Video statistics                                    |
| [audio](#audio) | Audio statistics                                    |

#### `video`

| Parameter               | Description                                                        |
| ------------------ | ----------------------------------------------------------- |
| bitrate            | Video bitrate (bit/s)                                       |
| framesPerSecond    | Video frame rate                                                    |
| frameWidth         | Video width, invalid for Firefox                                   |
| frameHeight        | Video height, invalid for Firefox                                   |
| framesEncoded      | Number of encoded frames                                                    |
| framesSent         | Number of published frames, invalid for Firefox                                   |
| packetsSent        | Number of data packets sent                                                    |
| nackCount          | Number of negative acknowledgements (NACK)                          |
| firCount           | Number of Full Intra Requests (FIR)                 |
| pliCount           | Number of Picture Loss Indications (PLI)             |
| frameEncodeAvgTime | Average encoding time (ms), invalid for Safari and Firefox            |
| packetSendDelay    | Average time (ms) data packets are cached locally before being sent, invalid for Firefox |

---

#### `audio`

| Parameter     | Description       |
| ----------- | --------------------- |
| bitrate     | Audio bitrate (bit/s) |
| packetsSent | Number of data packets sent              |
