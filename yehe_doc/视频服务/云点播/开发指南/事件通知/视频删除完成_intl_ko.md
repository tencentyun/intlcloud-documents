>!
>- 본문에서는 v3.0의 콜백에 대해 설명합니다. v2.0의 레거시 콜백은 [레거시 콜백](https://intl.cloud.tencent.com/document/product/266/33962#.E8.A7.86.E9.A2.91.E5.88.A0.E9.99.A4.E5.AE.8C.E6.88.90)을 참고하십시오.
>- 콜백 v2.0에 대한 문서가 더 이상 업데이트되지 않으므로 콜백을 v3.0으로 점진적으로 마이그레이션하는 것이 좋습니다.

## 이벤트 이름
FileDeleted

## 이벤트 설명
App에 이벤트 알림이 설정된 경우 동영상이 삭제된 후 App 백엔드는 ‘일반 콜백’ 또는 ‘신뢰할 수 있는 콜백’을 통해 이벤트 알림을 받을 수 있습니다. 이벤트 알림의 내용은 [FileDeleteTask 구조](https://intl.cloud.tencent.com/document/product/266/34187#FileDeleteTask)입니다.


## 예시
### 일반 콜백
일반 콜백 모드를 선택하면 콜백 URL은 아래와 같이 BODY에 내용이 있는 VOD로부터 HTTP POST 요청을 수신합니다(null 값이 있는 필드는 생략됨).

```json
{
    "EventType":"FileDeleted",
    "FileDeleteEvent":{
        "FileIdSet":[
            "24961954183381008",
            "24961954183381009",
            "24961954183381010"
        ]
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
				"EventHandle": "EventHandle.N",
				"EventType": "FileDeleted",
				"FileDeleteEvent": {
                    "FileIdSet": [
                        "24961954183381008",
                        "24961954183381009",
                        "24961954183381010"
                    ]
                }
			}
		],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
	}
}
```
