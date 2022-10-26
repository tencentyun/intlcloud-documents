## Event Name
ComposeMediaComplete

## Event Description
If the application is configured with event notification, after a video is composed, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`ComposeMediaTask` structure](https://intl.cloud.tencent.com/document/product/266/34187#ComposeMediaTask).

## Samples
### Normal callback
If you choose the normal callback mode, the callback URL will receive an HTTP POST request from VOD, whose content is in the `BODY` as shown below (the fields with null value are omitted):

```json
{
    "EventType": "ComposeMediaComplete",
    "ComposeMediaCompleteEvent": {
        "TaskId": "1256768367-ComposeMedia-f5ac8127b3b6b85cdc13f237c6005d8",
        "Status": "FINISH",
        "ErrCode": 0,
        "Message": "SUCCESS",
        "Input": {
            "Tracks": [{
                    "Type": "Video",
                    "TrackItems": [{
                        "Type": "Video",
                        "SourceMedia": "5285485487985271487",
                        "AudioOperations": [{
                            "Type": "Volume",
                            "VolumeParam": {
                                "Mute": 1
                            }
                        }]
                    }]
                },
                {
                    "Type": "Audio",
                    "TrackItems": [{
                            "Type": "Empty",
                            "EmptyItem": {
                                "Duration": 5
                            }
                        },
                        {
                            "Type": "Audio",
                            "AudioItem": {
                                "SourceMedia": "5285485487985271488",
                                "Duration": 15
                            }
                        },
                        {
                            "Type": "Audio",
                            "AudioItem": {
                                "SourceMedia": "5285485487985271489",
                                "SourceMediaStartTime": 2,
                                "Duration": 14
                            }
                        }
                    ]
                }
            ],
            "Output": {
                "FileName": "Video composing effect test",
                "Container": "mp4"
            }
        },
        "Output": {
            "FileType": "mp4",
            "FileId": 5285485487985271490,
            "FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4"
        }
    }
}
```


### Reliable callback
If you choose the reliable callback mode, after the [PullEvents](https://www.tencentcloud.com/document/product/266/34183) API is called, an HTTP response in the following format will be received (the fields with null value are omitted).

```json
{
    "Response":{
        "EventSet":[
            {
                "EventHandle":"EventHandle.N",
                "ComposeMediaCompleteEvent":{
                    "TaskId":"1256768367-ComposeMedia-f5ac8127b3b6b85cdc13f237c6005d8",
                    "Status":"FINISH",
                    "ErrCode":0,
                    "Message":"SUCCESS",
                    "Input":{
                        "Tracks":[
                            {
                                "Type":"Video",
                                "TrackItems":[
                                    {
                                        "Type":"Video",
                                        "SourceMedia":"5285485487985271487",
                                        "AudioOperations":[
                                            {
                                                "Type":"Volume",
                                                "VolumeParam":{
                                                    "Mute":1
                                                }
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                "Type":"Audio",
                                "TrackItems":[
                                    {
                                        "Type":"Empty",
                                        "EmptyItem":{
                                            "Duration":5
                                        }
                                    },
                                    {
                                        "Type":"Audio",
                                        "AudioItem":{
                                            "SourceMedia":"5285485487985271488",
                                            "Duration":15
                                        }
                                    },
                                    {
                                        "Type":"Audio",
                                        "AudioItem":{
                                            "SourceMedia":"5285485487985271489",
                                            "SourceMediaStartTime":2,
                                            "Duration":14
                                        }
                                    }
                                ]
                            }
                        ],
                        "Output":{
                            "FileName":"Video composing effect test",
                            "Container":"mp4"
                        }
                    },
                    "Output":{
                        "FileType":"mp4",
                        "FileId":5285485487985271490,
                        "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4"
                    }
                }
            }
        ],
        "RequestId":"335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
