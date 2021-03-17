>
>- このドキュメントは、バージョン3.0のコールバック用です。バージョン2.0のレガシーコールバックについては、[レガシーコールバック](https://intl.cloud.tencent.com/document/product/266/33962#ConcatComplete)のドキュメントをご参照ください。
>- コールバックをバージョン3.0に徐々に移行することをお勧めします。バージョン2.0のコールバックドキュメントのメンテナンスは終了となります。

## イベント名
ConcatComplete

## イベントの説明
Appがイベント通知で構成されている場合、かつビデオトランスコーディングが完了した場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」を介してイベント通知を取得することができます。APIイベント通知の内容は、[ConcatTask2017の構造](https://intl.cloud.tencent.com/document/product/266/34187#ConcatTask2017)です。


## 通常のコールバック
通常のコールバックモードを選択すると、コールバックURLは次の形式のHTTPリクエストを受信します。
```json
{
    "EventType":"ConcatComplete",
    "FileUploadEvent":null,
    "ProcedureStateChangeEvent":null,
    "FileDeleteEvent":null,
    "PullCompleteEvent":null,
    "EditMediaComplete":null,
    "WechatPublishComplete":null,
    "TranscodeCompleteEvent":null,
    "ConcatCompleteEvent":{
        "TaskId":"Concat-1edb7eb88a599d05abe451cfc541cfbd",
        "FileInfoSet":[
            {
                "ErrCode":0,
                "Message":"",
                "FileId":"14508071098244931831",
                "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/playlist.f6.m3u8",
                "FileType":"m3u8"
            },
            {
                "ErrCode":0,
                "Message":"",
                "FileId":"14508071098244929440",
                "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                "FileType":"mp4"
            }
        ]
    },
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
                "EventType":"ConcatComplete",
                "FileUploadEvent":null,
                "ProcedureStateChangeEvent":null,
                "FileDeleteEvent":null,
                "PullCompleteEvent":null,
                "EditMediaComplete":null,
                "WechatPublishComplete":null,
                "TranscodeCompleteEvent":null,
                "ConcatCompleteEvent":{
                    "TaskId":"Concat-1edb7eb88a599d05abe451cfc541cfbd",
                    "FileInfoSet":[
                        {
                            "ErrCode":0,
                            "Message":"",
                            "FileId":"14508071098244931831",
                            "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/playlist.f6.m3u8",
                            "FileType":"m3u8"
                        },
                        {
                            "ErrCode":0,
                            "Message":"",
                            "FileId":"14508071098244929440",
                            "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4",
                            "FileType":"mp4"
                        }
                    ]
                },
                "ClipCompleteEvent":null,
                "CreateImageSpriteCompleteEvent":null,
                "SnapshotByTimeOffsetCompleteEvent":null
            }
        ],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
