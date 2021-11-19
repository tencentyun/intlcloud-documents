Adaptive bitrate streaming refers to the process of transcoding a video into adaptive bitrate streams. The results include audio/video files with different bitrates and a descriptive manifest file. A player can dynamically select the most appropriate bitrate for playback based on the current bandwidth. Currently, the most widely used adaptive bitrate streaming format is HLS [master playlist](https://developer.apple.com/documentation/http_live_streaming/example_playlists_for_http_live_streaming/creating_a_master_playlist).

VOD can transcode videos to adaptive bitrate streams in HLS and MPEG-DASH formats. This feature has the following benefits:
* The player can dynamically select the most appropriate bitrate for playback based on the current bandwidth, delivering a smooth viewing experience.
* Mainstream players natively support HLS adaptive bitrate with no customization required.
* VOD provides a [superplayer SDK](https://intl.cloud.tencent.com/document/product/266/7836), which you can integrate into your project quickly and conveniently to enable the playback of adaptive bitrate streams.



## [](id:zsy)Adaptive Bitrate Streaming Template

You can specify the "video transcoding parameter", "audio transcoding parameter", and other parameters for each adaptive bitrate substream. VOD uses an adaptive bitrate streaming template to represent the parameters.

| Parameter | Description |
| -- | -- |
| Protocol | Adaptive bitrate streaming protocol. Currently, HLS and MPEG-DASH are supported. |
|Encryption|Currently, only HLS supports simple AES encryption. MPEG-DASH does not support encryption.|
| Substream specification | Controls how many substreams are output and the video and audio transcoding parameters of each substream: <li>Video transcoding parameters: resolution, bitrate, frame rate, codec, etc.</li><li>Audio transcoding parameters: sample rate, sound channel, codec, etc.</li> |
| Whether to filter "low resolution to high resolution" | Generally, a source video with a low resolution cannot be converted to high resolution to improve the video and sound quality. Enabling filtering "low resolution to high resolution" can help avoid unnecessary transcoding |

VOD provides [preset adaptive bitrate streaming templates](https://intl.cloud.tencent.com/document/product/266/33932) that include common parameter combinations. You can also customize your own template.

## Initiating a Task

There are three ways to initiate a transcoding task, namely, through a server API, via the console, and by specifying a task for video upon upload. For more information, please see “Task Initiation” in [Video Processing Task System](https://intl.cloud.tencent.com/document/product/266/33931).

Below are instructions for initiating adaptive bitrate streaming tasks in these ways:

* Call the server API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125) to initiate a task: set `MediaProcessTask.AdaptiveDynamicStreamingTaskSet` to the ID of the [adaptive bitrate streaming template](#zsy) in the API request.
* Initiate a task via the console: call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create an adaptive bitrate task flow (by specifying `MediaProcessTask.AdaptiveDynamicStreamingTaskSet`), and use it to [process videos](https://intl.cloud.tencent.com/document/product/266/33892) in the console.
* Specify a task upon upload from server: call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create an adaptive bitrate streaming task flow, (by specifying `MediaProcessTask.AdaptiveDynamicStreamingTaskSet`), and in the [ApplyUpload](https://intl.cloud.tencent.com/document/product/266/34120) request, set `procedure` to the created task flow.
* Specify a task upon upload from client: call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create an adaptive bitrate streaming task flow (by specifying `MediaProcessTask.AdaptiveDynamicStreamingTaskSet`), and in the [request to upload video from client](https://intl.cloud.tencent.com/document/product/266/33922), set `procedure` to the created task flow.
* Specify a task upon upload from the console: call a [server API](https://intl.cloud.tencent.com/document/product/266/34167) to create an adaptive bitrate task flow (by specifying `MediaProcessTask.AdaptiveDynamicStreamingTaskSet`), and when uploading video via the console, choose [**Automatic Processing After Upload**](https://intl.cloud.tencent.com/document/product/266/33890) and select the created task flow.

## Obtain Results

After initiating an adaptive bitrate streaming task, you can wait for [result notification](https://intl.cloud.tencent.com/document/product/266/33931) asynchronously or perform [task query](https://intl.cloud.tencent.com/document/product/266/33931) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the adaptive bitrate streaming task is initiated (the fields with null value are omitted):

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
                "Type":"AdaptiveDynamicStreaming",
                "AdaptiveDynamicStreamingTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Definition":10,
                        "Package":"hls",
                        "DrmType":"",
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/adp.10.m3u8"
                    }
                }
            },
            {
                "Type":"AdaptiveDynamicStreaming",
                "AdaptiveDynamicStreamingTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":20
                    },
                    "Output":{
                        "Definition":20,
                        "Package":"dash",
                        "DrmType":"",
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/adp.20.mpd"
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

In the callback, `ProcedureStateChangeEvent.MediaProcessResultSet` contains two adaptive bitrate streams, whose `Type` is `AdaptiveDynamicStreaming` and `Definition` 10 and 20 respectively.

