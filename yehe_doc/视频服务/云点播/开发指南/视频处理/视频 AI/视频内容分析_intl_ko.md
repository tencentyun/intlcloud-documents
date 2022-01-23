비디오 콘텐츠 분석은 AI를 통해 동영상 콘텐츠를 지능적으로 분석하는 오프라인 작업입니다. 동영상 플랫폼이 동영상을 정확하고 효율적으로 관리할 수 있도록 동영상 카테고리, 태그 지정 및 커버 생성에 대한 제안을 지능적으로 제공합니다.

비디오 콘텐츠 분석에는 다음 기능이 포함됩니다.

| 기능 이름 | 설명 |
| -- | -- |
| 스마트 카테고리 | 동영상 카테고리에 대한 제안을 제공합니다. 현재 다음과 같은 10개 이상의 카테고리가 있습니다. <br/>뉴스, 엔터테인먼트, 게임, 기술, 음식, 스포츠, 여행, 애니메이션, 댄스, 음악, 텔레비전 및 자동차 등. |
| 스마트 태그 | 동영상 태그에 대한 제안을 제공합니다. 현재 다음과 같은 3,000개가 넘는 태그가 있습니다. <br/>게임, 차량, 음악가, 경주차, 애완동물, 드럼, 자전거, 월드 오브 워크래프트, 컴퓨터, 학교 및 재킷 등.<br/>  |
| 스마트 커버 생성 | 동영상에서 하나 이상의 스크린샷을 캡처하여 커버로 추천합니다.  |
| 스마트 프레임별 태그 | 동영상 프레임별 태그에 대한 제안을 제공합니다. 현재 다음과 같은 1,000개가 넘는 태그가 있습니다. <br/>현대 무용, 수상 스포츠, 스테이크, 아기, 고양이, 일년생식물, 구축함, 만화, 잔디, 웨딩 드레스, 연회장 및 여권 등. |

<span id = "sh"></span>
## 비디오 콘텐츠 분석 템플릿

비디오 콘텐츠 분석 작업은 분석 매개변수의 영향을 받으며, 이는 아래와 같이 VOD 비디오 콘텐츠 분석 템플릿 형태로 표시될 수 있습니다.

- 스마트 카테고리 활성화 여부입니다.
- 스마트 태그 활성화 여부입니다.
- 스마트 커버 생성 활성화 여부입니다.
- 스마트 프레임별 태그 활성화 여부입니다.

