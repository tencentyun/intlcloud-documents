Video editing is an offline task that clips and splice videos in VOD. Specifically, it includes the following features:

* **Video clipping**: this refers to clipping a file in VOD to generating a new video.
* **Video splicing**: this refers to splicing multiple files in VOD to generate a new video.
* **Video clip splicing**: this refers to clipping multiple files in VOD and then splicing the clips to generate a new video.
* **Live stream transcoding**: this refers to transcoding a stream in VOD to generate a new video.
* **Stream clipping**: this refers to clipping a stream in VOD to generate a new video.
* **Stream splicing**: this refers to splicing multiple streams in VOD to generate a new video.
* **Stream clip splicing**: this refers to clipping multiple streams in VOD and then splicing the clips to generate a new video.

The container format of the generated video is MP4. When initiating a video editing task, you can specify whether to perform a [task flow](https://cloud.tencent.com/document/product/266/33475#.E4.BB.BB.E5.8A.A1.E6.B5.81) on the new video.

## Task Initiation

You can initiate a video editing task by calling a [server API](https://cloud.tencent.com/document/product/266/34783). The return result of the API contains the task ID, which is used to associate with the corresponding task result when [getting result](#.E7.BB.93.E6.9E.9C.E8.8E.B7.E5.8F.96).

## Getting Result

After initiating an editing task, you can wait for [result notification](https://cloud.tencent.com/document/product/266/33475#ResultNotification) asynchronously or perform [task query](https://cloud.tencent.com/document/product/266/33475#TaskQuery) synchronously to get the task execution result. Below is an example of getting the result notification in normal callback mode after the editing task is initiated (the fields with null value are omitted):

```json
{
    "EventType":"EditMediaComplete",
    "EditMediaComplete":{
        "TaskId":"EditMedia-f5ac8127b3b6b85cdc13f237c6005d8",
        "Status":"FINISH",
        "ErrCode":0,
        "Message":"SUCCESS",
        "Input":{
            "InputType":"File",
            "FileInfoSet":[
                {
                    "FileId":"24961954183381008",
                    "StartTimeOffset":0,
                    "EndTimeOffset":300
                },
                {
                    "FileId":"24961954183381009",
                    "StartTimeOffset":0,
                    "EndTimeOffset":300
                },
                {
                    "FileId":"24961954183381010",
                    "StartTimeOffset":0,
                    "EndTimeOffset":300
                }
            ]
        },
        "Output":{
            "FileType":"mp4",
            "FileId":"24961954183923290",
            "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
        },
        "ProcedureTaskId":""
    }
}
```

In the callback result, `Input.InputType` is `File`, indicating that the type of the edited video is of a file type. `Input.FileInfoSet` contains three elements, of which `StartTimeOffset` is `0` and `EndTimeOffset` is `300`, indicating to clip the first 5 minutes of each of the three videos and then splice them into a 15-minute video. `Output.FileId` is the `FileId` of the generated video, whose playback URL is the value in `FileUrl`.
