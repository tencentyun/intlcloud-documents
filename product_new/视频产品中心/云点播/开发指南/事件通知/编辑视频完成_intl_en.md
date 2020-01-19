## Event Name
EditMediaComplete

## Event Description
If the application is configured with event notification, after a video is edited, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`EditMediaTask` structure](https://cloud.tencent.com/document/api/266/31773#EditMediaTask).

## Samples
### Normal Callback
If you choose the normal callback mode, the callback URL will receive an HTTP POST request from VOD, whose content is in the `BODY` as shown below (the fields with null value are omitted):

```json
{
    "EventType":"EditMediaComplete",
    "EditMediaComplete":{
        "TaskId":"EditMedia-f5ac8127b3b6b85cdc13f237c6005d8",
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


### Reliable Callback
If you choose the reliable callback mode, after the [PullEvents](/document/product/266/33433) API is called, an HTTP response in the following format will be received (the fields with null value are omitted).

```json
{
	"Response": {
		"EventSet": [
			{
				"EventHandle": "EventHandle.N",
				"EventType": "EditMediaComplete",
				"EditMediaComplete": {
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
