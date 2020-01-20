>
>- This document describes the callback on v3.0. For legacy callback on v2.0, please see [Legacy Callback](https://intl.cloud.tencent.com/document/product/266/33962#ClipComplete).
>- You are recommended to gradually migrate the callback to v3.0, as the documentation for callback v2.0 will no longer be updated.


## Event Name
ClipComplete

## Event Description
If the application is configured with event notification, after a video is clipped, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`ClipTask2017` structure](#APIhttps://intl.cloud.tencent.com/document/api/266/31773#ClipTask2017).


## Normal Callback
If you choose the normal callback mode, the callback URL will receive an HTTP request in the following format:
```json
{
    "EventType":"ClipComplete",
    "FileUploadEvent":null,
    "ProcedureStateChangeEvent":null,
    "FileDeleteEvent":null,
    "PullCompleteEvent":null,
    "EditMediaComplete":null,
    "WechatPublishComplete":null,
    "TranscodeCompleteEvent":null,
    "ConcatCompleteEvent":null,
    "ClipCompleteEvent":{
        "TaskId":"clipVideo-0a78cf44c4285026a4c",
        "SrcFileId":"16092504232103571364",
        "FileInfo":{
            "ErrCode":0,
            "Message":"",
            "FileId":"14508071098244929440",
            "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
            "FileType":"mp4"
        }
    },
    "CreateImageSpriteCompleteEvent":null,
    "SnapshotByTimeOffsetCompleteEvent":null
}
```

## Reliable Callback
If you choose the reliable callback mode, after the [PullEvents](#APIhttps://intl.cloud.tencent.com/document/api/266/31773) API is called, an HTTP response in the following format will be received.
```json
{
    "Response":{
        "EventSet":[
            {
                "EventHandle":"EventHandle.N",
                "EventType":"ClipComplete",
                "FileUploadEvent":null,
                "ProcedureStateChangeEvent":null,
                "FileDeleteEvent":null,
                "PullCompleteEvent":null,
                "EditMediaComplete":null,
                "WechatPublishComplete":null,
                "TranscodeCompleteEvent":null,
                "ConcatCompleteEvent":null,
                "ClipCompleteEvent":{
                    "TaskId":"clipVideo-0a78cf44c4285026a4c",
                    "SrcFileId":"16092504232103571364",
                    "FileInfo":{
                        "ErrCode":0,
                        "Message":"",
                        "FileId":"14508071098244929440",
                        "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                        "FileType":"mp4"
                    }
                },
                "CreateImageSpriteCompleteEvent":null,
                "SnapshotByTimeOffsetCompleteEvent":null
            }
        ],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
