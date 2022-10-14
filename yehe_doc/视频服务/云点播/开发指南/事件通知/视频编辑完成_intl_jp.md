## イベント名
EditMediaComplete

## イベントの説明
Appがイベント通知で構成されている場合、かつビデオの編集が完了した場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」を介してイベント通知を取得することができます。APIイベント通知の内容は、[EditMediaTaskの構造](https://intl.cloud.tencent.com/document/product/266/34187#EditMediaTask)です。

## 事例
### 通常のコールバック
通常のコールバックモードを選択すると、コールバックURLはVODからのHTTPリクエストを受信します。リクエストはPOSTメソッドを使用します。リクエストの内容は、以下に示すようにBODYにあります（null値のフィールドは省略されています）。

```json
{
    "EventType":"EditMediaComplete",
    "EditMediaCompleteEvent":{
        "TaskId":"1256768367-EditMedia-f5ac8127b3b6b85cdc13f237c6005d8",
        "Status":"FINISH",
        "ErrCode":0,
        "Message":"SUCCESS",
        "Input":{
            "InputType":"File",
            "FileInfoSet":[
                {
                    "FileId":"24961954183381008",
                    "StartTimeOffset":0,
                    "EndTimeOffset":0
                },
                {
                    "FileId":"24961954183381009",
                    "StartTimeOffset":0,
                    "EndTimeOffset":0
                },
                {
                    "FileId":"24961954183381010",
                    "StartTimeOffset":0,
                    "EndTimeOffset":0
                }
            ]
        },
        "Output":{
            "FileType":"mp4",
            "FileId":"24961954183923290",
            "FileUrl":"http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
        },
        "ProcedureTaskId":""
    }
}
```


### 信頼できるコールバック
信頼できるコールバックモードを選択し、[プルイベント通知](https://www.tencentcloud.com/document/product/266/34183)APIが呼び出された後に、次の形式のHTTPレスポンスを受信します（null値のフィールドは省略されています）。

```json
{
	"Response": {
		"EventSet": [
			{
				"EventHandle": "EventHandle.N",
				"EventType": "EditMediaComplete",
				"EditMediaCompleteEvent": {
        			"TaskId": "EditMedia-f5ac8127b3b6b85cdc13f237c6005d8",
        			"Status": "FINISH",
        			"ErrCode": 0,
        			"Message": "SUCCESS",
        			"Input": {
						"InputType": "File",
						"FileInfoSet": [
							{
								"FileId": "24961954183381008",
								"StartTimeOffset": 0,
								"EndTimeOffset": 0
							},
							{
								"FileId": "24961954183381009",
								"StartTimeOffset": 0,
								"EndTimeOffset": 0
							},
							{
								"FileId": "24961954183381010",
								"StartTimeOffset": 0,
								"EndTimeOffset": 0
							}
						]
					},
        			"Output": {
						"FileType": "mp4",
						"FileId": "24961954183923290",
						"FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/f0.mp4"
					},
        			"ProcedureTaskId": ""
				}
			}
		],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
	}
}
```
