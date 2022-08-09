비디오 콘텐츠 스마트 식별은 AI를 활용해 동영상 콘텐츠를 지능적으로 식별하는 기능입니다. 비디오에 대한 콘텐츠 스마트 식별 작업을 수행한 후 실행 결과에는 스마트 식별 점수, 스마트 식별 제안 및 의심되는 비디오 클립이 포함됩니다. 결과의 ‘스마트 식별 제안’을 기반으로 비디오 공개 여부를 결정하여 친환경적이고 건강한 소셜 네트워크 환경을 구축할 수 있습니다.

## 분석 결과
비디오 콘텐츠 스마트 식별은 영상 화면, ASR 텍스트 및 OCR 텍스트의 세 가지 유형의 객체를 식별할 수 있습니다. 자세한 내용은 아래 표와 같습니다.

<table>
<tr>
<th style="text-align:center">객체</th><th >작업</th><th>설명</th>
</tr><tr>
<td rowspan=4 style="text-align:center">영상 화면<br>(사람과 물건)</td>
</tr><tr>
<td>포르노 정보</td>
<td>영상 화면에서 다음을 포함한 포르노 정보를 확인합니다.
    <li>vulgar: 저속</li>
    <li>intimacy: 애정 행위</li>
    <li>sexy: 선정적</li>
</td>
</tr><tr>
<td>정치적으로 민감한 정보</td>
<td>영상 화면에서 다음을 포함한 정치적으로 민감한 정보를 확인합니다.
    <li>bloody: 유혈이 낭자한 장면</li>
    <li>explosion: 폭발</li>
    <li>violation_photo: 규정 위반 아이콘</li>
    <li>guns: 무기와 총</li>
</td>
</tr><tr>
</tr><tr>
<td rowspan=2 style="text-align:center">ASR 텍스트<br>(오디오의 텍스트)</td>
<td>포르노 정보
<td>음성 텍스트에 대한 포르노 정보를 확인하여 의심되는 키워드 식별</td>
</tr><tr>
<td>정치적으로 민감한 정보</td>
<td>음성 텍스트에 대해 정치적으로 민감한 정보를 확인하여 의심되는 키워드 식별</td>
</tr><tr>
<td rowspan=2 style="text-align:center">OCR 텍스트<br>(영상 화면의 텍스트)</td>
<td>포르노 정보</td>
<td>영상 화면의 텍스트에 대한 포르노 정보를 확인하여 의심되는 키워드 식별</td>
</tr><tr>
<td>정치적으로 민감한 정보</td>
<td>영상 화면의 텍스트에 대해 정치적으로 민감한 정보를 확인하여 의심되는 키워드 식별</td>
</tr>
</table>

#### 매개변수 설명

| 필드     | 유형   | 의미                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| confidence | Float  | 스마트 인식 점수(0 – 100). 점수가 높을수록 의심도가 높음                |
| suggestion | String | 스마트 인식 유형은 pass, review, block의 세 가지 유형을 권장합니다.<ul style="margin:0;"><li >pass: 의심의 정도가 높지 않아 승인 권장.</li><li>review: 의심의 정도가 높아 수동 검토 권장.</li><li>block: 의심의 정도가 매우 높아 승인하지 않을 것을 권장</li></ul> |
| segments   | Array  | 의심되는 동영상 세그먼트, 부적절한 내용이 의심되는 동영상의 특정 세그먼트 찾기를 지원합니다.         |



## 작업 시작
### 작업 설명
비디오 콘텐츠 스마트 식별 작업은 ‘API를 통한 수동 시작’ 및 ‘업로드를 통한 자동 트리거’의 두 가지 방법을 지원합니다.

