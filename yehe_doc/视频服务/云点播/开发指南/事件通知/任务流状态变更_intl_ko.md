>!
>- 본문에서는 v3.0의 콜백에 대해 설명합니다. v2.0의 레거시 콜백은 [레거시 콜백](https://intl.cloud.tencent.com/document/product/266/33962#ProcedureStateChanged)을 참고하십시오.
>- 콜백 v2.0에 대한 문서가 더 이상 업데이트되지 않으므로 콜백을 v3.0으로 점진적으로 마이그레이션하는 것이 좋습니다.


## 이벤트 이름
ProcedureStateChanged

## 이벤트 설명

App에 이벤트 알림이 설정된 경우 태스크 플로우의 상태가 변경된 후 App 백엔드는 ‘일반 콜백’ 또는 ‘신뢰할 수 있는 콜백’을 통해 이벤트 알림을 받을 수 있습니다. 이벤트 알림의 내용은 [ProcedureTask 구조](https://intl.cloud.tencent.com/document/product/266/34187#ProcedureTask)입니다.

## 예시
### 일반 콜백
일반 콜백 모드를 선택하면 콜백 URL은 아래와 같이 BODY에 내용이 있는 VOD로부터 HTTP POST 요청을 수신합니다(null 값이 있는 필드는 생략됨).

```json
{
    "EventType":"ProcedureStateChanged",
    "ProcedureStateChangeEvent":{
        "TaskId":"1256768367-Procedure-475b72xxxcb177t1",
        "Status":"FINISH",
        "ErrCode":0,
        "Message":"",
        "FileId":"5285890784246869930",
        "FileName":"동물의 세계",
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


### 신뢰할 수 있는 콜백
신뢰할 수 있는 콜백 모드를 선택하면 [PullEvents](https://intl.cloud.tencent.com/document/product/266/34187) API가 호출된 후 다음 형식의 HTTP 응답이 수신됩니다(null 값이 있는 필드는 생략됨).

```json
{
	"Response": {
		"EventSet": [
			{
				"EventHandle": "EventHandleX",
				"EventType": "ProcedureStateChanged",
				"ProcedureStateChangeEvent":{
					"TaskId": "1256768367-Procedure-475b72xxxcb177t1",
					"Status": "FINISH",
					"FileId": "5285890784246869930",
					"FileName": "동물의 세계",
					"FileUrl": "https://1256768367.vod2.myqcloud.com/xxx/xxx/xxx.mp4",
					"MetaData":{
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
								"Input":{
									"Definition": 20
								},
								"Output":{
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
								"Input":{
									"Definition": 10,
									"PositionType": "Time",
									"PositionValue": 0
								},
								"Output":{
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
