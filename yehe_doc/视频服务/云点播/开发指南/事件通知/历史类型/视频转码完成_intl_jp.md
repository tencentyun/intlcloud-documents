>!
>- このドキュメントは、バージョン3.0のコールバック用です。バージョン2.0のレガシーコールバックについては、[レガシーコールバック](https://intl.cloud.tencent.com/document/product/266/33962#TranscodeComplete)のドキュメントをご参照ください。
>- コールバックをバージョン3.0に徐々に移行することをお勧めします。バージョン2.0のコールバックドキュメントのメンテナンスは終了となります。

## イベント名
TranscodeComplete

## イベントの説明
Appがイベント通知で構成されている場合、かつビデオトランスコーディングが完了した場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」を介してイベント通知を取得することができます。APIイベント通知の内容は、[TranscodeTask2017の構造](https://intl.cloud.tencent.com/document/product/266/34187#TranscodeTask2017)です。


## 通常のコールバック
通常のコールバックモードを選択すると、コールバックURLは次の形式のHTTPリクエストを受信します。
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
        "FileName":"アニマルワールド",
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

## 信頼できるコールバック
信頼できるコールバックモードを選択し、[プルイベント通知](https://intl.cloud.tencent.com/document/product/266/34187) APIが呼び出された後に、次の形式のHTTPレスポンスを受信します。
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
                    "FileName":"アニマルワールド",
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
