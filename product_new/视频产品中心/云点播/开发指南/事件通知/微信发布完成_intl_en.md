## Event Name
WechatPublishComplete

## Event Description
If the application is configured with event notification, after a video is published on WeChat, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`WechatPublishComplete` structure](#APIhttps://intl.cloud.tencent.com/document/api/266/31773#EventContent).

## Samples
### Normal Callback
If you choose the normal callback mode, the callback URL will receive an HTTP POST request from VOD, whose content is in the `BODY` as shown below (the fields with null value are omitted):

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

### Reliable Callback
If you choose the reliable callback mode, after the [PullEvents](#APIhttps://intl.cloud.tencent.com/document/api/266/31773) API is called, an HTTP response in the following format will be received (the fields with null value are omitted).

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
