## イベント名
ReviewAudioVideoComplete

## イベントの説明
Appにイベント通知が設定され、かつオーディオビデオ審査が完了した場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」からイベント通知を取得することができます。イベント通知の内容は [ReviewAudioVideoTaskの構造](https://www.tencentcloud.com/document/product/266/34187#ReviewAudioVideoTask)です。

## 事例
### 通常のコールバック
通常のコールバックモードを選択すると、コールバックURLはVODからのHTTPリクエストを受信します。リクエストはPOSTメソッドを使用します。リクエストの内容は、以下に示すようにBODYにあります（null値のフィールドは省略されています）。

```json
{
    "EventType": "ReviewAudioVideoComplete",
    "ReviewAudioVideoCompleteEvent": {
        "TaskId": "125xxxx-ReviewAudioVideo-07edbc78ba20563cdf2362cffbf4aa0ct",
        "Status": "FINISH",
        "ErrCodeExt": "",
        "Message": "SUCCESS",
        "Input":{
            "FileId": "387702130626135215"
        },
        "Output":{
            "Suggestion": "block",
            "Label": "porn",
            "Form": "Image",
            "SegmentSet":[
                {
                    "StartTimeOffset": 0,
                    "EndTimeOffset": 1,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "porn",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": []
                },
                {
                    "StartTimeOffset": 1,
                    "EndTimeOffset": 2,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "porn",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": []
                },
                {
                    "StartTimeOffset": 2,
                    "EndTimeOffset": 3,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "porn",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": []
                },
                {
                    "StartTimeOffset": 3,
                    "EndTimeOffset": 4,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "porn",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": []
                },
                {
                    "StartTimeOffset": 4,
                    "EndTimeOffset": 5,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "porn",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": []
                },
                {
                    "StartTimeOffset": 5,
                    "EndTimeOffset": 6,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "porn",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": []
                },
                {
                    "StartTimeOffset": 6,
                    "EndTimeOffset": 7,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "porn",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": []
                },
                {
                    "StartTimeOffset": 7,
                    "EndTimeOffset": 8,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "porn",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": []
                },
                {
                    "StartTimeOffset": 8,
                    "EndTimeOffset": 9,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "porn",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": []
                },
                {
                    "StartTimeOffset": 9,
                    "EndTimeOffset": 10,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "porn",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": []
                }
            ],
            "SegmentSetFileUrl": "http://251000800.vod2.myqcloud.com/a8800b40vodtranssgp251000800/0f9bd2b0-34a8-4642-f481-001894d93019.txt",
            "SegmentSetFileUrlExpireTime": "2022-10-12T07:01:07.695Z"
        },
        "SessionContext": "",
        "SessionId": ""
    }
}
```


### 信頼できるコールバック
信頼できるコールバックモードを選択し、[プルイベント通知](https://intl.cloud.tencent.com/document/product/266/34183) APIが呼び出された後に、次の形式のHTTPレスポンスを受信します（null値のフィールドは省略されています）。

```json
{
    "Response":{
        "EventSet":[
            {
                "EventHandle": "EventHandle.N",
                "EventType": "ReviewAudioVideoComplete",
                "ReviewAudioVideoCompleteEvent": {
                    "TaskId": "125xxxx-ReviewAudioVideo-07edbc78ba20563cdf2362cffbf4aa0ct",
                    "Status": "FINISH",
                    "ErrCodeExt": "",
                    "Message": "SUCCESS",
                    "Input":{
                        "FileId": "387702130626135215"
                    },
                    "Output":{
                        "Suggestion": "block",
                        "Label": "porn",
                        "Form": "Image",
                        "SegmentSet":[
                            {
                                "StartTimeOffset": 0,
                                "EndTimeOffset": 1,
                                "Confidence": 99,
                                "Suggestion": "block",
                                "Label": "Porn",
                                "SubLabel": "porn",
                                "Form": "Image",
                                "AreaCoordSet": [],
                                "Text": "",
                                "KeywordSet": []
                            },
                            {
                                "StartTimeOffset": 1,
                                "EndTimeOffset": 2,
                                "Confidence": 99,
                                "Suggestion": "block",
                                "Label": "Porn",
                                "SubLabel": "porn",
                                "Form": "Image",
                                "AreaCoordSet": [],
                                "Text": "",
                                "KeywordSet": []
                            },
                            {
                                "StartTimeOffset": 2,
                                "EndTimeOffset": 3,
                                "Confidence": 99,
                                "Suggestion": "block",
                                "Label": "Porn",
                                "SubLabel": "porn",
                                "Form": "Image",
                                "AreaCoordSet": [],
                                "Text": "",
                                "KeywordSet": []
                            },
                            {
                                "StartTimeOffset": 3,
                                "EndTimeOffset": 4,
                                "Confidence": 99,
                                "Suggestion": "block",
                                "Label": "Porn",
                                "SubLabel": "porn",
                                "Form": "Image",
                                "AreaCoordSet": [],
                                "Text": "",
                                "KeywordSet": []
                            },
                            {
                                "StartTimeOffset": 4,
                                "EndTimeOffset": 5,
                                "Confidence": 99,
                                "Suggestion": "block",
                                "Label": "Porn",
                                "SubLabel": "porn",
                                "Form": "Image",
                                "AreaCoordSet": [],
                                "Text": "",
                                "KeywordSet": []
                            },
                            {
                                "StartTimeOffset": 5,
                                "EndTimeOffset": 6,
                                "Confidence": 99,
                                "Suggestion": "block",
                                "Label": "Porn",
                                "SubLabel": "porn",
                                "Form": "Image",
                                "AreaCoordSet": [],
                                "Text": "",
                                "KeywordSet": []
                            },
                            {
                                "StartTimeOffset": 6,
                                "EndTimeOffset": 7,
                                "Confidence": 99,
                                "Suggestion": "block",
                                "Label": "Porn",
                                "SubLabel": "porn",
                                "Form": "Image",
                                "AreaCoordSet": [],
                                "Text": "",
                                "KeywordSet": []
                            },
                            {
                                "StartTimeOffset": 7,
                                "EndTimeOffset": 8,
                                "Confidence": 99,
                                "Suggestion": "block",
                                "Label": "Porn",
                                "SubLabel": "porn",
                                "Form": "Image",
                                "AreaCoordSet": [],
                                "Text": "",
                                "KeywordSet": []
                            },
                            {
                                "StartTimeOffset": 8,
                                "EndTimeOffset": 9,
                                "Confidence": 99,
                                "Suggestion": "block",
                                "Label": "Porn",
                                "SubLabel": "porn",
                                "Form": "Image",
                                "AreaCoordSet": [],
                                "Text": "",
                                "KeywordSet": []
                            },
                            {
                                "StartTimeOffset": 9,
                                "EndTimeOffset": 10,
                                "Confidence": 99,
                                "Suggestion": "block",
                                "Label": "Porn",
                                "SubLabel": "porn",
                                "Form": "Image",
                                "AreaCoordSet": [],
                                "Text": "",
                                "KeywordSet": []
                            }
                        ],
                        "SegmentSetFileUrl": "http://251000800.vod2.myqcloud.com/a8800b40vodtranssgp251000800/0f9bd2b0-34a8-4642-f481-001894d93019.txt",
                        "SegmentSetFileUrlExpireTime": "2022-10-12T07:01:07.695Z"
                    },
                    "SessionContext": "",
                    "SessionId": ""
                }
            }
        ],
        "RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
