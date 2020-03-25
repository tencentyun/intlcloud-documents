Transcoding is an offline task that converts the source video bitstream to another one. It changes parameters of the source bitstream, such as encoder, resolution, and bitrate, to adapt it to different devices and network conditions. The following benefits can be achieved with transcoding:
- Compatibility with more devices: a source video can be transcoded to various formats (e.g., MP4) that are compatible with more types of devices for smooth playback.
- Adaption to different bandwidth options: a source video can be transcoded and output in various definitions such as LD, SD, HD, and FHD, and end users can select the most appropriate bitrate for their network conditions.
- Improvement in playback efficiency: the moov atom can be moved from the end of an MP4 file to its beginning, so that the player can play back a video before the entire video is downloaded.
- Watermarking: a watermark can be added to a video to mark video ownership or copyright. For more information, please see [Watermarking](https://intl.cloud.tencent.com/document/product/266/33939).
- Reduced bandwidth consumption: with a more advanced codec (e.g., H.265), the bitrate of a video can be substantially reduced while retaining the original quality, which helps reduce the bandwidth consumption.
<span id = "zm" ></span>
## Transcoding Template


The target specification of an output video after transcoding is subject to parameters such as encoder, resolution, and bitrate, which can be customized in the form of VOD transcoding template as shown below:

<table>
    <tr>
        <th style="width:18%">
            Category
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
			The following video and audio container formats are supported:
            <li>Video: MP4, TS, HLS, and FLV</li>
            <li>Audio: MP3, M4A, FLAC, and OGG</li>
        </td>
    </tr>
    <tr>
        <td>
            Video stream deletion
        </td>
        <td>
            If this parameter is enabled, the output video after transcoding will contain only the audio stream with the video stream discarded
        </td>
    </tr>
    <tr>
        <td>
            Audio stream deletion
        </td>
        <td>
            If this parameter is enabled, the output video after transcoding will contain only the video stream with the audio stream discarded
        </td>
    </tr>
    <tr>
        <td rowspan=7>
            Video encoding
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
            Supported bitrate range: 10 Kbps–35 Mbps
        </td>
    </tr>
    <tr>
        <td>
            Frame rate
        </td>
        <td>
            Supported frame rate range: 1–60 fps; common values: 24, 25, and 30 fps
        </td>
    </tr>
    <tr>
        <td>
            Resolution
        </td>
        <td>
            <li>Supported width range: 128–4,096 px</li>
            <li>Supported height range: 128–4,096 px</li>
        </td>
    </tr>
    <tr>
        <td>
            GOP length
        </td>
        <td>
            Supported GOP length range: 1–10s
        </td>
    </tr>
    <tr>
        <td>
            Profile
        </td>
        <td>
            <li>When the video codec is H.264, the `Baseline`, `Main`, and `High` profiles are supported</li>
            <li>When the video codec is H.265, only the `Main` profile is supported</li>
        </td>
    </tr>
    <tr>
        <td>
            Color space
        </td>
        <td>
            YUV420p is supported
        </td>
    </tr>
    <tr>
        <td rowspan=4>
            Audio encoding parameter
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
            <li>34,000 Hz</li>
            <li>44,100 Hz</li>
            <li>48,000 Hz</li>
        </td>
    </tr>
    <tr>
        <td>
            Bitrate
        </td>
        <td>
            Supported bitrate range: 26–256 Kbps, including the following values:
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

For common transcoding specifications, VOD provides a [preset transcoding template](https://intl.cloud.tencent.com/document/product/266/33932#transcoding). In addition, you can also create and manage custom transcoding templates in the console (for detailed directions, please see [Template Settings](https://intl.cloud.tencent.com/document/product/266/14059#.E8.A7.86.E9.A2.91.E8.BD.AC.E7.A0.81.E6.A8.A1.E6.9D.BF)) <!--api or through [server API](https://intl.cloud.tencent.com/document/product/266/33773)-->.

## Task Initiation

There are three ways to initiate a transcoding task, namely, directly initiating through server API, directly initiating through the console, and specifying a task upon upload. For more information, please see [Task Initiation](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask) for video processing.

Below are instructions for initiating transcoding tasks in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: specify the [transcoding template](#zm) ID in the `MediaProcessTask.TranscodeTaskSet` parameter in the request.
* Initiate a task on a video through the console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target transcoding specification in the task flow, and use the task flow to [initiate video processing](https://intl.cloud.tencent.com/document/product/266/33890).
* Specify a task upon upload from server: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target transcoding specification in the task flow, and specify this task flow as the `procedure` in the [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) request.
* Specify a task upon upload from client: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target transcoding specification in the task flow, and specify this task flow as the `procedure` parameter in the [signature for upload from client](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0).
* Upload through console: [add a task flow](https://intl.cloud.tencent.com/document/product/266/14058) in the console, set the target transcoding specification in the task flow, upload a video through the console, select [Process Video During Upload](https://intl.cloud.tencent.com/document/product/266/33890#.E6.9C.AC.E5.9C.B0.E4.B8.8A.E4.BC.A0.E6.AD.A5.E9.AA.A4), and specify to execute this task flow upon video upload completion.

## Getting Result

After initiating a transcoding task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the transcoding task is initiated (the fields with null value are omitted):

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

In the callback result, `ProcedureStateChangeEvent.MediaProcessResultSet` contains the transcoding result in `Type` of `Transcode`, and `Definition` is 220.