일반적인 작업 조합을 위해 VOD는 [사전 설정된 비디오 콘텐츠 분석 템플릿](https://intl.cloud.tencent.com/document/product/266/33932#.E9.A2.84.E7.BD.AE.E8.A7.86.E9.A2.91.E5.86.85.E5.AE.B9.E5.88.86.E6.9E.90.E6.A8.A1.E6.9D.BF)을 제공합니다. <!-- 또한 [Server API](https://intl.cloud.tencent.com/document/product/266/34463)를 호출하여 맞춤형 비디오 콘텐츠 분석 템플릿을 생성하고 관리할 수도 있습니다.-->

## 작업 시작

비디오 콘텐츠 분석 작업을 시작하는 방법에는 ‘서버 API를 통한 직접 시작’, ‘콘솔을 통한 직접 시작’ 및 ‘업로드 시 실행할 작업 지정’의 세 가지 방법이 있습니다. 자세한 내용은 비디오 처리의 [작업 시작](https://intl.cloud.tencent.com/document/product/266/33931#OriginatingTask)을 참고하십시오.

다음은 비디오 콘텐츠 인식 작업을 시작하는 다양한 방식에 관한 설명입니다.

* 서버 API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125)를 호출하여 작업 시작: 요청의 ‘AiAnalysisTask’ 매개변수에 [비디오 콘텐츠 분석 템플릿](# sh)의 템플릿 ID를 지정합니다.
* 서버 API [ProcessMediaByUrl](https://intl.cloud.tencent.com/document/product/266/34123)를 호출하여 작업 시작: 요청의 ‘AiAnalysisTask’ 매개변수에 [비디오 콘텐츠 분석 템플릿](# sh)의 템플릿 ID를 지정합니다.
* 콘솔을 통해 동영상 작업 시작: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 만들고, 태스크 플로우에 비디오 콘텐츠 분석 작업을 설정(`MediaProcessTask.AiAnalysisTask`에서 지정)한 후, 콘솔에서의 [비디오 처리 시작](https://intl.cloud.tencent.com/document/product/266/33890)에 사용합니다.
* 서버 업로드 시 작업 지정: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 생성하고 태스크 플로우에 비디오 콘텐츠 분석(`MediaProcessTask.AiAnalysisTask`에서 지정) 작업을 구성한 뒤, [업로드 신청](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0)의 `procedure`를 이 태스크 플로우로 지정합니다.
* 클라이언트 업로드 시 작업 지정: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 생성하고 태스크 플로우에 비디오 콘텐츠 분석(`MediaProcessTask.AiAnalysisTask`에서 지정) 작업을 구성한 뒤, [클라이언트 업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922#.E7.AD.BE.E5.90.8D.E5.8F.82.E6.95.B0)의 `procedure`를 이 태스크 플로우로 지정합니다.
* 콘솔 업로드: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 생성하고, 태스크 플로우에 비디오 콘텐츠 분석 작업(`MediaProcessTask.AiAnalysisTask`에서 지정)을 구성합니다. 콘솔을 통해 동영상을 업로드한 뒤 [업로드 중 비디오 처리](https://intl.cloud.tencent.com/document/product/266/33890)을 선택하고 동영상 업로드 후 해당 태스크 플로우를 실행하도록 지정합니다.

## 결과 가져오기

비디오 콘텐츠 분석을 시작한 후 비동기화 방식으로 [결과 알림](https://intl.cloud.tencent.com/document/product/266/33931#ResultNotification)을 기다리거나 [작업 쿼리](https://intl.cloud.tencent.com/document/product/266/33931#TaskQuery)를 동기적으로 수행하여 비디오 콘텐츠 분석 작업의 실행 결과를 얻을 수 있습니다. 다음은 콘텐츠 분석 작업 시작 후 일반 콜백 방식으로 결과 알림을 받는 예시입니다(null 값이 있는 필드는 생략).

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
        "AiAnalysisResultSet":[
            {
                "Type":"Classification",
                "ClassificationTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "ClassificationSet":[
                            {
                                "Classification":"동물",
                                "Confidence":80
                            },
                            {
                                "Classification":"여행",
                                "Confidence":34
                            }
                        ]
                    }
                }
            },
            {
                "Type":"Cover",
                "CoverTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "CoverSet":[
                            {
                                "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx1.jpg",
                                "Confidence":79
                            },
                            {
                                "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx2.jpg",
                                "Confidence":70
                            },
                            {
                                "CoverUrl":"http://1256768367.vod2.myqcloud.com/xxx/xxx/xxx3.jpg",
                                "Confidence":66
                            }
                        ]
                    }
                }
            },
            {
                "Type":"Tag",
                "TagTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "TagSet":[
                            {
                                "Tag":"말",
                                "Confidence":34
                            },
                            {
                                "Tag":"새",
                                "Confidence":27
                            },
                            {
                                "Tag":"식물",
                                "Confidence":13
                            },
                            {
                                "Tag":"해변",
                                "Confidence":11
                            }
                        ]
                    }
                }
            }
        ],
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

콜백 결과에서 ‘ProcedureStateChangeEvent.AiAnalysisResultSet’에는 각각 스마트 카테고리, 스마트 커버 생성, 스마트 태그를 나타내는 ‘Type’인 ‘Classification’, ’Cover’, ‘Tag’ 분석 결과가 포함되어 있습니다.

* ‘Type’이 ‘Classification’인 결과에는 ‘Output.ClassificationSet’ 신뢰도가 가장 높은 카테고리는 `동물`이고 그 다음은 `여행`임을 보여줍니다.
* ‘Type’이 ‘Cover’인 결과 ‘Output.CoverSet’에는 3개의 권장 커버를 제공하며, ‘CoverUrl’은 해당 커버의 다운로드 주소입니다.
* ‘Type’이 ‘Tag’인 결과 ‘Output.TagSet’에는 신뢰도가 높은 순서대로 4개의 동영상 권장 태그를 제공합니다.
