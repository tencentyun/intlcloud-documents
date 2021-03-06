## イベント名
WechatPublishComplete

## イベントの説明
Appがイベント通知で構成されている場合、かつビデオがWeChatで公開が完了した場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」を介してイベント通知を取得することができます。APIイベント通知の内容は、[WechatPublishCompleteの構造](https://intl.cloud.tencent.com/document/product/266/34187#EventContent)です。

## 事例
### 通常のコールバック
通常のコールバックモードを選択すると、コールバックURLはVODからのHTTPリクエストを受信します。リクエストはPOSTメソッドを使用します。リクエストの内容は、以下に示すようにBODYにあります（null値のフィールドは省略されています）。

```json
{
    "EventType":"WechatPublishComplete",
    "WechatPublishComplete":{
        "TaskId":"Wechat-f5ac8127b3b6b85cdc13f237c6005d8",
        "Status":"FINISH",
        "ErrCode":0,
        "Message":"SUCCESS",
        "FileId":"24961954183381008",
        "Definition":10,
        "SourceDefinition":0,
        "WechatStatus":"SUCCESS",
        "WechatVid":"wechat-xxx-xxx",
        "WechatUrl":"http://xxx?xxx"
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
				"EventHandle": "EventHandle.N",
				"EventType": "WechatPublishComplete",
				"WechatPublishComplete": {
        			"TaskId": "Wechat-f5ac8127b3b6b85cdc13f237c6005d8",
        			"Status": "FINISH",
        			"ErrCode": 0,
        			"Message": "SUCCESS",
        			"FileId": "24961954183381008",
        			"Definition": 10,
        			"SourceDefinition": 0,
        			"WechatStatus": "SUCCESS",
        			"WechatVid": "wechat-xxx-xxx",
        			"WechatUrl": "http://xxx?xxx"
				}
			}
		],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
	}
}
```
