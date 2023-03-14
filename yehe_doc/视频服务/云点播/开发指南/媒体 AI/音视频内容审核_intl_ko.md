오디오/비디오 콘텐츠 조정은 AI의 도움을 받아 오디오/비디오 콘텐츠를 지능적으로 조정하는 오프라인 작업입니다. 작업 실행 결과에는 신뢰 점수, 조정 제안 및 의심되는 비디오 세그먼트가 포함됩니다. ‘조정 제안’에 따라 비디오 게시 허용 여부를 결정할 수 있으므로 규정을 준수하지 않는 비디오로 인한 잠재적인 법적 위험 및 브랜드 평판 손상을 효과적으로 피할 수 있습니다.

VOD는 화면 이미지, 화면 내 텍스트, 음성 내 텍스트, 사운드 콘텐츠의 네 가지 객체를 조정할 수 있으며 조정 태그에는 음란물, 테러 및 신음 소리가 포함됩니다.

<table>
    <tr>
        <th style="width:20%">
            객체
        </th>
        <th style="width:20%">
            조정 레이블
        </th>
        <th>
            설명
        </th>
    </tr>
    <tr>
        <td rowspan=3>
            이미지
        </td>
    </tr>
    <tr>
        <td>
            음란물(Porn)
        </td>
        <td>
				    음란물 및 외설적인 콘텐츠 등.
        </td>
    </tr>
    <tr>
        <td>
            테러(Terror)
        </td>
        <td>
				    폭력, 유혈, 테러 관련 콘텐츠 등.
        </td>
    </tr>
		<tr>
        <td rowspan=1>
           사운드
        </td>
        <td>
				    신음 소리(Moan)
        </td>
        <td>
            성적으로 암시적인 소리.
        </td>
    </tr>
    <tr>
        <td rowspan=3>
            음성 중 텍스트 인식(ASR)
        </td>
        <tr>
        <td>
            음란물(Porn)
        </td>
        <td>
				    음란물 및 외설적인 콘텐츠 등.
        </td>
    </tr>
    <tr>
        <td>
            테러(Terror)
        </td>
        <td>
				    폭력, 유혈, 테러 관련 콘텐츠 등.
        </td>
    </tr>
        <td rowspan=3>
            이미지 중의 텍스트 인식(OCR)
        </td>
        <tr>
        <td>
            음란물(Porn)
        </td>
        <td>
				    음란물 및 외설적인 콘텐츠 등.
        </td>
    </tr>
    <tr>
        <td>
            테러(Terror)
        </td>
        <td>
				    폭력, 유혈, 테러 관련 콘텐츠 등.
        </td>
    </tr>
</table>

아래 표에는 조정 결과의 일부 필드가 나열되어 있습니다.

| 필드     | 유형   | 설명                                                         |
| ---------- | ------ | ------------------------------------------------------------ |
| Confidence | Float  | 신뢰도 점수(0 – 100). 점수가 높을수록 의심의 정도가 큽니다.                |
| Suggestion | String | 조정 제안에는 pass, review, block의 세 가지 유형이 있습니다.<ul><li>pass: 부적절한 콘텐츠에 대한 의심이 높지 않으며 콘텐츠를 통과하도록 권장합니다</li><li>review: 부적절한 콘텐츠에 대한 의심이 높으며 수동 검토가 권장됩니다</li><li>block: 부적절한 콘텐츠에 대한 의심이 매우 높으며 차단을 권장합니다</li></ul> |
| Form   | String  | 조정 형식: <ul><li>Image: 영상</li><li>Voice: 음성</li><li>OCR: 광학 문자 인식</li><li>ASR: 자동 음성 인식</li></ul> |
| Label   | String  | 조정 레이블: <ul><li>Porn: 음란물</li><li>Terror: 테러</li><li>Moan: 신음 소리</li></ul> |

## [](id:sh)오디오/비디오 조정 템플릿

