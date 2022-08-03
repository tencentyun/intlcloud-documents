>!
>- このドキュメントは、バージョン3.0のコールバック用です。バージョン2.0のレガシーコールバックについては、[レガシーコールバック](https://intl.cloud.tencent.com/document/product/266/33962#.E8.A7.86.E9.A2.91.E5.88.A0.E9.99.A4.E5.AE.8C.E6.88.90)のドキュメントをご参照ください。
>- コールバックをバージョン3.0に徐々に移行することをお勧めします。バージョン2.0のコールバックドキュメントのメンテナンスは終了となります。

## イベント名
FileDeleted

## イベントの説明
Appがイベント通知で構成されている場合、かつビデオを削除した場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」を介してイベント通知を取得することができます。APIイベント通知の内容は、[FileDeleteTaskの構造](https://intl.cloud.tencent.com/document/product/266/34187#FileDeleteTask)です。


## 事例
### 通常のコールバック
通常のコールバックモードを選択すると、コールバックURLはVODからのHTTPリクエストを受信します。リクエストはPOSTメソッドを使用します。リクエストの内容は、以下に示すようにBODYにあります（null値のフィールドは省略されています）。

```json
{
    "EventType":"FileDeleted",
    "FileDeleteEvent":{
        "FileIdSet":[
            "24961954183381008"
        ],
        "FileDeleteResultInfo":[
            {
                "FileId":"24961954183381008",
                "DeleteParts":[
                    {
                        "Type":"TranscodeFiles",
                        "Definition":0
                    }
                ]
            }
        ]
    }
}
```


### 信頼できるコールバック
信頼できるコールバックモードを選択し、[プルイベント通知](https://intl.cloud.tencent.com/document/product/266/34187) APIが呼び出された後に、次の形式のHTTPレスポンスを受信します（null値のフィールドは省略されています）。


```json
{
    "Response":{
        "EventSet":[
            {
                "EventHandle":"EventHandle.N",
                "EventType":"FileDeleted",
                "FileDeleteEvent":{
                    "FileIdSet":[
                        "24961954183381008"
                    ],
                    "FileDeleteResultInfo":[
                        {
                            "FileId":"24961954183381008",
                            "DeleteParts":[
                                {
                                    "Type":"TranscodeFiles",
                                    "Definition":0
                                }
                            ]
                        }
                    ]
                }
            }
        ],
        "RequestId":"335bdaa3-db0e-46ce-9946-51941d9cb0f5"
    }
}
```
