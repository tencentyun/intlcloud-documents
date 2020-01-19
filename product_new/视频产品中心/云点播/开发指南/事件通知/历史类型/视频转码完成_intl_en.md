>
>- This document describes the callback on v3.0. For legacy callback on v2.0, please see [Legacy Callback](https://cloud.tencent.com/document/product/266/33796#TranscodeComplete).
>- You are recommended to gradually migrate the callback to v3.0, as the documentation for callback v2.0 will no longer be updated.

## Event Name
TranscodeComplete

## Event Description
If the application is configured with event notification, after a video is transcoded, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`TranscodeTask2017` structure](https://cloud.tencent.com/document/api/266/31773#TranscodeTask2017).


## Normal Callback
If you choose the normal callback mode, the callback URL will receive an HTTP request in the following format:
```json
{
    "EventType":"TranscodeComplete",
    "FileUploadEvent":null,
    "ProcedureStateChangeEvent":null,
    "FileDeleteEvent":null,
    "PullCompleteEvent":null,
    "EditMediaComplete":null,
    "WechatPublishComplete":null,
    "TranscodeCompleteEvent":{
        "TaskId":"Transcode-f5ac8127b3b6b85cdc13f237c6005d8",
        "ErrCode":0,
        "Message":"SUCCESS",
        "FileId":"24961954183923290",
        "FileName":"Animal World",
        "Duration":599,
        "CoverUrl":"http://125676836723.vod2.myqcloud.com/0/xxx/640.jpg",
        "PlayInfoSet":[
            {
                "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                "Definition":0,
                "Bitrate":246000,
                "Height":480,
                "Width":640
            },
            {
                "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f10.mp4",
                "Definition":10,
                "Bitrate":149193,
                "Height":240,
                "Width":320
            },
            {
                "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f20.mp4",
                "Definition":20,
                "Bitrate":297656,
                "Height":480,
                "Width":640
            },
            {
                "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f30.mp4",
                "Definition":30,
                "Bitrate":899976,
                "Height":960,
                "Width":1280
            }
        ]
    },
    "ConcatCompleteEvent":null,
    "ClipCompleteEvent":null,
    "CreateImageSpriteCompleteEvent":null,
    "SnapshotByTimeOffsetCompleteEvent":null
}
```

## Reliable Callback
If you choose the reliable callback mode, after the [PullEvents](/document/product/266/33433) API is called, an HTTP response in the following format will be received.
```json
{
    "Response":{
        "EventSet":[
            {
                "EventHandle":"EventHandle.N",
                "EventType":"TranscodeComplete",
                "FileUploadEvent":null,
                "ProcedureStateChangeEvent":null,
                "FileDeleteEvent":null,
                "PullCompleteEvent":null,
                "EditMediaComplete":null,
                "WechatPublishComplete":null,
                "TranscodeCompleteEvent":{
                    "TaskId":"Transcode-f5ac8127b3b6b85cdc13f237c6005d8",
                    "ErrCode":0,
                    "Message":"SUCCESS",
                    "FileId":"24961954183923290",
                    "FileName":"Animal World",
                    "Duration":599,
                    "CoverUrl":"http://125676836723.vod2.myqcloud.com/0/xxx/640.jpg",
                    "PlayInfoSet":[
                        {
                            "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                            "Definition":0,
                            "Bitrate":246000,
                            "Height":480,
                            "Width":640
                        },
                        {
                            "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f10.mp4",
                            "Definition":10,
                            "Bitrate":149193,
                            "Height":240,
                            "Width":320
                        },
                        {
                            "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f20.mp4",
                            "Definition":20,
                            "Bitrate":297656,
                            "Height":480,
                            "Width":640
                        },
                        {
                            "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f30.mp4",
                            "Definition":30,
                            "Bitrate":899976,
                            "Height":960,
                            "Width":1280
                        }
                    ]
                },
                "ConcatCompleteEvent":null,
                "ClipCompleteEvent":null,
                "CreateImageSpriteCompleteEvent":null,
                "SnapshotByTimeOffsetCompleteEvent":null
            }
        ],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
