화면 캡처는 특정 시점에서 비디오의 스크린샷을 캡처하는 오프라인 작업입니다. VOD는 다음과 같은 유형의 스크린샷을 제공합니다.
- 지정 시점 화면 캡처: 일정 시점을 지정하면 비디오의 해당 시점 화면을 캡처합니다.
- 샘플링 화면 캡처: 동일한 시간 간격으로 비디오의 여러 화면을 캡처합니다.
- 커버 스크린샷: VOD는 지정된 시점의 비디오 스크린샷을 캡처하고 해당 URL을 미디어 자산 관리 시스템의 비디오 커버로 사용할 수 있습니다.
- 이미지 스프라이트: VOD는 지정된 시간 간격으로 비디오(서브 이미지)의 스크린샷 세트를 캡처하고 함께 연결하여 큰 이미지(즉, 이미지 스프라이트)를 생성할 수 있습니다.

화면 캡처 기능은 다음 애플리케이션 시나리오 니즈를 충족할 수 있습니다.
- 동영상 커버 생성: 동영상의 스크린샷을 커버로 사용할 수 있습니다.
- 썸네일: 이미지 스프라이트는 일반적으로 비디오 개요를 나타내는 데 사용되는 여러 서브 이미지(즉, 썸네일)로 구성된 큰 이미지입니다.
- 재생 미리보기: VTT 파일과 함께 이미지 스프라이트를 사용하여 플레이어 진행률 표시줄에서 미리보기 효과를 얻을 수 있습니다.
<span id = "jt"></span>
## 화면 캡처 템플릿


스크린샷의 대상 규격은 스크린샷 파일 형식, 너비 및 높이와 같은 매개변수의 영향을 받으며 아래와 같이 VOD 화면 캡처 템플릿 형태로 사용자 정의할 수 있습니다.

### 시점 화면 캡처 템플릿

시점 화면 캡처 템플릿은 ‘지정된 시점의 스크린샷’을 찍거나 ‘스크린샷을 커버’로 찍을 때 사용합니다.

| 매개변수                     | 설명                                                         |
| -------------------- | ------------------------------------------------------------ |
| 포맷(Format)         | 화면 캡처 파일의 출력 포맷으로 현재 JPG만 지원.                         |
| 폭(Width)          | 캡처 화면의 폭으로 128px - 4096px까지 지원.                             |
| 높이(Height)       | 캡처 화면의 높이로 128px - 4096px까지 지원.                             |
| 채우기 방식(FillType) | 캡처 화면의 폭/높이 비율이 원본 비디오와 불일치할 경우, 캡처 화면을 '채우기' 방식으로 처리합니다. 일반적으로 다음과 같은 채우기 방식이 있습니다.<li>늘이기: 이미지를 늘려 이미지 전체를 채웁니다. 이미지가 '찌그러지거나' '길게 늘어날' 수 있습니다.</li><li>검은 테두리 남기기: 이미지의 폭/높이 비율을 유지하고 테두리의 남는 부분을 검은색으로 채웁니다.</li><li>흰 테두리 남기기: 이미지의 폭/높이 비율을 유지하고 테두리의 남는 부분을 흰색으로 채웁니다.</li><li>가우시안 블러: 이미지의 폭/높이 비율을 유지하고 테두리의 남는 부분을 가우시안 블러로 채웁니다.</li> |

