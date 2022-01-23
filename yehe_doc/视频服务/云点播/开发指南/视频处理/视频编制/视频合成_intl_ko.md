동영상 합성은 VOD의 동영상에 클리핑, 접합, 오버레이 및 뒤집기와 같은 일련의 복잡한 작업을 수행하는 오프라인 작업입니다. 다음과 같은 효과를 얻을 수 있습니다.

* **회전**: 비디오 또는 이미지를 특정 각도 또는 특정 방향으로 회전합니다.
* **오디오 제어**: 비디오/오디오의 사운드 볼륨을 조절하거나 동영상을 음소거합니다.
* **오버레이**: ‘PIP(Picture-in-Picture)’와 같은 효과를 얻기 위해 비디오/이미지를 순서대로 오버레이합니다.
* **오디오 믹싱**: 비디오/오디오의 사운드를 믹싱합니다.
* **오디오 추출**: 동영상에서 사운드를 추출합니다(화면 보관하지 않음).
* **클리핑**: 비디오/오디오 중 지정된 시간 내에 세그먼트를 클리핑합니다.
* **접합**: 비디오/오디오/이미지를 시간 순서대로 연결합니다.
* **전환**: 비디오 또는 이미지 접합 시 세그먼트 사이에 전환 효과를 추가합니다.

합성 후 미디어 파일의 컨테이너 형식은 MP4(비디오) 또는 MP3(오디오)입니다.

## 작업 시작

[서버 API](https://intl.cloud.tencent.com/document/product/266/34127)를 호출하여 동영상 합성 작업을 시작할 수 있습니다. API의 반환 결과에는 [결과 가져오기](#.E7.BB.93.E6.9E.9C.E8.8E.B7.E5.8F.96) 시 해당 작업 결과와 연결하는 데 사용되는 작업 ID가 포함됩니다.

## 결과 가져오기

작업을 시작한 후 비동기적으로 [결과 알림](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification)을 기다리거나 동기적으로 [작업 쿼리](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery)를 수행하여 작업 실행 결과를 얻을 수 있습니다. 다음은 동영상 합성 작업이 시작된 후 일반 콜백 모드에서 결과 알림을 받는 예시입니다(null 값이 있는 필드는 생략됨).

```json
{
	"EventType": "ComposeMediaComplete",
	"ComposeMediaCompleteEvent": {
		"TaskId": "ComposeMedia-f5ac8127b3b6b85cdc13f237c6005d8",
		"Status": "FINISH",
		"ErrCode": 0,
		"Message": "SUCCESS",
		"Input":{
			"Tracks": [{
					"Type": "Video",
					"TrackItems": [{
						"Type": "Video",
						"SourceMedia": "5285485487985271487",
						"AudioOperations": [{
							"Type": "Volume",
							"VolumeParam": {
								"Mute": 1
							}
						}]
					}]
				},
				{
					"Type": "Audio",
					"TrackItems": [{
							"Type": "Empty",
							"EmptyItem": {
								"Duration": 5
							}
						},
						{
							"Type": "Audio",
							"AudioItem": {
								"SourceMedia": "5285485487985271488",
								"Duration": 15
							}
						},
						{
							"Type": "Audio",
							"AudioItem": {
								"SourceMedia": "5285485487985271489",
								"SourceMediaStartTime": 2,
								"Duration": 14
							}
						}
					]
				}
			],
			"Output":{
				"FileName": "동영상 합성 효과 테스트",
				"Container": "mp4"
			}
		},
		"Output":{
			"FileType": "mp4",
			"FileId": 5285485487985271490,
			"FileUrl": "http://125676836723.vod2.myqcloud.com/xxx/xxx/xxx.mp4"
		}
	}
}
```

콜백 결과 중 `Input.Tracks`에는 `Type`의 두 요소인 Video 및 Audio가 포함되어 있는데, 이는 합성된 동영상에 비디오 트랙과 오디오 트랙이 포함되어 있음을 나타냅니다.
- 비디오 트랙: 소스 비디오의 ID는 5285485487985271487이며, 음소거되었습니다.
- 오디오 트랙: 5초의 묵음과 각각 15초 및 14초 동안 지속되는 2개의 음성 더빙을 포함합니다.

`Output.FileId`는 동영상 합성 후 생성된 새로운 동영상의 FileId이며, 재생 URL은 `FileUrl`의 값입니다.
