>
>- This document describes the callback on v3.0. For legacy callback on v2.0, please see [Legacy Callback](https://cloud.tencent.com/document/product/266/33796#ConcatComplete).
>- You are recommended to gradually migrate the callback to v3.0, as the documentation for callback v2.0 will no longer be updated.

## Event Name
ConcatComplete

## Event Description
If the application is configured with event notification, after a video is transcoded, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`ConcatTask2017` structure](https://cloud.tencent.com/document/api/266/31773#ConcatTask2017).


## Normal Callback
If you choose the normal callback mode, the callback URL will receive an HTTP request in the following format:
```json
{
    "EventType":"ConcatComplete",
    "FileUploadEvent":null,
    "ProcedureStateChangeEvent":null,
    "FileDeleteEvent":null,
    "PullCompleteEvent":null,
    "EditMediaComplete":null,
    "WechatPublishComplete":null,
    "TranscodeCompleteEvent":null,
    "ConcatCompleteEvent":{
        "TaskId":"Concat-1edb7eb88a599d05abe451cfc541cfbd",
        "FileInfoSet":[
            {
                "ErrCode":0,
                "Message":"",
                "FileId":"14508071098244931831",
                "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/playlist.f6.m3u8",
                "FileType":"m3u8"
            },
            {
                "ErrCode":0,
                "Message":"",
                "FileId":"14508071098244929440",
                "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                "FileType":"mp4"
            }
        ]
    },
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
                "EventType":"ConcatComplete",
                "FileUploadEvent":null,
                "ProcedureStateChangeEvent":null,
                "FileDeleteEvent":null,
                "PullCompleteEvent":null,
                "EditMediaComplete":null,
                "WechatPublishComplete":null,
                "TranscodeCompleteEvent":null,
                "ConcatCompleteEvent":{
                    "TaskId":"Concat-1edb7eb88a599d05abe451cfc541cfbd",
                    "FileInfoSet":[
                        {
                            "ErrCode":0,
                            "Message":"",
                            "FileId":"14508071098244931831",
                            "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/playlist.f6.m3u8",
                            "FileType":"m3u8"
                        },
                        {
                            "ErrCode":0,
                            "Message":"",
                            "FileId":"14508071098244929440",
                            "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                            "FileType":"mp4"
                        }
                    ]
                },
                "ClipCompleteEvent":null,
                "CreateImageSpriteCompleteEvent":null,
                "SnapshotByTimeOffsetCompleteEvent":null
            }
        ],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