VOD는 일반 규격에 대해 [사전 설정된 시점 화면 캡처 템플릿](https://intl.cloud.tencent.com/document/product/266/33932#screenshot01)을 제공합니다. 또한 콘솔에서 사용자 정의 화면 캡처 템플릿을 만들고 관리할 수도 있습니다. 자세한 내용은 [템플릿 설정](https://intl.cloud.tencent.com/document/product/266/14059#.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF)을 참고하십시오.

### 샘플링 화면 캡처 템플릿

샘플링된 스크린샷 캡처 템플릿은 샘플링된 스크린샷을 찍는 데 사용됩니다.

| 매개변수                   | 설명                                                         |
| ---------------------- | ------------------------------------------------------------ |
| 포맷(Format)         | 화면 캡처 파일의 출력 포맷으로 현재 JPG만 지원.                         |
| 폭(Width)          | 캡처 화면의 폭으로 128px - 4096px까지 지원.                             |
| 높이(Height)       | 캡처 화면의 높이로 128px - 4096px까지 지원.                             |
| 샘플링 방식(SampleType) | 샘플링 방식은 두 가지로 나뉩니다.<li>백분율로 샘플링: 5% 간격으로 샘플링할 경우 캡처 화면 20장 생성.</li><li>시간 간격으로 샘플링: 10s 간격으로 샘플링할 경우 캡처되는 화면 수는 비디오 길이에 따라 달라짐.</li> |
| 샘플링 간격(Interval)   | 샘플링 간격 길이: <li>백분율로 샘플링할 경우 간격은 백분율.</li><li>시간 간격으로 샘플링할 경우 간격은 초.</li> |
| 채우기 방식(FillType)   | 캡처 화면의 폭/높이 비율이 원본 비디오와 불일치할 경우, 캡처 화면을 '채우기' 방식으로 처리합니다. 일반적으로 다음과 같은 채우기 방식이 있습니다.<li>늘이기: 이미지를 늘려 이미지 전체를 채웁니다. 이미지가 '찌그러지거나' '길게 늘어날' 수 있습니다.</li><li>검은 테두리 남기기: 이미지의 폭/높이 비율을 유지하고 테두리의 남는 부분을 검은색으로 채웁니다.</li><li>흰 테두리 남기기: 이미지의 폭/높이 비율을 유지하고 테두리의 남는 부분을 흰색으로 채웁니다.</li><li>가우시안 블러: 이미지의 폭/높이 비율을 유지하고 테두리의 남는 부분을 가우시안 블러로 채웁니다.</li> |

VOD는 일반 규격에 대해 [사전 설정된 샘플 화면 캡처 템플릿](https://intl.cloud.tencent.com/document/product/266/33932#screenshot02)을 제공합니다. 또한 콘솔에서 사용자 정의 화면 캡처 템플릿을 만들고 관리할 수도 있습니다. 자세한 내용은 [템플릿 설정](https://intl.cloud.tencent.com/document/product/266/14059#.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF)을 참고하십시오.

### 스프라이트 이미지 템플릿

이미지 스프라이트 생성 템플릿은 스크린샷을 찍고 결합하여 ‘이미지 스프라이트를 생성’하는 데 사용됩니다.

| 매개변수                   | 설명                                       |
| ---------------------- | ------------------------------------------ |
| 포맷(Format)         | 스프라이트 이미지 파일의 출력 포맷으로 현재 JPG만 지원.     |
| 작은 이미지의 폭(Width)      | 스프라이트 이미지 내 작은 이미지의 폭.                       |
| 작은 이미지의 높이(Height)   | 스프라이트 이미지 내 작은 이미지의 높이.                       |
| 작은 이미지의 행 수(Rows)       | 큰 이미지 내 작은 이미지의 행 수.                 |
| 작은 이미지의 열 수(Columns)    | 큰 이미지 내 작은 이미지의 열 수.                  |
| 샘플링 방식(SampleType) | 작은 이미지의 샘플링 방식은 현재 시간 간격만 지원. |
| 샘플링 간격(Interval)   | 작은 이미지의 샘플링 간격은 작은 이미지를 샘플링하는 시간 간격을 의미.     |

>!
>- Width × Columns는 128px - 4096px 사이여야 합니다(큰 이미지의 폭은 128px - 4096px 사이).
>- Height × Rows는 128px - 4096px 사이여야 합니다(큰 이미지의 높이는 128px - 4096px 사이).

VOD는 일반 규격에 대해 [사전 설정된 이미지 스프라이트 생성 템플릿](https://intl.cloud.tencent.com/document/product/266/33932#screenshot03)을 제공하며, 콘솔에서 사용자 정의 화면 캡처 템플릿을 생성 및 관리할 수도 있습니다. 자세한 내용은 [템플릿 설정](https://intl.cloud.tencent.com/document/product/266/14059#.E6.88.AA.E5.9B.BE.E6.A8.A1.E6.9D.BF)을 참고하십시오.

## 작업 시작

화면 캡처 작업을 시작하는 방법에는 ‘서버 API를 통한 직접 시작’, ‘콘솔을 통한 직접 시작’ 및 ‘업로드 시 실행할 작업 지정’의 세 가지 방법이 있습니다. 자세한 내용은 비디오 처리의 [작업 시작](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask)을 참고하십시오.

다음은 이러한 방식으로 화면 캡처 작업을 시작하기 위한 내용입니다.

* 서버 API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125)를 호출하여 작업 시작: 요청의 `MediaProcessTask.SnapshotByTimeOffsetTaskSet` 매개변수에 [화면 캡처 템플릿](#jt)의 템플릿 ID를 지정합니다.
* 콘솔을 통해 비디오 작업 시작: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058)하고, 태스크 플로우에서 대상 스크린샷 사양을 설정한 후, 태스크 플로우를 사용하여 [비디오 처리 시작](https://intl.cloud.tencent.com/document/product/266/33890)합니다.
* 서버에서 업로드 시 작업 지정: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 대상 스크린샷 사양을 설정하고, 이 태스크 플로우를 [업로드 신청](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) 요청의 `procedure`로 지정합니다.
* 클라이언트에서 업로드할 때 작업 지정: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 대상 스크린샷 사양을 설정하고, [클라이언트에서 업로드하기 위한 서명](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0)에서 이 태스크 플로우를 `procedure` 매개변수로 지정합니다.
* 콘솔을 통해 업로드: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 대상 스크린샷 사양을 설정하고, 콘솔을 통해 비디오를 업로드한 다음, [업로드 중 비디오 처리](https://intl.cloud.tencent.com/document/product/266/33890#.E6.9C.AC.E5.9C.B0.E4.B8.8A.E4.BC.A0.E6.AD.A5.E9.AA.A4)를 선택하고, 비디오 업로드 완료 시 이 태스크 플로우를 실행하도록 지정합니다.

## 결과 가져오기

화면 캡처 작업을 시작한 후 비동기적으로 [결과 알림](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification)을 기다리거나 동기적으로 [작업 쿼리](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery)를 수행하여 작업 실행 결과를 얻을 수 있습니다. 다음은 화면 캡처 작업이 시작된 후 일반 콜백 모드에서 결과 알림을 받는 예시입니다(null 값이 있는 필드는 생략됨).

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
                "Type":"SnapshotByTimeOffset",
                "SnapshotByTimeOffsetTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10,
                        "Definition":[3, 6, 9]
                    },
                    "Output":{
                        "Definition":10,
                        "PicInfoSet": [
                            {
                                "TimeOffset":3,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg"
                            },
                            {
                                "TimeOffset":6,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx2.jpg"
                            },
                            {
                                "TimeOffset":9,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx3.jpg"
                            }
                        ]
                    }
                }
            },
            {
                "Type":"SampleSnapshot",
                "SampleSnapshotTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Definition":10,
                        "PicInfoSet": [
                            {
                                "TimeOffset":6,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg"
                            },
                            {
                                "TimeOffset":12,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx2.jpg"
                            },
                            {
                                "TimeOffset":18,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx3.jpg"
                            },
                            {
                                "TimeOffset":24,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx4.jpg"
                            },
                            {
                                "TimeOffset":30,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx5.jpg"
                            },
                            {
                                "TimeOffset":36,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx6.jpg"
                            },
                            {
                                "TimeOffset":42,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx7.jpg"
                            },
                            {
                                "TimeOffset":48,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx8.jpg"
                            },
                            {
                                "TimeOffset":54,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx9.jpg"
                            },
                            {
                                "TimeOffset":60,
                                "Url":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx10.jpg"
                            }
                        ]
                    }
                }
            },
            {
                "Type":"ImageSprites",
                "ImageSpriteTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Definition":10,
                        "Height":80,
                        "Width":142,
                        "TotalCount":1,
                        "ImageUrlSet":[
                            "http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg"
                        ],
                        "WebVttUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx.vtt"
                    }
                }
            },
            {
                "Type":"CoverBySnapshot",
                "CoverBySnapshotTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10,
                        "PositionType":"Time",
                        "PositionValue":0
                    },
                    "Output":{
                        "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx.jpg"
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

콜백 결과에서 `ProcedureStateChangeEvent.MediaProcessResultSet`에는 각각 시점 화면 캡처, 샘플링된 화면 캡처, 이미지 스프라이트 생성 및 커버 생성 작업을 나타내는 `SnapshotByTimeOffset`, `SampleSnapshot`, `ImageSprites` 및 `CoverBySnapshot`의 `Type` 결과가 포함됩니다.