- **API를 통해 능동적으로 시작:** [ProcessMedia 시작](https://intl.cloud.tencent.com/document/product/1041/33640) 인터페이스를 호출하여 요청의 AiContentReviewTask 매개변수에 [비디오 콘텐츠 스마트 식별 템플릿](#sh)의 템플릿 ID를 지정합니다.
- **업로드에 의해 자동으로 트리거됨:** 콘솔에서 [워크플로 생성](https://intl.cloud.tencent.com/document/product/1041/33485) 및 콘텐츠 스마트 식별을 활성화한 다음 워크플로에 바인딩된 트리거 디렉터리에 비디오를 업로드합니다. 

[](id:sh)
### 비디오 콘텐츠 스마트 인식 템플릿 생성
스마트 식별 작업은 스마트 비디오 식별 매개변수의 적용을 받으며, 이는 아래와 같이 MPS 비디오 콘텐츠 스마트 식별 템플릿 형태로 표시될 수 있습니다. 이러한 템플릿은 식별 작업에서 수행할 작업을 지정합니다.
- 영상 화면에서 포르노 정보 식별을 수행합니다.
- 영상 화면에서 정치적으로 민감한 정보 식별을 수행합니다.
- ASR을 기반으로 텍스트에 대해 포르노 정보 식별을 수행합니다.
- ASR을 기반으로 텍스트에 대해 정치적으로 민감한 정보 식별을 수행합니다.
- OCR을 기반으로 텍스트에 대해 포르노 정보 식별을 수행합니다.
- OCR을 기반으로 텍스트에 대해 정치적으로 민감한 정보 식별을 수행합니다.

일반적인 작업 조합을 위해 MPS는 [사전 설정된 비디오 콘텐츠 스마트 식별 템플릿](https://intl.cloud.tencent.com/document/product/1041/33476)을 제공합니다. 또한 [서버 API](https://intl.cloud.tencent.com/document/product/1041/33675)를 호출하여 맞춤형 비디오 콘텐츠 스마트 식별 템플릿을 생성하고 관리할 수도 있습니다.

## 결과 가져오기
스마트 비디오 인식 작업을 시작한 후 [쿼리 작업](https://intl.cloud.tencent.com/document/product/1041/33497)을 동기화하거나 [결과 알림](https://intl.cloud.tencent.com/document/product/1041/33499)을 비동기적으로 기다려 작업 실행 결과를 얻을 수 있습니다. 

다음은 비디오 콘텐츠 스마트 인식 작업이 시작된 후 ‘쿼리 작업’ 모드에서 얻은 결과의 예입니다(null 값이 있는 필드는 생략).
```json
{
    "TaskType":"WorkflowTask",
    "Status":"FINISH",
    "CreateTime":"2019-07-16T06:21:27Z",
    "BeginProcessTime":"2019-07-16T06:21:28Z",
    "FinishTime":"2019-07-16T06:21:46Z",
    "WorkflowTask":{
        "TaskId":"2356768367-WorkflowTask-2e1af2456351812be963e309cc133403t0",
        "Status":"FINISH",
        "InputInfo":{
            "Type":"COS",
            "CosInputInfo":{
                "Bucket":"MyVideoBucket-235303****",
                "Region":"ap-beijing",
                "Object":"/input/AnimalWorld.mp4"
            }
        },
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

        ],
        "AiContentReviewResultSet":[
            {
                "Type":"Porn",
                "PornTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Confidence":98,
                        "Suggestion":"block",
                        "Label":"sexy",
                        "SegmentSet":[
                            {
                                "StartTimeOffset":9.5,
                                "EndTimeOffset":14,
                                "Confidence":98,
                                "Suggestion":"block",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcloud.com/xxx/xxx/xx1.jpg",
                                "PicUrlExpireTime":"2019-07-23T06:21:46Z"
                            },
                            {
                                "StartTimeOffset":16.5,
                                "EndTimeOffset":18,
                                "Confidence":80,
                                "Suggestion":"review",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcloud.com/xxx/xxx/xx2.jpg",
                                "PicUrlExpireTime":"2019-07-23T06:21:46Z"
                            },
                            {
                                "StartTimeOffset":41,
                                "EndTimeOffset":49,
                                "Confidence":97,
                                "Suggestion":"block",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcloud.com/xxx/xxx/xx3.jpg",
                                "PicUrlExpireTime":"2019-07-23T06:21:46Z"
                            }
                        ]
                    }
                }
            },
            {
                "Type":"Terrorism",
                "TerrorismTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Confidence":0,
                        "Suggestion":"pass",
                        "SegmentSet":[

                        ]
                    }
                }
            },
            {
                "Type":"Political",
                "PoliticalTask":{
                    "Status":"SUCCESS",
                    "ErrCode":0,
                    "Message":"",
                    "Input":{
                        "Definition":10
                    },
                    "Output":{
                        "Confidence":0,
                        "Suggestion":"pass",
                        "SegmentSet":[

                        ]
                    }
                }
            }
        ],
        "AiAnalysisResultSet":[

        ],
        "AiRecognitionResultSet":[

        ]
    },
    "TasksPriority":0,
    "SessionId":"",
    "SessionContext":"",
    "RequestId":"xxx-xxx-xxx"
}
```

쿼리 결과에서 `WorkflowTask.AiContentReviewResultSet`에는 Type이 Porn, Terrorism 및 Political 의 세 가지 유형의 스마트 인식 결과가 포함됩니다.

- Type이 Porn인 결과에는 'Output.Suggestion'이 block된 것으로 나타났습니다. 즉 스마트 인식의 가능성이 높고 승인하지 않을 것을 권장하며 스마트 인식의 신뢰도는 98점, 스마트 인식의 이유는 sexy(관능)입니다.
- Type이 Porn인 결과에는 `Output.SegmentSet`에는 스마트 인식으로 의심되는 세 개의 비디오 세그먼트가 나열됩니다. 각 세그먼트의 시작 시간과 종료 시간은 StartTimeOffset 및 EndTimeOffset으로 표시됩니다.
- Type이 Terrorism 및 Political의 결과는 동영상에 부적절한 내용이 포함된 것으로 의심되지 않음을 보여줍니다.
