Transcoding is an offline task that converts the source audio/video bitstream. It changes parameters of the source bitstream, such as codec, resolution, and bitrate, to adapt it to different devices and network conditions. The following benefits can be achieved with transcoding:
- Compatible with multiple clients: A source video can be transcoded to formats (.mp4 for example) that are compatible with more types of devices for smooth playback.
- Adapt to different bandwidths: a source video can be transcoded for output in multiple definitions such as LD, SD, HD, and FHD. End users can select the appropriate bitrate depending on their network conditions.
- Improved playback efficiency: The moov atom can be moved from the end of an MP4 file to its beginning, so the video can be played before it is entirely downloaded.
- Watermarking: you can add a watermark to a video to mark ownership or copyright. For more information, please see [Watermarking](https://intl.cloud.tencent.com/document/product/266/33939).
- Reduce bandwidth usage: use advanced encoding modes (H.265 for example) for transcoding to reduce the bitrate of a video substantially with the original quality retained, thus lowering the payback bandwidth usage.

After a video is transcoded, the playback URL of the output video can be obtained according to [Getting the Result](#jghq). You can use your own player or a third-party player to play back the output video.

>The transcoding feature is mainly suitable for **UGSV** scenarios. For **long video** scenarios (video websites, online education, etc.), [adaptive bitrate streaming](https://intl.cloud.tencent.com/document/product/266/33942) can deliver a better user experience.

## [](id:zm)Transcoding Template

The target specification of an output video after transcoding is specified by parameters such as codec, resolution, and bitrate. VOD integrates these parameters in the transcoding template as shown below:
>? For more audio/video transcoding types, see [Supported transcoding types](https://intl.cloud.tencent.com/document/product/266/7898).
<table>
    <tr>
        <th style="width:18%">
            Type
        </th>
        <th style="width:22%">
            Parameter
        </th>
        <th>
            Description
        </th>
    </tr>
    <tr>
        <td rowspan=4>
            Muxing
        </td>
    </tr>
    <tr>
        <td>
            Container format
        </td>
        <td>
			Supported video and audio container formats for transcoding:
            <li>Video: MP4, TS, HLS, and FLV</li>
            <li>Audio: MP3, M4A, FLAC, and OGG</li>
        </td>
    </tr>
    <tr>
        <td>
            Deleting video stream
        </td>
        <td>
            If this is enabled, the output video will contain only the audio stream with no video stream.
        </td>
    </tr>
    <tr>
        <td>
            Deleting audio stream
        </td>
        <td>
            If this is enabled, the output video will contain only the video stream with no audio stream.
        </td>
    </tr>
    <tr>
        <td rowspan=7>
            Video codec
        </td>
        <td>
            Codec
        </td>
        <td>
            H.264 and H.265 are supported
        </td>
    </tr>
    <tr>
        <td>
            Bitrate
        </td>
        <td>
            Supported bitrate range: 10 Kbps - 35 Mbps
        </td>
    </tr>
    <tr>
        <td>
            Frame Rate
        </td>
        <td>
            Supported frame rate range: 1-60 fps; common values: 24, 25, and 30
        </td>
    </tr>
    <tr>
        <td>
            Resolution
        </td>
        <td>
            <li>Supported width range: 128-4096 px</li>
            <li>Supported height range: 128-4096 px</li>
        </td>
    </tr>
    <tr>
        <td>
            GOP length
        </td>
        <td>
            Supported GOP length range: 1-10s
        </td>
    </tr>
    <tr>
        <td>
            Profile
        </td>
        <td>
            <li>When the video codec is H.264, the `Baseline`, `Main`, and `High` profiles are supported.</li>
            <li>When the video codec is H.265, only the `Main` profile is supported.</li>
        </td>
    </tr>
    <tr>
        <td>
            Color Space
        </td>
        <td>
            YUV420P is supported.
        </td>
    </tr>
    <tr>
        <td rowspan=4>
            Audio codec
        </td>
        <td>
            Codec
        </td>
        <td>
            MP3, AAC, AC3, and FLAC are supported
        </td>
    </tr>
    <tr>
        <td>
            Sample rate
        </td>
        <td>
            The following audio sample rates are supported:
            <li>34000 Hz</li>
            <li>44100 Hz</li>
            <li>48000 Hz</li>
        </td>
    </tr>
    <tr>
        <td>
            Bitrate
        </td>
        <td>
            Supported bitrate range: 26-256 Kbps, including the following values:
            <li>48 Kbps</li>
            <li>64 Kbps</li>
            <li>128 Kbps</li>
        </td>
    </tr>
    <tr>
        <td>
            Channel
        </td>
        <td>
        	<li>Mono</li>
			    <li>Dual</li>
			    <li>Stereo</li>
        </td>
    </tr>
</table>

VOD provides a [List of Preset Parameter Templates](https://intl.cloud.tencent.com/document/product/266/33932) for common transcoding specifications. You can also create and manage custom transcoding templates on the console (see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059) for detailed directions) or through [server API](https://intl.cloud.tencent.com/document/product/266/34164).

## Initiating a Task

There are three ways to initiate a transcoding task, namely, directly initiating through server API, directly initiating through the console, and specifying a task upon upload. For more information, please see [Video Processing Task System](https://intl.cloud.tencent.com/document/product/266/33931) for video processing.

Methods of initiating transcoding tasks:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: specify the [transcoding template](#zm) ID in the `MediaProcessTask.TranscodeTaskSet` parameter in the request.
* Initiate a task on a video through the console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the specifications of transcoding output in it, and use it to [initiate video processing](https://intl.cloud.tencent.com/document/product/266/33892).
* Specify a task upon upload from server: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the specifications of transcoding output in it, and specify it as the `procedure` parameter in the [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120) API.
* Specify a task upon upload from client: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the specifications of transcoding output in it, and specify it as the `procedure` parameter in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922).
* Upload through console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the specifications of transcoding output in it, upload a video through the console, select [Process Video During Upload](https://intl.cloud.tencent.com/document/product/266/33890), and specify to execute this task flow upon video upload completion.

## Getting the Result[](id:jghq) 

After initiating a transcoding task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback (the fields with null value are omitted):

```json
{
    "EventType":"ProcedureStateChanged",
    "ProcedureStateChangeEvent":{
        "TaskId":"1256768367-Procedure-2e1af2456351812be963e309cc133403t0",
        "Status":"FINISH",
        "FileId":"5285890784246869930",
        "FileName":"Animal World",
        "FileUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/AtUCmy6gmIYA.mp4",
        "MetaData":{
            "AudioDuration":60,
            "AudioStreamSet":[
                {
                    "Bitrate":383854,
                    "Codec":"aac",
                    "SamplingRate":48000
                }
            ],
            "Bitrate":1021028,
            "Container":"mov,mp4,m4a,3gp,3g2,mj2",
            "Duration":60,
            "Height":480,
            "Rotate":0,
            "Size":7700180,
            "VideoDuration":60,
            "VideoStreamSet":[
                {
                    "Bitrate":637174,
                    "Codec":"h264",
                    "Fps":23,
                    "Height":480,
                    "Width":640
                }
            ],
            "Width":640
        },
        "MediaProcessResultSet":[
            {
                "Type":"Transcode",
                "TranscodeTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":220
                    },
                    "Output":{
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/v.f20.m3u8",
                        "Size":63120997,
                        "Container":"mov,mp4,m4a,3gp,3g2,mj2",
                        "Height":480,
                        "Width":640,
                        "Bitrate":513402,
                        "Md5":"084d403c73930ca2f835679af1f37bd3",
                        "Duration":60,
                        "VideoStreamSet":[
                            {
                                "Bitrate":473101,
                                "Codec":"h264",
                                "Fps":24,
                                "Height":480,
                                "Width":640
                            }
                        ],
                        "AudioStreamSet":[
                            {
                                "Bitrate":48581,
                                "Codec":"aac",
                                "SamplingRate":44100
                            }
                        ],
                        "Definition":220
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

In the callback result, `ProcedureStateChangeEvent.MediaProcessResultSet` contains the transcoding result with `Type` as `Transcode` and `Definition` as `220`.
