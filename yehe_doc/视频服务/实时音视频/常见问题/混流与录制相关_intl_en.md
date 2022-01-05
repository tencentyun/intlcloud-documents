## 1. Mixtranscoding
[](id:m1)
### How do I know whether the new MCU stream mixing scheme or legacy on-cloud stream mixing scheme is used?
If the following conditions are met and `mcumix = 1` is printed in the client log, the new MCU stream mixing scheme is used:
- The application is created on or after January 9, 2020.
- The version of the TRTC SDK is v6.9 or above.

[](id:m2)
### What should I do if the stream mixing API fail to work?
1. Make sure you have enabled relayed push in the [TRTC console](https://console.cloud.tencent.com/trtc).
2. Listen for `onSetMixTranscodingConfig()` and make modifications based on the error message returned.
3. If a relayed stream ID is specified through an SDK API, the legacy on-cloud stream mixing scheme will fail.
4. If the `onSetMixTranscodingConfig()` callback indicates that stream mixing is successful, but no mixed stream can be pulled via CDN, it may be caused by failure to set a playback domain name. Please check the configuration of your playback domain name.

## 2. On-Cloud Recording

[](id:r1)
### How do I record users’ streams separately?
- Select **Global Auto-Recording** in the console, and each user’s stream in a room will be recorded automatically during publishing. For details, see [Scheme 1: global auto-recording](https://intl.cloud.tencent.com/document/product/647/35426).
- Select **Specified User Recording** in the console and specify the `userDefineRecordId` parameter in `TRTCParams` during room entry. For details, see [Scheme 2: user specified recording (SDK API)](https://intl.cloud.tencent.com/document/product/647/35426).
- If you do not want to use global auto-recording and your platform does not support the APIs of the TRTC SDK, you can also use the [Live Recording](https://intl.cloud.tencent.com/document/product/267/31563) feature of [CSS](https://intl.cloud.tencent.com/products/css) to record the streams of specified users.

[](id:r2)
### How do I record mixed streams?
- If **Global Auto-Recording** is selected in the console, mixed streams will be recorded automatically.
- If **Specified User Recording** is selected in the console, and a RESTful API is used to initiate stream mixing, you can record the mixed stream by specifying the `OutputParams.RecordId` parameter when calling the API. For details, see [OutputParams](https://intl.cloud.tencent.com/document/product/647/36760).
- If **Specified User Recording** is selected in the console, and an SDK API is used to initiate stream mixing, you can record the mixed stream by letting the anchor specify the `userDefineRecordId` parameter in `TRTCParams` during room entry. For details, see [Scheme 2: user specified recording (SDK API)](https://intl.cloud.tencent.com/document/product/647/35426).

[](id:r3)
### When does recording start?
- Separate stream recording: a few seconds (network latency and keyframe waiting time) after publishing starts
- Mixed stream recording: a few seconds (network latency and keyframe waiting time) after stream mixing starts

[](id:r4)
### When does recording end?
- Separate stream recording ends after a stream stops. If a resumption timeout period is specified, the recording ends after the timeout period elapses.
- If the SDK API `setMixTranscodingConfig()` is used to initiate stream mixing, the recording ends after the anchor leaves or after `setMixTranscodingConfig()` is called again with `null` passed in.
- If the RESTful API `StartMCUMixTranscode` is used to initiate stream mixing, the recording ends after all users in the room leave or after `StopMCUMixTranscode` is called to stop stream mixing.

[](id:r5)
### When are recording files and callbacks generated?
- A recording file is saved to the [VOD](https:/intl.cloud.tencent.com/product/vod) platform and recording callback triggered 5 minutes after recording finishes.
- If a resumption timeout period is specified, the time to wait will be 5 minutes plus the timeout period. Before the timeout period elapses, recording will not end even if the stream is interrupted. No recording file or callback will be generated either.
- There is an upper limit (which can be configured in the console) to the duration of recording files in MP4, FLV, or AAC format. Whenever this limit is exceeded, a recording file and callback will be generated, and the recording will continue.

[](id:r6)
### How do I obtain recording files?
- You can search for recording files in the VOD console or via a RESTful API of VOD. For detailed directions, see [Searching for Recording Files](https://intl.cloud.tencent.com/document/product/647/35426).
- You can get the download URLs for recording files in recording callbacks. For details, see [Receiving Recording File](https://intl.cloud.tencent.com/document/product/647/35426).

[](id:r6)
### What should I do if no recording files are generated?
- If a call is not set up successfully or publishing continues for a too short period (preferably longer than 30 seconds), a recording file may not be generated. You can check whether your upstream data is normal in the dashboard.
- If **Specified User Recording** is selected in the console, and `userDefineRecordId` in `TRTCParams` is not specified during room entry, the streams in a room will not be recorded.
- If **Specified User Recording** is selected in the console and a RESTful API is used to initiate stream mixing, but `OutputParams.RecordId` is not specified when the API is called, the mixed stream will not be recorded.
- If **Specified User Recording** is selected in the console and an SDK API is used to initiate stream mixing, but `userDefineRecordId` is not specified when the anchor calls the API, the mixed stream will not be recorded.

[](id:r7)
### What should I do if I don’t receive recording callbacks?
- Check in the console if recording files are generated. If not, refer to the previous question. For how to search for recording files, see [Searching for Recording Files](https://intl.cloud.tencent.com/document/product/647/35426).
- If recording files are generated, check whether you have configured the callback correctly. For more information about callback configuration, see [Receiving Recording File](https://intl.cloud.tencent.com/document/product/647/35426).
- If you have configured the callback correctly, check whether the server can handle callbacks properly, for example, by using curl to simulate callback requests.

[](id:r8)
### Why are so many recording files generated?
- If **Global Auto-Recording** is selected in the console, each stream in a room will be recorded into a separate file.
- If you haven’t configured a resumption timeout period, a recording file will be generated each time a stream is interrupted.
- There is an upper limit to the duration of recording files in MP4, FLV, or AAC format. Whenever the limit is exceeded, a recording file and callback will be generated, and the recording will continue.
- Multiple recording files may be generated if stream mixing is initiated multiple times in a room.

