## Event Name
ReviewAudioVideoComplete

## Event Description
If you have configured event notifications for your application, after a moderation task is completed, your application backend will be notified either by a “normal callback” or a “reliable callback”. For the content of the callback, see [ReviewAudioVideoTask](https://www.tencentcloud.com/document/product/266/34187#ReviewAudioVideoTask).

## Examples
### Normal callback
In the normal callback mode, your callback URL will receive an HTTP POST request from VOD. The content of the callback is included in the request body, as shown below (fields with null values are omitted):

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
            "SegmentSet": [
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


### Reliable callback
In the reliable callback mode, after calling the [PullEvents](https://intl.cloud.tencent.com/document/product/266/34183) API, you will receive an HTTP response in the following format (fields with null values are omitted):

```json
{
    "Response": {
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
                        "SegmentSet": [
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
