>!
>- 본문에서는 v3.0의 콜백에 대해 설명합니다. v2.0의 레거시 콜백은 [레거시 콜백](https://intl.cloud.tencent.com/document/product/266/33962#TranscodeComplete)을 참고하십시오.
>- 콜백 v2.0에 대한 문서가 더 이상 업데이트되지 않으므로 콜백을 v3.0으로 점진적으로 마이그레이션하는 것이 좋습니다.

## 이벤트 이름
TranscodeComplete

## 이벤트 설명
App에 이벤트 알림이 설정된 경우 동영상이 트랜스코딩된 후 App 백엔드는 ‘일반 콜백’ 또는 ‘신뢰할 수 있는 콜백’을 통해 이벤트 알림을 받을 수 있습니다. 이벤트 알림의 내용은 [TranscodeTask2017 구조](https://intl.cloud.tencent.com/document/product/266/34187#TranscodeTask2017)입니다.


## 일반 콜백
일반 콜백 모드를 선택하면 콜백 URL은 다음 형식의 HTTP 요청을 수신합니다.
```json
{
    "EventType":"TranscodeComplete",
    "FileUploadEvent":null,
    "ProcedureStateChangeEvent":null,
    "FileDeleteEvent":null,
    "PullCompleteEvent":null,
    "EditMediaComplete":null,
    "WechatPublishComplete":null,
    "TranscodeCompleteEvent":{
        "TaskId":"Transcode-f5ac8127b3b6b85cdc13f237c6005d8",
        "ErrCode":0,
        "Message":"SUCCESS",
        "FileId":"24961954183923290",
        "FileName":"동물의 세계",
        "Duration":599,
        "CoverUrl":"http://125676836723.vod2.myqcloud.com/0/xxx/640.jpg",
        "PlayInfoSet":[
            {
                "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                "Definition":0,
                "Bitrate":246000,
                "Height":480,
                "Width":640
            },
            {
                "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f10.mp4",
                "Definition":10,
                "Bitrate":149193,
                "Height":240,
                "Width":320
            },
            {
                "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f20.mp4",
                "Definition":20,
                "Bitrate":297656,
                "Height":480,
                "Width":640
            },
            {
                "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f30.mp4",
                "Definition":30,
                "Bitrate":899976,
                "Height":960,
                "Width":1280
            }
        ]
    },
    "ConcatCompleteEvent":null,
    "ClipCompleteEvent":null,
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
                "EventType":"TranscodeComplete",
                "FileUploadEvent":null,
                "ProcedureStateChangeEvent":null,
                "FileDeleteEvent":null,
                "PullCompleteEvent":null,
                "EditMediaComplete":null,
                "WechatPublishComplete":null,
                "TranscodeCompleteEvent":{
                    "TaskId":"Transcode-f5ac8127b3b6b85cdc13f237c6005d8",
                    "ErrCode":0,
                    "Message":"SUCCESS",
                    "FileId":"24961954183923290",
                    "FileName":"동물의 세계",
                    "Duration":599,
                    "CoverUrl":"http://125676836723.vod2.myqcloud.com/0/xxx/640.jpg",
                    "PlayInfoSet":[
                        {
                            "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                            "Definition":0,
                            "Bitrate":246000,
                            "Height":480,
                            "Width":640
                        },
                        {
                            "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f10.mp4",
                            "Definition":10,
                            "Bitrate":149193,
                            "Height":240,
                            "Width":320
                        },
                        {
                            "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f20.mp4",
                            "Definition":20,
                            "Bitrate":297656,
                            "Height":480,
                            "Width":640
                        },
                        {
                            "Url":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f30.mp4",
                            "Definition":30,
                            "Bitrate":899976,
                            "Height":960,
                            "Width":1280
                        }
                    ]
                },
                "ConcatCompleteEvent":null,
                "ClipCompleteEvent":null,
                "CreateImageSpriteCompleteEvent":null,
                "SnapshotByTimeOffsetCompleteEvent":null
            }
        ],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
