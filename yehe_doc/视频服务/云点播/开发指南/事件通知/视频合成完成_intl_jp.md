## イベント名
ComposeMediaComplete

## イベントの説明
Appがイベント通知で構成されている場合、かつビデオの合成が完了した場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」を介してイベント通知を取得することができます。APIイベント通知の内容は、[ComposeMediaTaskの構造](https://intl.cloud.tencent.com/document/product/266/34187#ComposeMediaTask)です。

## 事例
### 通常のコールバック
通常のコールバックモードを選択すると、コールバックURLはVODからのHTTPリクエストを受信します。リクエストはPOSTメソッドを使用します。リクエストの内容は、以下に示すようにBODYにあります（null値のフィールドは省略されています）。

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
                "FileName": "ビデオ合成効果テスト",
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


### 信頼できるコールバック
信頼できるコールバックモードを選択し、[プルイベント通知](https://www.tencentcloud.com/document/product/266/34183)APIが呼び出された後に、次の形式のHTTPレスポンスを受信します（null値のフィールドは省略されています）。

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
                            "FileName":"ビデオ合成効果テスト",
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
