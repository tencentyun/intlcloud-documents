## 이벤트 이름
ReviewAudioVideoComplete

## 이벤트 설명
App에 이벤트 알림이 설정된 경우 오디오/비디오 조정 완료 후 App 백엔드는 ‘일반 콜백’ 또는 ‘신뢰할 수 있는 콜백’을 통해 이벤트 알림을 받을 수 있습니다. 이벤트 알림의 내용은 [ReviewAudioVideoTask](https://www.tencentcloud.com/document/product/266/34187#ReviewAudioVideoTask)입니다.

## 예시
### 일반 콜백
일반 콜백 모드를 선택하면 콜백 URL은 아래와 같이 BODY에 내용이 있는 VOD로부터 HTTP POST 요청을 수신합니다(null 값이 있는 필드는 생략됨).

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


### 신뢰할 수 있는 콜백
신뢰할 수 있는 콜백 모드를 선택하면 [PullEvents](https://intl.cloud.tencent.com/document/product/266/34183) API가 호출된 후 다음 형식의 HTTP 응답이 수신됩니다(null 값이 있는 필드는 생략됨).

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
