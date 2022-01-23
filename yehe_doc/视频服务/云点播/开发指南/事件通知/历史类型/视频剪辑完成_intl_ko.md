>？
>- 본문에서는 v3.0의 콜백에 대해 설명합니다. v2.0의 레거시 콜백은 [레거시 콜백](https://intl.cloud.tencent.com/document/product/266/33962#ClipComplete)을 참고하십시오.
>- 콜백 v2.0에 대한 문서가 더 이상 업데이트되지 않으므로 콜백을 v3.0으로 점진적으로 마이그레이션하는 것이 좋습니다.


## 이벤트 이름
ClipComplete

## 이벤트 설명
App에 이벤트 알림이 설정된 경우 비디오가 잘린 후 App 백엔드는 ‘일반 콜백’ 또는 ‘신뢰할 수 있는 콜백’을 통해 이벤트 알림을 받을 수 있습니다. 이벤트 알림의 내용은 [ClipTask2017  구조](https://intl.cloud.tencent.com/document/product/266/34187#ClipTask2017)입니다.


## 일반 콜백
일반 콜백 모드를 선택하면 콜백 URL은 다음 형식의 HTTP 요청을 수신합니다.
```json
{
    "EventType":"ClipComplete",
    "FileUploadEvent":null,
    "ProcedureStateChangeEvent":null,
    "FileDeleteEvent":null,
    "PullCompleteEvent":null,
    "EditMediaComplete":null,
    "WechatPublishComplete":null,
    "TranscodeCompleteEvent":null,
    "ConcatCompleteEvent":null,
    "ClipCompleteEvent":{
        "TaskId":"clipVideo-0a78cf44c4285026a4c",
        "SrcFileId":"16092504232103571364",
        "FileInfo":{
            "ErrCode":0,
            "Message":"",
            "FileId":"14508071098244929440",
            "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
            "FileType":"mp4"
        }
    },
    "CreateImageSpriteCompleteEvent":null,
    "SnapshotByTimeOffsetCompleteEvent":null
}
```

## 신뢰할 수 있는 콜백
신뢰할 수 있는 콜백 모드를 선택하면 [PullEvents](https://intl.cloud.tencent.com/document/product/266/34187) API가 호출된 후 다음 형식의 HTTP 응답이 수신됩니다.
```json
{
    "Response":{
        "EventSet":[
            {
                "EventHandle":"EventHandle.N",
                "EventType":"ClipComplete",
                "FileUploadEvent":null,
                "ProcedureStateChangeEvent":null,
                "FileDeleteEvent":null,
                "PullCompleteEvent":null,
                "EditMediaComplete":null,
                "WechatPublishComplete":null,
                "TranscodeCompleteEvent":null,
                "ConcatCompleteEvent":null,
                "ClipCompleteEvent":{
                    "TaskId":"clipVideo-0a78cf44c4285026a4c",
                    "SrcFileId":"16092504232103571364",
                    "FileInfo":{
                        "ErrCode":0,
                        "Message":"",
                        "FileId":"14508071098244929440",
                        "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                        "FileType":"mp4"
                    }
                },
                "CreateImageSpriteCompleteEvent":null,
                "SnapshotByTimeOffsetCompleteEvent":null
            }
        ],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
