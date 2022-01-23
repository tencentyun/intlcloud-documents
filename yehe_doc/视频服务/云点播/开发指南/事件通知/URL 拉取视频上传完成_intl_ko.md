>!
>- 본문에서는 v3.0의 콜백에 대해 설명합니다. v2.0의 레거시 콜백은 [레거시 콜백](https://intl.cloud.tencent.com/document/product/266/33962#url-.E6.8B.89.E5.8F.96.E8.A7.86.E9.A2.91.E4.B8.8A.E4.BC.A0.E5.AE.8C.E6.88.90)을 참고하십시오.
>- 콜백 v2.0에 대한 문서가 더 이상 업데이트되지 않으므로 콜백을 v3.0으로 점진적으로 마이그레이션하는 것이 좋습니다.

## 이벤트 이름
PullComplete

## 이벤트 설명
App에 이벤트 알림이 설정된 경우, 동영상 풀링 업로드가 완료된 후 App 백엔드는 ‘일반 콜백’ 또는 ‘신뢰할 수 있는 콜백’을 통해 이벤트 알림을 받을 수 있으며 이벤트 알림의 내용은 [PullComplete 구조](https://intl.cloud.tencent.com/document/product/266/34187#EventContent)입니다.


## 예시
### 일반 콜백
일반 콜백 모드를 선택하면 콜백 URL은 VOD에서 HTTP POST 요청을 수신하고 그 내용은 아래와 같이 BODY에 있습니다(null 값이 있는 필드는 생략됨).

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
            "FileId": "14508071098244959037", 
            "MediaBasicInfo": {
                "Name": "동물의 세계", 
                "Description": "", 
                "CreateTime": "2019-01-09T16:36:22Z", 
                "UpdateTime": "2019-01-09T16:36:24Z", 
                "ExpireTime": "9999-12-31T23:59:59Z", 
                "ClassId": 0, 
                "ClassName": "기타", 
                "ClassPath": "기타", 
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
            }
        }, 
        "FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4", 
        "ProcedureTaskId": "",
        "SessionContext": "",
        "SessionId": ""
    }
}
```

### 신뢰할 수 있는 콜백
신뢰할 수 있는 콜백 모드를 선택하면 [PullEvents](https://intl.cloud.tencent.com/document/product/266/34187) API가 호출된 후 다음 형식의 HTTP 응답이 수신됩니다(null 값이 있는 필드는 생략됨).

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
                        "FileId": "14508071098244959037", 
                        "MediaBasicInfo": {
                            "Name": "동물의 세계", 
                            "Description": "", 
                            "CreateTime": "2019-01-09T16:36:22Z", 
                            "UpdateTime": "2019-01-09T16:36:24Z", 
                            "ExpireTime": "9999-12-31T23:59:59Z", 
                            "ClassId": 0, 
                            "ClassName": "기타", 
                            "ClassPath": "기타", 
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
                        }
                    }, 
                    "FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4", 
                    "ProcedureTaskId": "",
                    "SessionContext": "",
                    "SessionId": ""
                }
            }
        ]
    }
}
```
