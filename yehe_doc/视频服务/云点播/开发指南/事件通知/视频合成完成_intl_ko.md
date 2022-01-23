## 이벤트 이름
ComposeMediaComplete

## 이벤트 설명
App에 이벤트 알림이 설정된 경우 동영상 합성 후 App 백엔드는 ‘일반 콜백’ 또는 ‘신뢰할 수 있는 콜백’을 통해 이벤트 알림을 받을 수 있습니다. 이벤트 알림의 내용은 [ComposeMediaTask 구조](https://intl.cloud.tencent.com/document/product/266/34187#ComposeMediaTask)입니다.

## 예시
### 일반 콜백
일반 콜백 모드를 선택하면 콜백 URL은 아래와 같이 BODY에 내용이 있는 VOD로부터 HTTP POST 요청을 수신합니다(null 값이 있는 필드는 생략됨).

```json
{
    "EventType": "ComposeMediaComplete",
    "ComposeMediaCompleteEvent": {
        "TaskId": "1256768367-ComposeMedia-f5ac8127b3b6b85cdc13f237c6005d8",
        "Status": "FINISH",
        "ErrCode": 0,
        "Message": "SUCCESS",
        "Input":{
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
            "Output":{
                "FileName": "동영상 합성 효과 테스트",
                "Container": "mp4"
            }
        },
        "Output":{
            "FileType": "mp4",
            "FileId": 5285485487985271490,
            "FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4"
        }
    }
}
```


### 신뢰할 수 있는 콜백
신뢰할 수 있는 콜백 모드를 선택하면 [PullEvents](/document/product/266/33433) API가 호출된 후 다음 형식의 HTTP 응답이 수신됩니다(null 값이 있는 필드는 생략됨).

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
                            "FileName":"동영상 합성 효과 테스트",
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
