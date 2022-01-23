워터마킹은 비디오 트랜스코딩 또는 화면 캡처 중에 비디오의 지정된 위치에 이미지 또는 텍스트를 추가하는 오프라인 작업입니다. VOD는 다음 유형의 워터마크를 지원합니다.
- 정적 이미지 워터마크: PNG 형식의 이미지 워터마크를 나타냅니다. 저작권 소유자 또는 TV 방송국 LOGO가 될 수 있으며 일반적으로 비디오 저작권 소유권을 나타내는 데 사용됩니다.
- 애니메이션 이미지 워터마크: 애니메이션이 가능한 APNG 형식의 이미지 워터마크를 나타냅니다.
- 텍스트 워터마크: 다국어 텍스트 워터마크를입니다. 사용자의 닉네임이 될 수 있으며 일반적으로 UGSV 콘텐츠 제작자를 식별하는 데 사용됩니다.

VOD는 동영상 또는 스크린샷에 여러 워터마크를 추가할 수 있습니다. 크기와 위치는 개별적으로 사용자 정의할 수 있습니다.

## <span id = "sy"></span>
워터마크 템플릿

워터마크의 대상 사양은 워터마크 유형, 너비, 높이 및 위치와 같은 매개변수의 영향을 받으며 아래와 같이 VOD 워터마킹 템플릿 형태로 사용자 정의할 수 있습니다.

| 매개변수                     | 설명                                                         |
| ------------------------ | ------------------------------------------------------------ |
| 워터마크 유형(Type)         | 이미지 및 텍스트 워터마크가 지원됩니다.:<li>이미지 워터마크: 정적 또는 애니메이션 이미지가 지원됩니다.</li><li>텍스트 워터마크: 다양한 언어의 텍스트가 지원됩니다.</li> |
| 워터마크 위치(Position)     | 동영상에서 워터마크의 상대적 위치입니다.                                 |
| 이미지 크기(ImageSize)    | 동영상의 워터마크 크기입니다.                                |
| 이미지 콘텐츠(ImageContent) | 워터마크의 이진법 콘텐츠입니다.                                 |
| 글꼴 크기(FontSize)     | 텍스트 워터마크의 글꼴 크기입니다.                                       |
| 글꼴 유형(FontType)     | 텍스트 워터마크의 글꼴입니다(예: Times New Roman).                         |
| 글꼴 색상(FontColor)    | 텍스트 워터마크의 색상입니다(예: 0xRRGGBB).                           |
| 글꼴 투명도(FontAlpha)  | 텍스트 워터마크의 투명도. 값 범위: 0 – 100%.                         |

콘솔을 사용하거나(자세한 내용은 [템플릿 설정](https://intl.cloud.tencent.com/document/product/266/14059#.E6.B0.B4.E5.8D.B0.E6.A8.A1.E6.9D.BF) 참고)) [서버 API](https://intl.cloud.tencent.com/document/product/266/34163)를 호출하여 사용자 지정 워터마킹 템플릿을 만들고 관리할 수 있습니다.

## 작업 시작

워터마크로 트랜스코딩 작업을 시작하는 방법에는 ‘서버 API를 통해 직접 시작하는 방법’, ‘콘솔을 통해 직접 시작하는 방법’, ‘업로드 시 작업을 지정하는 방법’이 있습니다. 자세한 내용은 비디오 처리를 위한 [작업 시작](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask)을 참고하십시오.

다음은 이러한 방식으로 워터마크를 사용하여 트랜스코딩 작업을 시작하기 위한 설명입니다.

* 서버 API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125)를 호출하여 작업 시작: 요청의 `MediaProcessTask.TranscodeTaskSet` 매개변수에 [워터마크 템플릿](#sy)의 템플릿 ID를 지정합니다.
* 콘솔을 통해 동영상 작업 시작: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 워터마크 사양을 설정하고, 태스크 플로우를 사용하여 [비디오 처리 시작](https://intl.cloud.tencent.com/document/product/266/33890)합니다.
* 서버에서 업로드 시 작업 지정: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 대상 워터마크 사양을 설정하고, 이 태스크 플로우를 [업로드 신청](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) 요청의 `procedure`로 지정합니다.
* 클라이언트에서 업로드할 때 작업 지정: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 대상 워터마크 사양을 설정하고, [클라이언트 업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0)에서 이 태스크 플로우를 `procedure` 매개변수로 지정합니다.
* 콘솔을 통해 업로드: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 대상 워터마크 사양을 설정하고, 콘솔을 통해 비디오를 업로드하고, [[업로드 중 비디오 처리]](https://intl.cloud.tencent.com/document/product/266/33890)를 선택하고, 동영상 업로드 완료 시 이 태스크 플로우를 실행하도록 지정합니다.

## 결과 가져오기

워터마크로 트랜스코딩 작업을 시작한 후 비동기식으로 [결과 알림](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification)을 기다리거나 동기식으로 [작업 쿼리](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery)를 수행하여 작업 실행 결과를 얻을 수 있습니다. 다음은 워터마크가 있는 트랜스코딩 작업이 시작된 후 일반 콜백 모드에서 결과 알림을 받는 예시입니다(null 값이 있는 필드는 생략됨).

```json
{
    "EventType":"ProcedureStateChanged",
    "ProcedureStateChangeEvent":{
        "TaskId":"1256768367-Procedure-2e1af2456351812be963e309cc133403t0",
        "Status":"FINISH",
        "FileId":"5285890784246869930",
        "FileName":"동물의 세계",
        "FileUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/AtUCmy6gmIYA.mp4",
        "MetaData":{
            "AudioDuration":60,
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
                    "Message":"",
                    "Input":{
                        "Definition":220,
                        "WatermarkSet": [
                            {
                                "Definition": 23120
                            }
                        ]
                    },
                    "Output":{
                        "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/v.f20.m3u8",
                        "Size":63120997,
                        "Container":"mov,mp4,m4a,3gp,3g2,mj2",
                        "Height":1086,
                        "Width":1920,
                        "Bitrate":513402,
                        "Md5":"084d403c73930ca2f835679af1f37bd3",
                        "Duration":60,
                        "VideoStreamSet":[
                            {
                                "Bitrate":473101,
                                "Codec":"h264",
                                "Fps":24,
                                "Height":480,
                                "Width":640
                            }
                        ],
                        "AudioStreamSet":[
                            {
                                "Bitrate":48581,
                                "Codec":"aac",
                                "SamplingRate":44100
                            }
                        ],
                        "Definition":220
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

콜백 결과에서 `ProcedureStateChangeEvent.MediaProcessResultSet`에는 `Transcode` `Type`의 트랜스코딩 결과가 포함됩니다. 트랜스코딩 사양 `Definition`은 220이고, 사양 `Definition`은 23120인 트랜스코딩 중에 워터마크가 추가됩니다.
