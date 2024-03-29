>!
>- This document describes the callback on version 3.0. 
>- You are recommended to gradually migrate the callback to v3.0, as the documentation for callback v2.0 will no longer be updated.

## Event Name
PullComplete

## Event Description
If the application is configured with event notification, after a video pull upload is completed, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`PullComplete` structure](https://intl.cloud.tencent.com/document/product/266/34187#EventContent).


## Examples
### Normal callback
If you choose the normal callback mode, the callback URL will receive an HTTP POST request from VOD, and its content is in the `BODY` as shown below (the fields with null value are omitted):

```json
{
    "EventType": "PullComplete", 
    "PullCompleteEvent":{
"TaskId": "125676836723-Pull-f5ac8127b3b6b85cdc13f237c6005d8", 
        "Status": "FINISH",
        "ErrCode": 0, 
        "Message": "SUCCESS", 
            "FileId": "14508071098244959037", 
            "MediaBasicInfo": {
                "Name": "Animal World", 
                "Description": "", 
                "CreateTime": "2019-01-09T16:36:22Z", 
                "UpdateTime": "2019-01-09T16:36:24Z", 
                "ExpireTime": "9999-12-31T23:59:59Z", 
                "ClassId": 0, 
                "ClassName": "Other", 
                "ClassPath": "Other", 
                "CoverUrl": "", 
                "Type": "mp4", 
                "MediaUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4", 
                "TagSet": [ ], 
                "StorageRegion": "ap-guangzhou-2", 
                "SourceInfo": {
                    "SourceType": "Upload", 
                    "SourceContext": ""
                }, 
                "Vid": ""
        }, 
        "FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4", 
        "ProcedureTaskId": "",
        "ReviewAudioVideoTaskId":"",
        "SessionContext": "",
        "SessionId": ""
    }
}
```

### Reliable callback
If you choose the reliable callback mode, after the [event notification puling](https://intl.cloud.tencent.com/document/product/266/34187) API is called, an HTTP response in the following format will be received (the fields with null values are omitted).

```json
{
    "Response": {
        "EventSet": [
            {
                "EventHandle": "EventHandleX", 
                "EventType": "PullComplete", 
                "PullCompleteEvent": {
                    "TaskId": "125676836723-Pull-f5ac8127b3b6b85cdc13f237c6005d8", 
                    "Status": "FINISH",
                    "ErrCode": 0, 
                    "Message": "SUCCESS", 
                        "FileId": "14508071098244959037", 
                        "MediaBasicInfo": {
                            "Name": "Animal World", 
                            "Description": "", 
                            "CreateTime": "2019-01-09T16:36:22Z", 
                            "UpdateTime": "2019-01-09T16:36:24Z", 
                            "ExpireTime": "9999-12-31T23:59:59Z", 
                            "ClassId": 0, 
                            "ClassName": "Other", 
                            "ClassPath": "Other", 
                            "CoverUrl": "", 
                            "Type": "mp4", 
                            "MediaUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4", 
                            "TagSet": [ ], 
                            "StorageRegion": "ap-guangzhou-2", 
                            "SourceInfo": {
                                "SourceType": "Upload", 
                                "SourceContext": ""
                            }, 
                            "Vid": ""
                    }, 
                    "FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4", 
                    "ProcedureTaskId": "",
                    "ReviewAudioVideoTaskId":"",
                    "SessionContext": "",
                    "SessionId": ""
                }
            }
        ]
    }
}
```
