>!
>- このドキュメントは、バージョン3.0のコールバック用です。バージョン2.0のレガシーコールバックについては、[レガシーコールバック](https://intl.cloud.tencent.com/document/product/266/33962#NewFileUpload) のドキュメントをご参照ください。
>- コールバックをバージョン3.0に徐々に移行することをお勧めします。バージョン2.0のコールバックドキュメントのメンテナンスは終了となります。

## イベント名
NewFileUpload

## イベントの説明
Appがイベント通知で構成されている場合、かつビデオをクライアントまたはサーバーからアップロードした場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」を介してイベント通知を取得することができます。APIイベント通知の内容は、[FileUploadTaskの構造](https://intl.cloud.tencent.com/document/product/266/34187#FileUploadTask)です。



## 通常のコールバック3.0
通常のコールバックモードを選択すると、コールバックURLはVODからのHTTPリクエストを受信します。リクエストはPOSTメソッドを使用します。リクエストの内容は、以下に示すようにBODYにあります（null値のフィールドは省略されています）。

```json
{
    "EventType":"NewFileUpload",
    "FileUploadEvent":{
        "FileId":"5285890784273533167",
        "MediaBasicInfo":{
            "Name":"アニマルワールド",
            "Description":"",
            "CreateTime":"2019-01-09T16:36:22Z",
            "UpdateTime":"2019-01-09T16:36:24Z",
            "ExpireTime":"9999-12-31T23:59:59Z",
            "ClassId":0,
            "ClassName":"その他",
            "ClassPath":"その他",
            "CoverUrl":"",
            "Type":"mp4",
            "MediaUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/q1BORBPQH1IA.mp4",
            "TagSet":[

            ],
            "StorageRegion":"ap-guangzhou-2",
            "SourceInfo":{
                "SourceType":"Upload",
                "SourceContext":""
            },
            "Vid":"5285890784273533167"
        },
        "ProcedureTaskId":"",
        "ReviewAudioVideoTaskId":""
    }
}
```
## 信頼できるコールバック3.0
信頼できるコールバックモードを選択し、[プルイベント通知](https://intl.cloud.tencent.com/document/product/266/34187) APIが呼び出された後に、次の形式のHTTPレスポンスを受信します（null値のフィールドは省略されています）。

```json
{
	"Response": {
		"EventSet": [
			{
				"EventHandle": "EventHandle.N",
				"EventType": "NewFileUpload",
				"FileUploadEvent": {
					"FileId": "5285890784273533167",
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
						"MediaUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/q1BORBPQH1IA.mp4",
						"TagSet": [],
						"StorageRegion": "ap-guangzhou-2",
						"SourceInfo": {
							"SourceType": "Upload",
							"SourceContext": ""
						},
						"Vid": "5285890784273533167"
					},
					"ProcedureTaskId": "",
					"ReviewAudioVideoTaskId":""
				}
			}
		],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
	}
}
```





