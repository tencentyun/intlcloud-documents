비디오 콘텐츠 심사는 AI를 통해 동영상 콘텐츠를 지능적으로 심사하는 오프라인 작업입니다. 작업 실행 결과에는 심사 점수, 심사 제안 및 의심되는 동영상 세그먼트가 포함됩니다. ‘심사 제안’에 따라 동영상 게시 허용 여부를 결정할 수 있으므로 규정을 준수하지 않는 동영상으로 인한 잠재적인 법적 위험 및 브랜드 이미지 손상을 효과적으로 방지할 수 있습니다.

VOD는 영상 화면, ASR로 인식한 텍스트, OCR로 인식한 텍스트를 지능적으로 인식할 수 있습니다. 이 작업에는 포르노, 테러 및 정치적으로 민감한 정보 인식이 포함됩니다.

<table>
    <tr>
        <th style="width:20%">
            객체
        </th>
        <th style="width:10%">
            작업
        </th>
        <th>
            설명
        </th>
    </tr>
    <tr>
        <td rowspan=4>
            영상 화면(사람 및 물체)
        </td>
    </tr>
    <tr>
        <td>
            포르노 정보
        </td>
        <td>
				    영상 화면에서 다음을 포함한 포르노 정보 식별을 수행합니다.
				    <li>vulgar: 저속</li>
				    <li>intimacy: 애정 행위</li>
				    <li>sexy: 선정적</li>
        </td>
    </tr>
    <tr>
        <td>
            테러 정보
        </td>
        <td>
				    다음을 포함하여 영상 화면에 대한 테러 정보 식별을 수행합니다.
				    <li>militant: 무장 단체</li>
				    <li>guns: 무기와 총</li>
				    <li>bloody: 유혈이 낭자한 장면</li>
				    <li>police: 경찰 부대</li>
				    <li>crowd: 밀집한 군중</li>
        </td>
    </tr>
    <tr>
        <td>
            정치적으로 민감한 정보
        </td>
        <td>
            영상 화면에서 다음을 포함한 정치적으로 민감한 정보 식별을 수행합니다.
				    <li>violation_photo: 규정 위반 아이콘</li>
				    <li>politician: 관련 인물</li>
        </td>
    </tr>
    <tr>
        <td rowspan=2>
            ASR 텍스트(구절)
        </td>
        <td>
				    포르노 정보
        <td>
            음성 문구에 대한 포르노 정보 식별을 수행하여 의심되는 키워드를 식별합니다.
        </td>
    </tr>
    <tr>
        <td>
            정치적으로 민감한 정보
        </td>
        <td>
            음성 구문에 대해 정치적으로 민감한 정보 식별을 수행하여 의심되는 키워드를 식별합니다.
        </td>
    </tr>
    <tr>
        <td rowspan=2>
            OCR 텍스트(영상 화면의 텍스트)
        </td>
        <td>
				    포르노 정보
        </td>
        <td>
            영상 화면의 텍스트에 대한 포르노 정보 식별을 수행하여 의심되는 키워드를 식별합니다.
        </td>
    </tr>
    <tr>
        <td>
            정치적으로 민감한 정보
        </td>
        <td>
            영상 화면의 텍스트에 대해 정치적으로 민감한 정보 식별을 수행하여 의심되는 키워드를 식별합니다.
        </td>
    </tr>
</table>


| 필드     | 유형   | 의미                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| confidence | Float  | 심사 점수(0 – 100). 점수가 높을수록 의심도가 높습니다.                |
| suggestion | String | 심사 유형은 pass, review, block의 세 가지 유형을 권장합니다.<ul><li>pass: 의심의 정도가 높지 않아 승인 권장</li><li>review: 의심의 정도가 높아 수동 검토 권장</li><li>block: 의심의 정도가 매우 높아 차단 권장</li></ul> |
| segments   | Array  | 의심되는 동영상 세그먼트. 위반이 의심되는 동영상의 특정 세그먼트를 찾는 데 도움을 줍니다.         |

## [](id:sh)비디오 심사 템플릿

비디오 심사 매개변수를 통해 심사 작업에서 수행하는 심사 작업을 제어할 수 있습니다. VOD는 비디오 심사 템플릿을 사용하여 심사 매개변수 집합을 나타냅니다. 비디오 심사 템플릿을 통해 심사 작업에서 수행할 다음 작업 중 하나 이상을 지정할 수 있습니다.
- 영상 화면에서 포르노 정보 식별을 수행합니다.
- 영상 화면에서 테러 정보 식별을 수행합니다.
- 영상 화면에서 정치적으로 민감한 정보 식별을 수행합니다.
- ASR을 기반으로 텍스트에 대해 포르노 정보 식별을 수행합니다.
- ASR을 기반으로 텍스트에 대해 정치적으로 민감한 정보 식별을 수행합니다.
- OCR을 기반으로 텍스트에 대해 포르노 정보 식별을 수행합니다.
- OCR을 기반으로 텍스트에 대해 정치적으로 민감한 정보 식별을 수행합니다.

