CSS의 음란물 감지 기능을 사용하려면 화면 캡처를 활성화해야 합니다. 음란물 감지 기능은 [CSS 콘솔](https://intl.cloud.tencent.com/document/product/267/31072)에서 구성하거나 API를 사용하여 사용할 수 있습니다. 이 문서는 음란물 감지 API를 사용하는 방법을 보여줍니다.


## 주의 사항
COS Bucket의 액세스 권한이 공개 읽기일 때, 정치적으로 민감한 내용, 음란물 또는 기타 부적절한 콘텐츠가 있는 경우 COS Bucket이 차단되지 않도록 하려면 먼저 콘텐츠를 삭제하십시오.

## 라이브 방송 음란물 감지 활성화
음란물 감지 기능은 화면 캡처를 기반으로 하므로 음란물 감지를 활성화하려면 먼저 화면 캡처를 활성화해야 합니다. 단계는 다음과 같습니다.

### 1. 음란물 감지가 활성화된 화면 캡처 템플릿 생성
[CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834)을 호출하고 PornFlag = 1을 설정하여 음란물 감지가 활성화된 화면 캡처 템플릿을 생성합니다.

### 2. 화면 캡처 규칙 생성
[CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30835)을 호출하여 1단계에서 만든 화면 캡처 템플릿의 ID를 대상 AppId, DomainName, AppName 및 StreamName과 바인딩하는 화면 캡처 규칙을 만듭니다.

### 3. 라이브 스트리밍 시작
음란물 감지가 활성화된 화면 캡처 규칙을 생성하면 음란물 감지 기능이 새 스트림에 대해 자동으로 활성화됩니다. 진행 중인 스트림에 대해 음란물 감지를 활성화하려면 스트림을 중지했다가 다시 시작해야 합니다.

## 음란물 감지 결과 가져오기
음란물 감지가 활성화되면 음란물 감지 콜백 템플릿에 등록된 도메인 이름을 구성하여 음란물 감지 결과의 콜백을 수신할 수 있습니다.
>! 기본적으로 의심스러운 결과만 콜백됩니다.

### 1. 음란물 감지 콜백 템플릿 생성
[CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815)을 호출하고 PornCensorshipNotifyUrl을 도메인 이름으로 설정하여 음란물 감지 콜백 템플릿을 만듭니다.
### 2. 음란물 감지 콜백 규칙 생성

[CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816)을 호출하여 음란물 감지 콜백 규칙을 만들고 1단계에서 만든 음란물 감지 콜백 템플릿의 ID를 대상 AppId, DomainName 및 AppName에 바인딩합니다.

### 3. 음란물 감지 결과 가져오기
CSS 백엔드는 음란물 감지 결과를 HTTP POST 요청 형식으로 도메인에 보냅니다. 요청 Body에서 JSON 형식의 결과를 찾을 수 있습니다. type 필드는 라이브 스트림에 음란물 콘텐츠가 포함되어 있는지 여부를 나타냅니다.
>! 시스템 정확도가 100%일 수는 없으므로 허위 양성 또는 허위 음성이 있을 수 있습니다. 음란물로 의심되는 이미지는 'type' 필드를 사용하여 2차 검토하는 것이 좋습니다.  

#### 매개변수는 다음과 같습니다.
| 매개변수      | 필수        | 데이터 유형        | 설명        |
| -------- | -------- | -------- | -------- |
| streamId    | No     | String | 스트림 이름     |
| channelId      | No     | string   | 채널 ID     |
| img     | Yes     | string   | 의심스러운 이미지의 링크      |
| type    | Yes     | Array    | 감지 결과 우선순위가 가장 높은 레이블 값입니다. 자세한 내용은 label 설명을 참고하십시오. |
| score       | Yes     | Array    | 신뢰도 점수   |
| ocrMsg      | No     | string   | OCR 결과(존재할 경우)       |
| suggestion     | Yes     | string   | 권장, 유효한 값: <ul style="margin:0"><li/>Block: 차단<li/>Review: 재심사<li/>Pass: 통과</ul> |
| label       | Yes     | string   | 감지 결과(LabelResults)에서 우선 순위가 가장 높은 레이블입니다. 이것은 모델에 의해 생성된 결과입니다. 비즈니스 요구에 따라 다양한 유형의 위반을 처리하십시오. |
| subLabel    | Yes     | string   | 음란물 - 성행위 등 감지 결과에서 우선 순위가 가장 높은 레이블의 서브 레이블입니다. 히트된 서브 레이블이 없으면 이 필드는 비어 있습니다. |
| labelResults   | No     | [Array of LabelResult](#labelresult)   | 음란물, 광고, 테러리스트 콘텐츠 및 정치적으로 민감한 콘텐츠의 탐지를 포함하여 카테고리 모델에서 생성된 레이블 히트 결과입니다. <br>참고: **이 필드는 유효한 값을 얻을 수 없음을 나타내는 null을 반환할 수 있습니다**. |
| objectResults  | No     | [Array of ObjectResult](#objectresult) | 레이블 이름, 히트 점수, 좌표, 시나리오 및 수상한 객체에 대한 제안, 광고 로고, QR 코드 등을 포함하는 객체 모델의 감지 결과입니다. 자세한 내용은 ObjectResults의 데이터 구조 설명을 참고하십시오.<br> 참고: **이 필드는 유효한 값을 얻을 수 없음을 나타내는 null을 반환할 수 있습니다**. |
| ocrResults     | No     | [Array of OcrResult](#ocrresult)    | 텍스트 좌표, 인식된 텍스트, 제안된 작업 등을 포함한 OCR 결과입니다. 자세한 내용은 OcrResults의 데이터 구조 설명을 참고하십시오.<br> 참고: **이 필드는 유효한 값을 얻을 수 없음을 나타내는 null을 반환할 수 있습니다**. |
| libResults     | No     | [Array of LibResult](#libresult)    | 블록리스트/얼로우리스트 감지 결과  |
| screenshotTime | Yes     | Number | 스크린샷 시간 |
| sendTime    | Yes     | Number | 요청이 전송된 Unix 타임스탬프 |
| stream_param   | No     | String | 푸시 매개변수 |
| app | No     | String | 푸시 도메인 |
| appid     | No     | Number | 애플리케이션 ID |
| appname     | No     | String | 푸시 path |

#### LabelResult
카테고리 모델에서 생성된 레이블 히트 결과입니다.

| 매개변수   | 유형  | 설명    |
| ---------- | ------------------------ | ------------------------ |
| Scene      | String      | 광고, 음란물, 유해성 등 모델 식별 시나리오.      |
| Suggestion | String     | 현재 악성 레이블에 대해 시스템에서 제안한 작업입니다. 비즈니스 요구 사항에 따라 다양한 유형의 위반 및 제안을 처리하는 것이 좋습니다. 반환된 값: <ul style="margin:0"><li/>Block: 차단<li/>Review: 재심사<li/>Pass: 통과</ul> |
| label | String      | 레이블 히트 |
| SubLabel   | String | 서브 레이블 이름|
| Score      | Integer | 레이블의 신뢰도 점수    |
| Details    | Array of [LabelDetailItem](#labeldetailitem) | 카테고리 모델의 서브 레이블 히트 세부 정보     |

#### LabelDetailItem

카테고리 모델의 서브 레이블 히트 세부 정보입니다.

| 매개변수 | 유형 | 설명 |
| -------- | -------- | ----- |
| Id    | Integer  | ID   |
| Name     | String   | 서브 태그 이름     |
| Score    | Integer  | 서브 레이블 점수, 값 범위: 0점 - 100점|

#### ObjectResult

객체 감지 결과입니다.

| 매개변수   | 유형    | 설명     |
| ---------- | --------------------- | --------------------- |
| Scene      | String   | QR 코드, logo, OCR 등 객체 시나리오 식별 |
| Suggestion | String   | 현재 악성 레이블에 대해 시스템에서 제안한 작업입니다. 비즈니스 요구 사항에 따라 다양한 유형의 위반 및 제안을 처리하는 것이 좋습니다. 반환된 값: <ul style="margin:0"><li/>Block: 차단<li/>Review: 재심사<li/>Pass: 통과</ul> |
| label | String   | 레이블 히트 |
| SubLabel   | String      | 서브 레이블 이름 |
| Score      | Integer | 서브 레이블 점수, 값 범위: 0점 - 100점. |
| Names      | Array of String    | 객체 이름 리스트 |
| Details    | Array of [ObjectDetail](#objectdetail) | 객체 감지 세부 정보 |

#### ObjectDetail

객체 감지 세부 정보입니다. 감지 시나리오가 엔터티, 광고 로고, QR 코드인 경우 감지 프레임의 레이블 이름, 레이블 값, 레이블 점수 및 위치 정보를 반환합니다.

| 매개변수     | 유형     | 설명    |
| -------- | -------- | -------- |
| Id    | Integer    | 식별된 객체의 ID    |
| Name     | String     | 레이블 히트   |
| Value    | String     | 레이블 히트 값 또는 내용입니다. 예를 들어 레이블이 QR 코드(QrCode)인 경우 이 매개변수는 QR 코드의 URL입니다. |
| Score    | Integer    | 레이블의 히트 점수입니다. 값 범위: 0-100. 예를 들어 QrCode 99는 콘텐츠가 QR 코드일 가능성이 높다는 것을 나타냅니다. |
| Location | [Location](#location) | 객체 감지 프레임의 좌표(왼쪽 상단 xy 좌표, 길이 및 너비, 회전 각도), 크기 및 회전 |

#### Location

감지 프레임의 좌표 및 기타 정보.

| 매개변수     | 유형     | 설명    |
| -------- | -------- | ---------------- |
| X        | Float    | 왼쪽 상단 모서리의 가로 좌표     |
| Y        | Float    | 왼쪽 상단 모서리의 세로 좌표     |
| Width    | Float    | 폭             |
| Height   | Float    | 높이             |
| Rotate   | Float    | 감지 프레임의 회전 각도 |

#### OcrResult

OCR 결과.

| 매개변수   | 유형  | 설명   |
| ---------- | ---------------------- | ---------------------- |
| Scene      | String    | 인식 시나리오. 기본값: OCR. |
| Suggestion | String     | 우선순위가 가장 높은 악성 레이블에 대해 시스템에서 제안한 작업입니다. 비즈니스 요구 사항에 따라 다양한 유형의 위반 및 제안을 처리하는 것이 좋습니다. 반환된 값: <ul style="margin:0"><li/>Block: 차단<li/>Review: 재심사<li/>Pass: 통과</ul> |
| label | String     | 레이블 히트 |
| SubLabel   | String      | 서브 레이블 이름 |
| Score      | Integer | 서브 레이블의 신뢰도 점수, 값 범위: 0점 - 100점. |
| Text    | String | 텍스트 |
| Details    | Array of [OcrTextDetail](#ocrtextdetail) | OCR 세부 정보 |

#### OcrTextDetail
OCR 세부 정보

| 매개변수 | 유형     | 설명  |
| -------- | --------------- | --------------- |
| Text     | String     | 텍스트 인식(**최대 5000바이트**). |
| label | String     | 레이블 히트 |
| Keywords | Array of String | 레이블 아래에 있는 히트된 키워드 |
| Score    | Integer      | 레이블의 신뢰도 점수, 값 범위: 0점 - 100점 |
| Location | [Location](#location) | OCR 텍스트 좌표 |

#### LibResult
블록리스트/얼로우리스트 결과.

| 매개변수   | 유형    | 설명     |
| ---------- | ------------------ | ------------------ |
| Scene      | String     | 모델의 시나리오 인식 결과. 기본값: Similar.    |
| Suggestion | String      | 시스템에서 제안한 작업입니다. 비즈니스 요구 사항에 따라 다양한 유형의 위반 및 제안을 처리하는 것이 좋습니다. 반환된 값: <ul style="margin:0"><li/>Block: 차단<li/>Review: 재심사<li/>Pass: 통과</ul> |
| label | String      | 레이블 히트 |
| SubLabel   | String      | 서브 레이블 이름 |
| Score      | Integer     | 신뢰도 점수, 값 범위: 0점 - 100점 |
| Details    | Array of [LibDetail](#libdetail) | 블록리스트/얼로우리스트 세부 정보 |

#### LibDetail
사용자 지정 목록 또는 블롤리스트/얼로우리스트 세부 정보.

| 매개변수     | 유형     | 설명    |
| -------- | -------- | ------------------ |
| Id    | Integer  | ID    |
| ImageId  | String   | 이미지ID    |
| label | String  | 레이블 히트 |
| Tag      | String   | 사용자 지정 레이블|
| Score    | Integer  | 신뢰도 점수. 값 범위: 0점 - 100점    |

#### 콜백 메시지 예시
<dx-codeblock>
::: HTTPbody  json
{
        "ocrMsg": "",
        "type": [1],
        "socre": 99,
        "screenshotTime": 1610640000,
        "level": 0,
        "img": "http://1.1.1.1/download/porn/test.jpg",
        "abductionRisk": [],
        "faceDetails": [],
        "sendTime": 1615859827,
        "suggestion": "Block",
        "label": "Porn",
        "subLabel": "PornHigh",
        "labelResults": [{
                "HitFlag": 0,
                "Scene": "Illegal",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }, {
                "HitFlag": 1,
                "Scene": "Porn",
                "Suggestion": "Block",
                "Label": "Porn",
                "SubLabel": "PornHigh",
                "Score": 99,
                "Details": [{
                        "Id": 0,
                        "Name": "PornHigh",
                        "Score": 99
                }, {
                        "Id": 1,
                        "Name": "WomenChest",
                        "Score": 99
                }]
        }, {
                "HitFlag": 0,
                "Scene": "Sexy",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "Terror",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Details": []
        }],
        "objectResults": [{
                "HitFlag": 0,
                "Scene": "QrCode",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "MapRecognition",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }, {
                "HitFlag": 0,
                "Scene": "PolityFace",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Names": [],
                "Details": []
        }],
        "ocrResults": [{
                "HitFlag": 0,
                "Scene": "OCR",
                "Suggestion": "Pass",
                "Label": "Normal",
                "SubLabel": "",
                "Score": 0,
                "Text": "",
                "Details": []
        }],
        "streamId": "teststream",
        "channelId": "teststream",
        "stream_param": "txSecret=40f38f69f574fd51126c421a3d96c374&txTime=5DEBEC80",
        "app": "5000.myqcloud.com",
        "appname": "live",
        "appid": 10000,
        "event_type": 317,
        "sign": "ac920c3e66**********78cf1b5de2c63",
        "t": 1615860427
}
:::
</dx-codeblock>

## 음란물 감지 비활성화

화면 캡처 규칙을 삭제하거나 화면 캡처 템플릿을 수정하여 음란물 감지를 비활성화할 수 있습니다. 삭제 및 수정은 모두 새로운 라이브 스트림에만 적용됩니다. 진행 중인 라이브 스트림에 대해 음란물 감지를 비활성화하려면 스트림을 중지했다가 다시 시작해야 합니다.

### 1. 화면 캡처 규칙 삭제

[DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833)을 호출하여 화면 캡처 규칙을 삭제하기 위해 화면 캡처 템플릿 ID에 바인딩된 DomainName, AppName 및 StreamName을 전달합니다.

### 2. 화면 캡처 템플릿 수정

[ModifyLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30828)을 호출하여 PornFlag를 0으로 설정합니다.