>
>- このドキュメントは、バージョン3.0のコールバック用です。バージョン2.0のレガシーコールバックについては、[レガシーコールバック](https://intl.cloud.tencent.com/document/product/266/33962#ClipComplete)のドキュメントをご参照ください。
>- コールバックをバージョン3.0に徐々に移行することをお勧めします。バージョン2.0のコールバックドキュメントのメンテナンスは終了となります。


## イベント名
ClipComplete

## イベントの説明
Appがイベント通知で構成されている場合、かつビデオトリミングが完了した場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」を介してイベント通知を取得することができます。APIイベント通知の内容は、[ClipTask2017の構造](https://intl.cloud.tencent.com/document/product/266/34187#ClipTask2017)です。


## 通常のコールバック
通常のコールバックモードを選択すると、コールバックURLは次の形式のHTTPリクエストを受信します。
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

## 信頼できるコールバック
信頼できるコールバックモードを選択し、[プルイベント通知](https://intl.cloud.tencent.com/document/product/266/34187) APIが呼び出された後に、次の形式のHTTPレスポンスを受信します。
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
