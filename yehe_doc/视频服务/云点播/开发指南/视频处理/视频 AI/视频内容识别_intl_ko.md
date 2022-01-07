비디오 콘텐츠 인식은 AI를 이용하여 오프라인에서 동영상 콘텐츠를 지능적으로 식별하는 작업입니다. 비디오 콘텐츠 인식을 통해 동영상 화면의 얼굴, 텍스트, 오픈 크레딧과 엔딩 크레딧, 음성 텍스트를 식별할 수 있습니다. 비디오 콘텐츠 인식 결과에 따라 정확하고 효과적으로 동영상을 관리할 수 있습니다. 비디오 콘텐츠 인식에는 다음과 같은 기능이 포함됩니다.

| 기능 이름 | 기능 설명 | 적용 사례 |
| -- | -- | -- |
| Face Recognition | 화면 속 얼굴 인식 | <li>화면에서 스타가 나타나는 위치 표시</li><li>화면에 나타나는 관련 인물 인식</li>  |
| 음성 텍스트 전체 인식 | 음성에 나타나는 모든 텍스트 인식 | <li>강연 내용에 대한 자막 생성</li><li>동영상 음성 콘텐츠에 대한 데이터 분석 수행</li>  |
| 문자 텍스트 전체 인식 | 화면에 나타나는 모든 텍스트 인식 | 화면의 문자 텍스트에 대한 데이터 분석 수행  |
| 음성 키워드 인식 | 음성에 존재하는 키워드 인식 | <li>음성에서 민감한 단어 조사</li><li>음성에서 언급된 특정 키워드 검색</li>  |
| 문자 키워드 인식 | 화면에 존재하는 키워드 인식 | <li>화면에서 민감한 단어 조사</li><li>화면에 나타나는 특정 키워드 검색</li>  |
| 동영상 오프닝 크레딧과 엔딩 크레딧 인식 | 동영상의 오프닝 크레딧과 엔딩 크레딧 인식 | <li>프로그래스 바에서 오프닝 크레딧, 엔딩 크레딧 및 본편 위치를 표시</li><li>동영상에서 불필요한 부분 일괄 처리</li> |


부분 콘텐츠 인식 기능은 공용 라이브러리와 사용자 정의 라이브러리 두 가지 소재 라이브러리를 기반으로 합니다.

* 공용 라이브러리: VOD 사전 설정한 소재 라이브러리.
* 사용자 정의 라이브러리: 사용자가 자체 생성 및 관리하는 소재 라이브러리.

