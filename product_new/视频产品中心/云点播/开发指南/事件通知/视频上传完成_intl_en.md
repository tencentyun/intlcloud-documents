>
>- This document describes the callback on v3.0. For legacy callback on v2.0, please see [Legacy Callback](https://cloud.tencent.com/document/product/266/33796#NewFileUpload).
>- You are recommended to gradually migrate the callback to v3.0, as the documentation for callback v2.0 will no longer be updated.

## Event Name
NewFileUpload

## Event Description
If the application is configured with event notification, after a video is uploaded from a client or server, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`FileUploadTask` structure](https://cloud.tencent.com/document/api/266/31773#FileUploadTask).



## Normal Callback v3.0
If you choose the normal callback mode, the callback URL will receive an HTTP POST request from VOD, whose content is in the `BODY` as shown below (the fields with null value are omitted):

```json
{
    "EventType":"NewFileUpload",
    "FileUploadEvent":{
        "FileId":"5285890784273533167",
        "MediaBasicInfo":{
            "Name":"Animal World",
            "Description":"",
            "CreateTime":"2019-01-09T16:36:22Z",
            "UpdateTime":"2019-01-09T16:36:24Z",
            "ExpireTime":"9999-12-31T23:59:59Z",
            "ClassId":0,
            "ClassName":"Other",
            "ClassPath":"Other",
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
        "ProcedureTaskId":""
    }
}
```
## Reliable Callback v3.0
If you choose the reliable callback mode, after the [PullEvents](/document/product/266/33433) API is called, an HTTP response in the following format will be received (the fields with null value are omitted).

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
						"Name": "Animal World",
						"Description": "",
						"CreateTime": "2019-01-09T16:36:22Z",
						"UpdateTime": "2019-01-09T16:36:24Z",
						"ExpireTime": "9999-12-31T23:59:59Z",
						"ClassId": 0,
						"ClassName": "Other",
						"ClassPath": "Other",
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
					"ProcedureTaskId": ""
				}
			}
		],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
	}
}
```