일반적인 작업 조합을 위해 VOD는 [사전 설정된 비디오 심사 템플릿](https://intl.cloud.tencent.com/document/product/266/33932)을 제공합니다. 또한 [서버 API](https://intl.cloud.tencent.com/document/product/266/37566)를 호출하여 맞춤형 비디오 심사 템플릿을 생성 및 관리할 수 있습니다.

## 작업 시작

비디오 콘텐츠 심사 작업을 시작하는 방법에는 ‘서버 API를 통한 직접 시작’, ‘콘솔을 통한 직접 시작’ 및 ‘업로드 시 실행할 작업 지정’의 세 가지 방법이 있습니다. 자세한 내용은 비디오 처리 [작업 시스템](https://intl.cloud.tencent.com/document/product/266/33931)을 참고하십시오.

다음은 비디오 콘텐츠 심사 작업을 시작하는 다양한 방식에 관한 설명입니다.

* 서버 API [ProcessMedia](https://intl.cloud.tencent.com/document/product/266/34125)를 호출하여 작업 시작: 요청의 `AiContentReviewTask` 매개변수에 [비디오 콘텐츠 심사 템플릿](#sh)의 템플릿 ID를 지정합니다.
* 서버 API [ProcessMediaByUrl](https://intl.cloud.tencent.com/document/product/266/34123)를 호출하여 작업 시작: 요청의 `AiContentReviewTask` 매개변수에 [비디오 콘텐츠 심사 템플릿](#sh)의 템플릿 ID를 지정합니다.
* 콘솔을 통해 동영상 작업 시작: 콘솔에 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 콘솔에서 비디오 콘텐츠 심사를 활성화하고, [비디오 처리 시작](https://intl.cloud.tencent.com/document/product/266/33892)합니다.
* 서버에서 업로드 시 작업 지정: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 태스크 플로우에서 비디오 콘텐츠 심사를 활성화하고, 이 태스크 플로우를 [업로드 신청](https://intl.cloud.tencent.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0) 요청의 `procedure`로 지정합니다.
* 클라이언트에서 업로드할 때 작업 지정: 콘솔에서 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 내부에서 비디오 콘텐츠 심사를 활성화하고, [클라이언트 업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922)에서 이 태스크 플로우를 `procedure` 매개변수로 지정합니다.
* 콘솔을 통해 업로드: 콘솔에 [태스크 플로우 추가](https://intl.cloud.tencent.com/document/product/266/14058) 후, 비디오 콘텐츠 심사를 활성화하고, 콘솔을 통해 동영상을 업로드한 다음, [업로드 중 비디오 처리](https://intl.cloud.tencent.com/document/product/266/33890)를 선택하여 비디오 업로드 완료 시 이 태스크 플로우를 실행하도록 지정합니다.

## 결과 가져오기

비디오 심사를 시작한 후 비동기화 방식으로 [결과 알림](https://intl.cloud.tencent.com/document/product/266/33931)을 비동기적으로 기다리거나 [작업 쿼리](https://intl.cloud.tencent.com/document/product/266/33931)를 동기적으로 수행하여 작업 실행 결과를 얻을 수 있습니다. 다음은 비디오 심사 작업이 시작된 후 일반 콜백 방식으로 결과 알림을 받는 예시입니다(null 값이 있는 필드는 생략).
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
                                "Url":"http://xxx.vod2.myqcluod.com/xxx/xxx/xx1.jpg",
                                "PicUrlExpireTimeStamp":1530005146
                            },
                            {
                                "StartTimeOffset":16.5,
                                "EndTimeOffset":18,
                                "Confidence":80,
                                "Suggestion":"review",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcluod.com/xxx/xxx/xx2.jpg",
                                "PicUrlExpireTimeStamp":1530005146
                            },
                            {
                                "StartTimeOffset":41,
                                "EndTimeOffset":49,
                                "Confidence":97,
                                "Suggestion":"block",
                                "Label":"sexy",
                                "Url":"http://xxx.vod2.myqcluod.com/xxx/xxx/xx3.jpg",
                                "PicUrlExpireTimeStamp":1530005146
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
        "TasksPriority":0,
        "TasksNotifyMode":""
    }
}
```

콜백 결과에서 `ProcedureStateChangeEvent.AiContentReviewResultSet`에는 포르노, 테러 및 정치적으로 민감한 정보의 영상 화면 식별을 각각 나타내는 `Porn`, `Terrorism`, `Political`의 세 가지 `Type`의 심사 결과가 포함됩니다.

* `Type`이 `Porn`인 결과에는 `Output.Suggestion`이 `block`된 것으로 나타났습니다. 즉, 포르노 정보의 존재 가능성이 높고 차단을 권장하며, 포르노 정보의 신뢰도는 98, 이유는 `sexy`(선정적)입니다.
* `Type`이 `Porn`인 결과에는 `Output.SegmentSet`에는 포르노 정보가 포함된 것으로 의심되는 세 개의 비디오 세그먼트가 나열됩니다. 각 세그먼트의 시작 시간과 종료 시간은 `StartTimeOffset` 및 `EndTimeOffset`으로 표시됩니다.
* `Type`이 `Terrorism` 및 `Political`인 결과는 동영상에 테러 및 정치적으로 민감한 정보가 포함된 것으로 의심되지 않음을 보여줍니다.


