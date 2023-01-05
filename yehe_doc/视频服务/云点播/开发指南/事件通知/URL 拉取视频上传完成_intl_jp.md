>!
>- このドキュメントは、バージョン3.0のコールバック用です。バージョン2.0のレガシーコールバックについては、[レガシーコールバック](https://intl.cloud.tencent.com/document/product/266/33962#url-.E6.8B.89.E5.8F.96.E8.A7.86.E9.A2.91.E4.B8.8A.E4.BC.A0.E5.AE.8C.E6.88.90)のドキュメントをご参照ください。
>- コールバックをバージョン3.0に徐々に移行することをお勧めします。バージョン2.0のコールバックドキュメントのメンテナンスは終了となります。

## イベント名
PullComplete

## イベントの説明
Appがイベント通知で構成されている場合、かつビデオのプルアップロードが完了した場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」を介してイベント通知を取得することができます。APIイベント通知の内容は、[PullCompleteの構造](https://intl.cloud.tencent.com/document/product/266/34187#EventContent)です。


## 事例
### 通常のコールバック
通常のコールバックモードを選択すると、コールバックURLはVODからのHTTPリクエストを受信します。リクエストはPOSTメソッドを使用します。リクエストの内容は、以下に示すようにBODYにあります（null値のフィールドは省略されています）。

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
                "Name": "アニマルワールド", 
                "Description": "", 
                "CreateTime": "2019-01-09T16:36:22Z", 
                "UpdateTime": "2019-01-09T16:36:24Z", 
                "ExpireTime": "9999-12-31T23:59:59Z", 
                "ClassId": 0, 
                "ClassName": "その他", 
                "ClassPath": "その他", 
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
        }, 
        "FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4", 
        "ProcedureTaskId": "",
        "ReviewAudioVideoTaskId":"",
        "SessionContext": "",
        "SessionId": ""
    }
}
```

### 信頼できるコールバック
信頼できるコールバックモードを選択し、[プルイベント通知](https://intl.cloud.tencent.com/document/product/266/34187) APIが呼び出された後に、次の形式のHTTPレスポンスを受信します（null値のフィールドは省略されています）。

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
                            "Name": "アニマルワールド", 
                            "Description": "", 
                            "CreateTime": "2019-01-09T16:36:22Z", 
                            "UpdateTime": "2019-01-09T16:36:24Z", 
                            "ExpireTime": "9999-12-31T23:59:59Z", 
                            "ClassId": 0, 
                            "ClassName": "その他", 
                            "ClassPath": "その他", 
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
                    }, 
                    "FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4", 
                    "ProcedureTaskId": "",
                    "ReviewAudioVideoTaskId":"",
                    "SessionContext": "",
                    "SessionId": ""
                }
            }
        ]
    }
}
```