오디오/비디오 조정 템플릿은 조정 매개변수 집합을 나타냅니다. 템플릿을 사용하여 다음 조정 레이블 중 사용할 항목을 지정할 수 있습니다.
- 음란물(Porn)
- 테러(Terror)
- 신음 소리(Moan)

VOD는 일반적인 매개변수 조합에 대한 [사전 설정 오디오/비디오 조정 템플릿](https://intl.cloud.tencent.com/document/product/266/33932)을 제공합니다. [서버 API](https://www.tencentcloud.com/document/product/266/37566)를 사용하여 사용자 정의 템플릿을 생성하고 관리할 수도 있습니다.

## 작업 시작

오디오/비디오 콘텐츠 조정 작업을 시작하는 방법에는 ‘서버 API를 통한 직접 시작’, ‘콘솔을 통한 직접 시작’ 및 ‘업로드 시 실행할 작업 지정’의 세 가지 방법이 있습니다. 자세한 내용은 [비디오 처리 작업 시스템](https://intl.cloud.tencent.com/document/product/266/33931)을 참고하십시오.

다음과 같은 방법으로 오디오/비디오 조정 작업을 시작할 수 있습니다.

* 서버측 API [ReviewAudioVideo](https://www.tencentcloud.com/document/product/266/50634)를 호출합니다.
* 콘솔에서 작업을 시작합니다. 자세한 지침은 [오디오/비디오 조정](https://intl.cloud.tencent.com/document/product/266/33897)을 참고하십시오.
* 서버 업로드 시 작업 지정: 서버 측 API [CreateProcedureTemplate](https://www.tencentcloud.com/document/product/266/34167)을 호출하여 오디오/비디오 조정이 활성화된 태스크 플로우(`ReviewAudioVideoTask`)를 생성하고, [ApplyUpload](https://www.tencentcloud.com/document/product/266/34120#2.-.E8.BE.93.E5.85.A5.E5.8F.82.E6.95.B0)를 호출하여 비디오를 업로드할 때 생성된 태스크 플로우의 이름으로 `procedure`를 설정합니다.
* 클라이언트 업로드 시 작업 지정: 서버 측 API [CreateProcedureTemplate](https://www.tencentcloud.com/document/product/266/34167)을 호출하여 오디오/비디오 조정이 활성화된 태스크 플로우(`ReviewAudioVideoTask`)를 생성하고 [클라이언트 업로드 서명](https://intl.cloud.tencent.com/document/product/266/33922)에서 생성된 태스크 플로우의 이름으로 `procedure`를 설정합니다.
* 콘솔 업로드: 서버 측 API [CreateProcedureTemplate](https://www.tencentcloud.com/document/product/266/34167)을 호출하여 오디오/비디오 조정이 활성화된 태스크 플로우(`ReviewAudioVideoTask`)를 생성하고, 콘솔을 통해 비디오를 업로드할 때 [오디오/비디오 업로드](https://intl.cloud.tencent.com/document/product/266/33890)를 선택한 후 생성된 태스크 플로우를 선택합니다.

## 결과 가져오기

조정 작업을 시작한 후 [ReviewAudioVideoComplete](https://www.tencentcloud.com/document/product/266/50677) 알림을 비동기적으로 기다리거나 [작업 쿼리](https://intl.cloud.tencent.com/document/product/266/33931)를 동기적으로 수행하여 작업 실행 결과를 얻을 수 있습니다. 다음은 일반 콜백 모드에서 알림의 예입니다(null 값이 있는 필드는 생략됨).
```json
{
    "EventType": "ReviewAudioVideoComplete",
    "ReviewAudioVideoCompleteEvent": {
        "TaskId": "125xxxx-ReviewAudioVideo-07edbc78ba20563cdf2362cffbf4aa0ct",
        "Status": "FINISH",
        "ErrCodeExt": "",
        "Message": "SUCCESS",
        "Input":{
            "FileId": "387702130626135215"
        },
        "Output":{
            "Suggestion": "block",
            "Label": "Porn",
            "Form": "Image",
            "SegmentSet":[
                {
                    "StartTimeOffset": 0,
                    "EndTimeOffset": 1,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163480.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:16.039Z"
                },
                {
                    "StartTimeOffset": 1,
                    "EndTimeOffset": 2,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163481.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:17.039Z"
                },
                {
                    "StartTimeOffset": 2,
                    "EndTimeOffset": 3,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163482.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:18.039Z"
                },
                {
                    "StartTimeOffset": 3,
                    "EndTimeOffset": 4,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163483.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:19.039Z"
                },
                {
                    "StartTimeOffset": 4,
                    "EndTimeOffset": 5,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163484.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:20.039Z"
                },
                {
                    "StartTimeOffset": 5,
                    "EndTimeOffset": 6,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163485.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:21.039Z"
                },
                {
                    "StartTimeOffset": 6,
                    "EndTimeOffset": 7,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163486.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:22.039Z"
                },
                {
                    "StartTimeOffset": 7,
                    "EndTimeOffset": 8,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163487.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:23.039Z"
                },
                {
                    "StartTimeOffset": 8,
                    "EndTimeOffset": 9,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163488.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:24.039Z"
                },
                {
                    "StartTimeOffset": 9,
                    "EndTimeOffset": 10,
                    "Confidence": 99,
                    "Suggestion": "block",
                    "Label": "Porn",
                    "SubLabel": "SexyBehavior",
                    "Form": "Image",
                    "AreaCoordSet": [],
                    "Text": "",
                    "KeywordSet": [],
                    "Url": "https://251000800.vod2.myqcloud.com/1a168d62vodcq251000800/result/vod/w-video-Y7uETQ0Oqj4SY3Fh/screenshot_0_1638163489.jpg",
                    "PicUrlExpireTime": "2023-01-16T03:06:25.039Z"
                }
            ],
            "SegmentSetFileUrl": "http://251000800.vod2.myqcloud.com/a8800b40vodtranssgp251000800/0f9bd2b0-34a8-4642-f481-001894d93019.txt",
            "SegmentSetFileUrlExpireTime": "2022-10-12T07:01:07.695Z"
        },
        "SessionContext": "",
        "SessionId": ""
    }
}
```

상기 콜백에서 `ReviewAudioVideoCompleteEvent.Output`은 오디오/비디오 조정 결과입니다. `Output.Suggestion` = `block`은 VOD가 콘텐츠 차단을 제안함을 나타냅니다. `Output.Label=Porn` 및 `Output.Form=Image`는 가장 위반 가능성이 높은 콘텐츠가 비디오 화면에 포함된 선정적인 정보임을 나타냅니다.

오디오/비디오 클립에는 의심스러운 부분이 여러 개 포함될 수 있습니다. `Output.SegmentSet`은 처음 10개만 나열합니다. 유효 기간 내에 `Output.SegmentSetFileUrl`을 방문하면 모든 의심스러운 세그먼트의 정보를 볼 수 있습니다.

`StartTimeOffset` 및 `EndTimeOffset`은 의심 세그먼트의 시작 및 종료 시간이며 `SubLabel`은 위반 유형을 나타냅니다.

이미지 또는 음성의 텍스트가 조정되는 경우:
* `Text`는 인식된 전체 텍스트입니다.
* `KeywordSet`는 히트된 키워드 목록입니다.

이미지(사람 및 사물) 또는 이미지의 텍스트가 조정되는 경우:
* `AreaCoordSet`은 규정 위반 객체의 좌표입니다.
* `Url`은 규정 위반 이미지의 URL입니다.
* `PicUrlExpireTime`은 `Url`의 만료 시간입니다. 이 시간 이후에는 액세스할 수 없습니다.
