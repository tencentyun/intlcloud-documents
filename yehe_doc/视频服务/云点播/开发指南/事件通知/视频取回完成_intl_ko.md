## 이벤트 이름
RestoreMediaComplete

## 이벤트 설명
App에 이벤트 알림이 설정된 경우, 아카이브 또는 딥 아카이브 미디어 파일의 동결 해제 또는 검색 후, App 백엔드는 ‘일반 콜백’ 또는 ‘신뢰할 수 있는 콜백’을 통해 이벤트 알림을 받을 수 있습니다. 이벤트 알림의 내용은 [RestoreMediaTask 구조](https://intl.cloud.tencent.com/document/product/266/34187)입니다.


## 예시
### 일반 콜백3.0
일반 콜백 모드를 선택하면 콜백 URL은 다음 형식의 HTTP 요청을 수신합니다.

```json
{
    "EventType":"RestoreMediaComplete",
    "RestoreMediaCompleteEvent":{
        "FileId":"24961954183381008",
        "OriginalStorageClass":"ARCHIVE",
        "TargetStorageClass":"STANDARD",
        "RestoreTier":"Standard",
        "RestoreDay":0,
        "Status":0,
        "Message":"Restore success!"
    }
}
```
### 신뢰할 수 있는 콜백3.0
신뢰할 수 있는 콜백 모드를 선택하면 [PullEvents](https://intl.cloud.tencent.com/document/product/266/34183) API가 호출된 후 다음 형식의 HTTP 응답이 수신됩니다.

```json
{
    "Response":{
        "EventSet":[
            {
                "EventHandle":"EventHandle.N",
                "EventType":"RestoreMediaComplete",
                "RestoreMediaCompleteEvent":{
                    "FileId":"24961954183381008",
                    "OriginalStorageClass":"ARCHIVE",
                    "TargetStorageClass":"STANDARD",
                    "RestoreTier":"Standard",
                    "RestoreDay":0,
                    "Status":0,
                    "Message":"Restore success!"
                }
            }
        ],
        "RequestId":"335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
