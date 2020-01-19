>
>- This document describes the callback on v3.0. For legacy callback on v2.0, please see [Legacy Callback](https://cloud.tencent.com/document/product/266/33796#ProcedureStateChanged).
>- You are recommended to gradually migrate the callback to v3.0, as the documentation for callback v2.0 will no longer be maintained.


## Event Name
ProcedureStateChanged

## Event Description

If the application is configured with event notification, after the status of a task flow changes, the application backend can get an event notification through "normal callback" or "reliable callback". The content of the event notification is the [`ProcedureTask` structure](https://cloud.tencent.com/document/api/266/31773#ProcedureTask).

## Samples
### Normal callback
If you choose the normal callback mode, the callback URL will receive an HTTP POST request from VOD, whose content is in the `BODY` as shown below (the fields with null value are omitted):

```json
{
    "EventType":"ProcedureStateChanged",
    "ProcedureStateChangeEvent":{
        "TaskId":"1256768367-Procedure-475b72xxxcb177t1",
        "Status":"FINISH",
        "ErrCode":0,
        "Message":"",
        "FileId":"5285890784246869930",
        "FileName":"Animal World",
        "FileUrl":"https://1256768367.vod2.myqcloud.com/xxx/xxx/xxx.mp4",
        "MetaData":{
            "AudioDuration":59.990001678467,
            "AudioStreamSet":[
                {
                    "Bitrate":383854,
                    "Codec":"aac",
                    "SamplingRate":48000
                }
            ],
            "Bitrate":1021028,
            "Container":"mov,mp4,m4a,3gp,3g2,mj2",
            "Duration":60,
            "Height":480,
            "Rotate":0,
            "Size":7700180,
            "VideoDuration":60,
            "VideoStreamSet":[
                {
                    "Bitrate":637174,
                    "Codec":"h264",
                    "Fps":23,
                    "Height":480,
                    "Width":640
                }
            ],
            "Width":640
        },
        "MediaProcessResultSet":[
            {
                "Type":"Transcode",
                "TranscodeTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"SUCCESS",
                    "Input":{
                        "Definition":20
                    },
                    "Output":{
                        "Url":"https://1256768367.vod2.myqcloud.com/xxx/xxx/v.f20.mp4",
                        "Size":4189073,
                        "Container":"mov,mp4,m4a,3gp,3g2,mj2",
                        "Height":480,
                        "Width":640,
                        "Bitrate":552218,
                        "Md5":"eff7031ad7877865f9a3240e9ab165ad",
                        "Duration":60.04700088501,
                        "VideoStreamSet":[
                            {
                                "Bitrate":503727,
                                "Codec":"h264",
                                "Fps":24,
                                "Height":480,
                                "Width":640
                            }
                        ],
                        "AudioStreamSet":[
                            {
                                "Bitrate":48491,
                                "Codec":"aac",
                                "SamplingRate":44100
                            }
                        ],
                        "Definition":0
                    }
                }
            },
            {
                "Type":"CoverBySnapshot",
                "CoverBySnapshotTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"SUCCESS",
                    "Input":{
                        "Definition":10,
                        "PositionType":"Time",
                        "PositionValue":0
                    },
                    "Output":{
                        "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx.100_0.jpg"
                    }
                }
            }
        ]
    }
}
```


### Reliable callback
If you choose the reliable callback mode, after the [PullEvents](/document/product/266/33433) API is called, an HTTP response in the following format will be received (the fields with null value are omitted).

```json
{
	"Response": {
		"EventSet": [
			{
				"EventHandle": "EventHandleX",
				"EventType": "ProcedureStateChanged",
				"ProcedureStateChangeEvent": {
					"TaskId": "1256768367-Procedure-475b72xxxcb177t1",
					"Status": "FINISH",
					"FileId": "5285890784246869930",
					"FileName": "Animal World",
					"FileUrl": "https://1256768367.vod2.myqcloud.com/xxx/xxx/xxx.mp4",
					"MetaData": {
						"AudioDuration": 59.990001678467,
						"AudioStreamSet": [{
							"Bitrate": 383854,
							"Codec": "aac",
							"SamplingRate": 48000
						}],
						"Bitrate": 1021028,
						"Container": "mov,mp4,m4a,3gp,3g2,mj2",
						"Duration": 60,
						"Height": 480,
						"Rotate": 0,
						"Size": 7700180,
						"VideoDuration": 60,
						"VideoStreamSet": [{
							"Bitrate": 637174,
							"Codec": "h264",
							"Fps": 23,
							"Height": 480,
							"Width": 640
						}],
						"Width": 640
					},
					"MediaProcessResultSet": [{
							"Type": "Transcode",
							"TranscodeTask": {
								"Status": "SUCCESS",
								"ErrCode": 0,
								"Message": "SUCCESS",
								"Input": {
									"Definition": 20
								},
								"Output": {
									"Url": "https://1256768367.vod2.myqcloud.com/xxx/xxx/v.f20.mp4",
									"Size": 4189073,
									"Container": "mov,mp4,m4a,3gp,3g2,mj2",
									"Height": 480,
									"Width": 640,
									"Bitrate": 552218,
									"Md5": "eff7031ad7877865f9a3240e9ab165ad",
									"Duration": 60.04700088501,
									"VideoStreamSet": [{
										"Bitrate": 503727,
										"Codec": "h264",
										"Fps": 24,
										"Height": 480,
										"Width": 640
									}],
									"AudioStreamSet": [{
										"Bitrate": 48491,
										"Codec": "aac",
										"SamplingRate": 44100
									}],
									"Definition": 0
								}
							}
						},
						{
							"Type": "CoverBySnapshot",
							"CoverBySnapshotTask": {
								"Status": "SUCCESS",
								"ErrCode": 0,
								"Message": "SUCCESS",
								"Input": {
									"Definition": 10,
									"PositionType": "Time",
									"PositionValue": 0
								},
								"Output": {
									"CoverUrl": "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx.100_0.jpg"
								}
							}
						}
					]
				}
			}
		],
		"RequestId": "335bdaa3-db0e-46ce-9946-51941d9cb0f5"
	}
}
```
