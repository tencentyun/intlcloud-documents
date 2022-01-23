## 이벤트 이름
EditMediaComplete

## 이벤트 설명
App에 이벤트 알림이 설정된 경우 동영상 편집 완료 후 App 백엔드는 ‘일반 콜백’ 또는 ‘신뢰할 수 있는 콜백’을 통해 이벤트 알림을 받을 수 있습니다. 이벤트 알림의 내용은 [EditMediaTask 구조](https://intl.cloud.tencent.com/document/product/266/34187#EditMediaTask)입니다.

## 예시
### 일반 콜백
일반 콜백 모드를 선택하면 콜백 URL은 아래와 같이 BODY에 내용이 있는 VOD로부터 HTTP POST 요청을 수신합니다(null 값이 있는 필드는 생략됨).

```json
{
    "EventType":"EditMediaComplete",
    "EditMediaCompleteEvent":{
        "TaskId":"1256768367-EditMedia-f5ac8127b3b6b85cdc13f237c6005d8",
        "Status":"FINISH",
        "ErrCode":0,
        "Message":"SUCCESS",
        "Input":{
            "InputType":"File",
            "FileInfoSet":[
                {
                    "FileId":"24961954183381008",
                    "StartTimeOffset":0,
                    "EndTimeOffset":0
                },
                {
                    "FileId":"24961954183381009",
                    "StartTimeOffset":0,
                    "EndTimeOffset":0
                },
                {
                    "FileId":"24961954183381010",
                    "StartTimeOffset":0,
                    "EndTimeOffset":0
                }
            ]
        },
        "Output":{
            "FileType":"mp4",
            "FileId":"24961954183923290",
            "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
        },
        "ProcedureTaskId":""
    }
}
```


### 신뢰할 수 있는 콜백
신뢰할 수 있는 콜백 모드를 선택하면 [PullEvents](/document/product/266/33433) API가 호출된 후 다음 형식의 HTTP 응답이 수신됩니다(null 값이 있는 필드는 생략됨).

```json
{
	"Response": {
		"EventSet": [
			{
				"EventHandle": "EventHandle.N",
				"EventType": "EditMediaComplete",
				"EditMediaCompleteEvent": {
        			"TaskId": "EditMedia-f5ac8127b3b6b85cdc13f237c6005d8",
        			"Status": "FINISH",
        			"ErrCode": 0,
        			"Message": "SUCCESS",
        			"Input":{
						"InputType": "File",
						"FileInfoSet": [
							{
								"FileId": "24961954183381008",
								"StartTimeOffset": 0,
								"EndTimeOffset": 0
							},
							{
								"FileId": "24961954183381009",
								"StartTimeOffset": 0,
								"EndTimeOffset": 0
							},
							{
								"FileId": "24961954183381010",
								"StartTimeOffset": 0,
								"EndTimeOffset": 0
							}
						]
					},
        			"Output":{
						"FileType": "mp4",
						"FileId": "24961954183923290",
						"FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
					},
        			"ProcedureTaskId": ""
				}
			}
		],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
	}
}
```
