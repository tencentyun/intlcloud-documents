>
>- このドキュメントは、バージョン3.0のコールバック用です。バージョン2.0のレガシーコールバックについては、[レガシーコールバック](https://intl.cloud.tencent.com/document/product/266/33962#CreateImageSpriteComplete)のドキュメントをご参照ください。
>- コールバックをバージョン3.0に徐々に移行することをお勧めします。バージョン2.0のコールバックドキュメントのメンテナンスは終了となります。

## イベント名
CreateImageSpriteComplete

## イベントの説明
Appがイベント通知で構成されている場合、かつスプライトイメージのキャプチャが完了した場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」を介してイベント通知を取得することができます。APIイベント通知の内容は、[CreateImageSpriteTask2017の構造](https://intl.cloud.tencent.com/document/product/266/34187#CreateImageSpriteTask2017)です。


## 通常のコールバック
通常のコールバックモードを選択すると、コールバックURLは次の形式のHTTPリクエストを受信します。
```json
{
    "EventType":"CreateImageSpriteComplete",
    "FileUploadEvent":null,
    "ProcedureStateChangeEvent":null,
    "FileDeleteEvent":null,
    "PullCompleteEvent":null,
    "EditMediaComplete":null,
    "WechatPublishComplete":null,
    "TranscodeCompleteEvent":null,
    "ConcatCompleteEvent":null,
    "ClipCompleteEvent":null,
    "CreateImageSpriteCompleteEvent":{
        "ErrCode":0,
        "Message":"",
        "TaskId":"CreateImageSprite-1edb7eb88a599d05abe451cfc541cfbd",
        "FileId":"14508071098244929440",
        "Definition":10,
        "TotalCount":106,
        "ImageSpriteUrlSet":[
            "http://125676836723.vod2.myqcloud.com/xxx/xxx/1.png",
            "http://125676836723.vod2.myqcloud.com/xxx/xxx/2.png"
        ],
        "WebVttUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.vtt"
    }
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
                "EventType":"CreateImageSpriteComplete",
                "FileUploadEvent":null,
                "ProcedureStateChangeEvent":null,
                "FileDeleteEvent":null,
                "PullCompleteEvent":null,
                "EditMediaComplete":null,
                "WechatPublishComplete":null,
                "TranscodeCompleteEvent":null,
                "ConcatCompleteEvent":null,
                "ClipCompleteEvent":null,
                "CreateImageSpriteCompleteEvent":{
                    "ErrCode":0,
                    "Message":"",
                    "TaskId":"CreateImageSprite-1edb7eb88a599d05abe451cfc541cfbd",
                    "FileId":"14508071098244929440",
                    "Definition":10,
                    "TotalCount":106,
                    "ImageSpriteUrlSet":[
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/1.png",
                        "http://125676836723.vod2.myqcloud.com/xxx/xxx/2.png"
                    ],
                    "WebVttUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.vtt"
                }
            }
        ],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
