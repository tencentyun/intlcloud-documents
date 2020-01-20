>
>- This document describes the callback on v3.0. For legacy callback on v2.0, please see [Legacy Callback](https://intl.cloud.tencent.com/document/product/266/33962#CreateImageSpriteComplete).
>- You are recommended to gradually migrate the callback to v3.0, as the documentation for callback v2.0 will no longer be updated.

## Event Name
CreateImageSpriteComplete

## Event Description
If the application is configured with event notification, after image sprite generating is completed, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`CreateImageSpriteTask2017` structure](#APIhttps://intl.cloud.tencent.com/document/api/266/31773#CreateImageSpriteTask2017).


## Normal Callback
If you choose the normal callback mode, the callback URL will receive an HTTP request in the following format:
```json
{
    "EventType":"CreateImageSpriteComplete",
    "FileUploadEvent":null,
    "ProcedureStateChangeEvent":null,
    "FileDeleteEvent":null,
    "PullCompleteEvent":null,
    "EditMediaComplete":null,
    "WechatPublishComplete":null,
    "TranscodeCompleteEvent":null,
    "ConcatCompleteEvent":null,
    "ClipCompleteEvent":null,
    "CreateImageSpriteCompleteEvent":{
        "ErrCode":0,
        "Message":"",
        "TaskId":"CreateImageSprite-1edb7eb88a599d05abe451cfc541cfbd",
        "FileId":"14508071098244929440",
        "Definition":10,
        "TotalCount":106,
        "ImageSpriteUrlSet":[
            "http://125676836723.vod2.myqcloud.com/xxx/xxx/1.png",
            "http://125676836723.vod2.myqcloud.com/xxx/xxx/2.png"
        ],
        "WebVttUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.vtt"
    }
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
                "EventType":"CreateImageSpriteComplete",
                "FileUploadEvent":null,
                "ProcedureStateChangeEvent":null,
                "FileDeleteEvent":null,
                "PullCompleteEvent":null,
                "EditMediaComplete":null,
                "WechatPublishComplete":null,
                "TranscodeCompleteEvent":null,
                "ConcatCompleteEvent":null,
                "ClipCompleteEvent":null,
                "CreateImageSpriteCompleteEvent":{
                    "ErrCode":0,
                    "Message":"",
                    "TaskId":"CreateImageSprite-1edb7eb88a599d05abe451cfc541cfbd",
                    "FileId":"14508071098244929440",
                    "Definition":10,
                    "TotalCount":106,
                    "ImageSpriteUrlSet":[
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/1.png",
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/2.png"
                    ],
                    "WebVttUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.vtt"
                }
            }
        ],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