| 인식 유형 | 공용 라이브러리 | 사용자 정의 라이브러리 |
| -- | -- | -- |
| Face Recognition | 지원. 주로 연예인, 스포츠 스타 및 관련 인물 | 지원. [서버 API](https://intl.cloud.tencent.com/document/product/266/37584)를 호출하여 사용자 정의 얼굴 라이브러리 관리 |
| 음성 단어 인식 | 미지원| 지원. [서버 API](https://intl.cloud.tencent.com/document/product/266/37583)를 호출하여 키워드 라이브러리 관리 |
| 문자 단어 인식 | 미지원| 지원. [서버 API](https://intl.cloud.tencent.com/document/product/266/37583)를 호출하여 키워드 라이브러리 관리 |

[](id:sh)
## 비디오 콘텐츠 인식 템플릿

비디오 콘텐츠 인식에는 여러 인식 기능이 통합되어 있어 매개변수를 통한 정밀한 제어가 필요하며, 제어 타깃은 다음과 같습니다.

* 활성화된 인식 유형: 콘텐츠 인식에서 활성화된 기능들.
* 사용된 소재 라이브러리: 얼굴 인식에 공용 라이브러리 또는 사용자 정의 라이브러리 사용 여부.
* 필터링 점수 지정: 결과가 반환되는 얼굴 인식의 신뢰도 점수.
* 필터링 태그 지정: 결과가 반환되는 얼굴 태그의 범위.

일반적인 작업 조합을 위해 VOD는 [사전 설정된 비디오 콘텐츠 인식 템플릿](https://intl.cloud.tencent.com/document/product/266/33932)을 제공합니다. 또한 [서버 API](https://intl.cloud.tencent.com/document/product/266/37568)를 호출하여 맞춤형 비디오 콘텐츠 인식 템플릿을 생성 및 관리할 수 있습니다.

## 작업 시작

비디오 콘텐츠 인식 작업을 시작하는 방법에는 ‘서버 API를 통한 직접 시작’, ‘콘솔을 통한 직접 시작’ 및 ‘업로드 시 실행할 작업 지정’의 세 가지 방법이 있습니다. 자세한 내용은 비디오 처리의 [작업 시작](https://intl.cloud.tencent.com/document/product/266/33931)을 참고하십시오.

다음은 비디오 콘텐츠 인식을 시작하는 다양한 방식에 관한 설명입니다.

* 서버 API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125)를 호출하여 작업 시작: 요청의 `AiRecognitionTask` 매개변수에 [비디오 콘텐츠 인식 템플릿](#sh)의 템플릿 ID를 지정합니다.
* 서버 API [ProcessMediaByUrl](https://intl.cloud.tencent.com/document/product/266/34123)를 호출하여 작업 시작: 요청의 `AiRecognitionTask` 매개변수에 [비디오 콘텐츠 인식 템플릿](#sh)의 템플릿 ID를 지정합니다.
* 콘솔을 통해 동영상에 대한 작업 시작: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 생성하고, 태스크 플로우에 비디오 콘텐츠 인식 작업(`MediaProcessTask.AiRecognitionTask`에서 지정)을 구성한 뒤, 콘솔에서 태스크 플로우를 사용하여 [비디오 처리 시작](https://intl.cloud.tencent.com/document/product/266/33892)을 진행합니다.
* 서버 업로드 시 작업 지정: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 생성하고 태스크 플로우에 비디오 콘텐츠 인식(`MediaProcessTask.AiRecognitionTask`에서 지정) 작업을 구성한 뒤, [업로드 신청](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0)의 `procedure`를 이 태스크 플로우로 지정합니다.
* 클라이언트 업로드 시 작업 지정: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 생성하고 태스크 플로우에 비디오 콘텐츠 인식(`MediaProcessTask.AiRecognitionTask`에서 지정) 작업을 구성한 뒤, [클라이언트 업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922)의 `procedure`를 이 태스크 플로우로 지정합니다.
* 콘솔 업로드: [서버 API](https://intl.cloud.tencent.com/document/product/266/34167)를 호출하여 태스크 플로우를 생성하고, 태스크 플로우에 비디오 콘텐츠 인식 작업(`MediaProcessTask.AiRecognitionTask`에서 지정)을 구성합니다. 콘솔을 통해 비디오를 업로드한 뒤 [업로드 중 비디오 처리](https://intl.cloud.tencent.com/document/product/266/33890)을 선택하고 동영상 업로드 후 이 태스크 플로우를 실행하도록 지정합니다.

## 결과 가져오기

비디오 콘텐츠 인식을 시작한 후 비동기화 방식으로 [결과 알림](https://intl.cloud.tencent.com/document/product/266/33931)을 비동기적으로 기다리거나 [작업 쿼리](https://intl.cloud.tencent.com/document/product/266/33931)를 동기적으로 수행하여 작업 실행 결과를 얻을 수 있습니다. 다음은 비디오 콘텐츠 스마트 인식 작업이 시작된 후 일반 콜백 방식으로 결과 알림을 받는 예시입니다(null 값이 있는 필드는 생략).

```json
{
    "EventType":"ProcedureStateChanged",
    "ProcedureStateChangeEvent":{
        "TaskId":"1400155958-Procedure-2e1af2456351812be963e309cc133403t0",
        "Status":"FINISH",
        "FileId":"5285890784363430543",
        "FileName":"컬렉션",
        "FileUrl":"http://1400155958.vod2.myqcloud.com/xxx/xxx/aHjWUx5Xo1EA.mp4",
        "MetaData":{
            "AudioDuration":243,
            "AudioStreamSet":[
                {
                    "Bitrate":125599,
                    "Codec":"aac",
                    "SamplingRate":48000
                }
            ],
            "Bitrate":1459299,
            "Container":"mov,mp4,m4a,3gp,3g2,mj2",
            "Duration":243,
            "Height":1080,
            "Rotate":0,
            "Size":44583593,
            "VideoDuration":243,
            "VideoStreamSet":[
                {
                    "Bitrate":1333700,
                    "Codec":"h264",
                    "Fps":29,
                    "Height":1080,
                    "Width":1920
                }
            ],
            "Width":1920
        },
        "AiRecognitionResultSet":[
            {
                "Type":"FaceRecognition",
                "FaceRecognitionTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "ResultSet":[
                            {
                                "Id":183213,
                                "Type":"Default",
                                "Name":"홍길동",
                                "SegmentSet":[
                                    {
                                        "StartTimeOffset":10,
                                        "EndTimeOffset":12,
                                        "Confidence":97,
                                        "AreaCoordSet":[
                                            830,
                                            783,
                                            1030,
                                            599
                                        ]
                                    },
                                    {
                                        "StartTimeOffset":12,
                                        "EndTimeOffset":14,
                                        "Confidence":97,
                                        "AreaCoordSet":[
                                            844,
                                            791,
                                            1040,
                                            614
                                        ]
                                    }
                                ]
                            },
                            {
                                "Id":236099,
                                "Type":"Default",
                                "Name":"심청이",
                                "SegmentSet":[
                                    {
                                        "StartTimeOffset":120,
                                        "EndTimeOffset":122,
                                        "Confidence":96,
                                        "AreaCoordSet":[
                                            579,
                                            903,
                                            812,
                                            730
                                        ]
                                    }
                                ]
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

콜백 결과 중 `ProcedureStateChangeEvent.AiRecognitionResultSet`에 `Type`이 `FaceRecognition`인 인식 결과가 있으며, 안면 인식을 나타냅니다.

`Type`이 `FaceRecognition`인 결과는 `Output.ResultSet`에 ‘홍길동’과 ‘심청이’라는 두 명의 인물 인식 결과가 포함되어 있음을 의미합니다. `SegmentSet`는 비디오에 얼굴이 나오는 시간대(`StartTimeOffset`와 `EndTimeOffset`으로 결정)와 화면의 좌표(`AreaCoordSet`로 결정)가 인식되었음을 나타냅니다.


