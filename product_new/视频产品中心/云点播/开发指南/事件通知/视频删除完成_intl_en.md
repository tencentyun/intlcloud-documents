>!
>- This document describes the callback on v3.0. For legacy callback on v2.0, please see [Legacy Callback](https://intl.cloud.tencent.com/document/product/266/33962?lang=en&pg=#video-deletion-completion).
>- You are recommended to gradually migrate the callback to v3.0, as the documentation for callback v2.0 will no longer be updated.

## Event Name
FileDeleted

## Event Description
If the application is configured with event notification, after a video is deleted, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`FileDeleteTask` structure](https://intl.cloud.tencent.com/document/product/266/34187#FileDeleteTask).


## Samples
### Normal Callback
If you choose the normal callback mode, the callback URL will receive an HTTP POST request from VOD, whose content is in the `BODY` as shown below (the fields with null value are omitted):

```json
{
    "EventType":"FileDeleted",
    "FileDeleteEvent":{
        "FileIdSet":[
            "24961954183381008"
        ],
        "FileDeleteResultInfo":[
            {
                "FileId":"24961954183381008",
                "DeleteParts":[
                    {
                        "Type":"TranscodeFiles",
                        "Definition":0
                    }
                ]
            }
        ]
    }
}
```


### Reliable Callback
If you choose the reliable callback mode, after the [PullEvents](https://intl.cloud.tencent.com/document/product/266/34187) API is called, an HTTP response in the following format will be received (the fields with null value are omitted).


```json
{
    "Response":{
        "EventSet":[
            {
                "EventHandle":"EventHandle.N",
                "EventType":"FileDeleted",
                "FileDeleteEvent":{
                    "FileIdSet":[
                        "24961954183381008"
                    ],
                    "FileDeleteResultInfo":[
                        {
                            "FileId":"24961954183381008",
                            "DeleteParts":[
                                {
                                    "Type":"TranscodeFiles",
                                    "Definition":0
                                }
                            ]
                        }
                    ]
                }
            }
        ],
        "RequestId":"335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
