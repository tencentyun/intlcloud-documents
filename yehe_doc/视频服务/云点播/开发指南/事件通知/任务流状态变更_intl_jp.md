>!
>- このドキュメントは、バージョン3.0のコールバック用です。バージョン2.0のレガシーコールバックについては、[レガシーコールバック](https://intl.cloud.tencent.com/document/product/266/33962#ProcedureStateChanged) のドキュメントをご参照ください。
>- コールバックをバージョン3.0に徐々に移行することをお勧めします。バージョン2.0のコールバックドキュメントのメンテナンスは終了となります。


## イベント名
ProcedureStateChanged

## イベントの説明

Appがイベント通知で構成されている場合、かつタスクフローのステータスが変更された場合、Appバックエンドは「通常のコールバック」または「信頼できるコールバック」を介してイベント通知を取得することができます。APIイベント通知の内容は、[ProcedureTaskの構造](https://intl.cloud.tencent.com/document/product/266/34187#ProcedureTask)です。

## 事例
### 通常のコールバック
通常のコールバックモードを選択すると、コールバックURLはVODからのHTTPリクエストを受信します。リクエストはPOSTメソッドを使用します。リクエストの内容は、以下に示すようにBODYにあります（null値のフィールドは省略されています）。

```json
{
    "EventType":"ProcedureStateChanged",
    "ProcedureStateChangeEvent":{
        "TaskId":"1256768367-Procedure-475b72xxxcb177t1",
        "Status":"FINISH",
        "ErrCode":0,
        "Message":"",
        "FileId":"5285890784246869930",
        "FileName":"アニマルワールド",
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


### 信頼できるコールバック
信頼できるコールバックモードを選択し、[プルイベント通知](https://intl.cloud.tencent.com/document/product/266/34187) APIが呼び出された後に、次の形式のHTTPレスポンスを受信します（null値のフィールドは省略されています）。

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
					"FileName":"アニマルワールド",
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
