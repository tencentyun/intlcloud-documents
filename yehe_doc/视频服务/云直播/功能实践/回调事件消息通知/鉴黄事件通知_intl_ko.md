라이브 방송 음란물 감지는 라이브 방송 스트리밍에서 선정성이 의심되는 화면을 실시간으로 캡처하고, 생성된 이미지 파일을 COS에 저장합니다. 음란물 감지 콜백은 문제 이미지의 소속 유형, 등급 평가, 화면 캡처 시간과 같은 라이브 방송 음란물 감지 이미지 정보를 푸시하는 데 사용됩니다. 콜백 템플릿에서 음란물 감지 콜백 메시지를 수신할 서버 주소를 설정하고, 해당 템플릿을 푸시 스트림 도메인과 연결해야 합니다. 라이브 방송 스트리밍에서 음란물 감지 이벤트가 트리거 될 경우, 음란물 이미지 정보를 Tencent Cloud CSS 백그라운드에서 귀하가 설정한 수신용 서버로 콜백합니다.

본 문서에서는 음란물 감지 콜백 이벤트 발생 시 Tencent Cloud CSS가 사용자의 콜백 메시지 알림 필드로 발송하는 과정을 설명합니다.

## 주의 사항
- Tencent Cloud CSS의 콜백 기능 설정 방법을 이해하신 후 본 문서를 읽으실 것을 권장합니다. 콜백 메시지를 수신하는 방법은 [이벤트 알림 수신 방법](https://intl.cloud.tencent.com/document/product/267/38080)을 참고 바랍니다.
- 라이브 방송 음란물 감지는 기본적으로 의심스러운 결과만 콜백하며, 정상적인 결과는 콜백하지 않습니다.
- 이미지를 사용한 [type](#type)으로 음란물 판정을 진행할 것을 권장합니다. 검사 시스템의 정확도가 100%를 달성할 수는 없기 때문에, 일부 이미지가 음란물 의심 판정을 받거나 잘못된 식별 결과가 나올 수 있습니다. 실제 응용 시나리오에 따라 육안으로 2차 확인 작업을 진행할 수 있습니다.

## 화면 캡처 이벤트 매개변수 설명
### 이벤트 유형 매개변수

| 이벤트 유형 | 필드 값 설명           |
| :------- | :------------- |
| 라이브 방송 음란물 감지 | event_type = 317 |


### 콜백 공용 매개변수

<table>
<tr><th>필드 이름</th><th>유형</th><th>설명</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>만료 시간, 이벤트 알림 서명 만료 UNIX 타임스탬프입니다. <ul style="margin:0"><li>Tencent Cloud 메시지 알림의 기본 만료 시간은 10분입니다. 메시지 알림의 t 값으로 지정된 시간이 만료되었을 경우, 해당 알림을 무효라고 판정할 수 있으며, 네트워크 리플레이 공격을 방지할 수 있습니다. <li>t의 형식은 10진법 UNIX 타임스탬프입니다. 즉, 1970년 01월 01일(UTC/GMT의 자정)부터 경과한 초 단위 수입니다. </ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>이벤트 알림 보안 서명은 sign = MD5(key + t)입니다. <br>설명: Tencent Cloud는 암호화된 <a href="#key">key</a>와 t의 문자열 연결 후, MD5 계산을 통해 sign 값을 얻은 후, 이를 알림 메시지에 입력합니다. 사용자의 백그라운드 서버는 알림 메시지 수신 후 같은 계산법으로 sign이 정확한지 확인하고, 메시지 출처가 Tencent Cloud 백그라운드인지 확인할 수 있습니다. </td>
</tr></table>

>? [](Id:key)key는 **이벤트 센터>[라이브 방송 콜백](https://console.cloud.tencent.com/live/config/callback)**의 콜백 키로 주로 인증에 사용됩니다. 데이터 정보를 안전하게 보호하기 위해 입력을 권장합니다.

![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)




### 콜백 메시지 매개변수
| 매개변수      | 필수 입력 여부        | 데이터 유형        | 설명        |
| ---------- | ---------- | ---------- | --------------------------- |
| streamId | 선택 사항     | String | 스트림 이름 |
| channelId | 선택 사항     | string | 채널 ID |
| img | 필수 입력     | string | 알람 이미지 링크 |
| type | 필수 입력     | Array | 탐지 결과(labelResults) 중 우선 순위가 가장 높은 악성 태그를 반환하며, 모델 권장 심사 결과를 나타냅니다. 비즈니스 니즈에 따라 다양한 유형의 위반 및 권장 값을 처리할 것을 권장합니다. 반환 값은 숫자입니다: <ul style="margin:0"><li/>0: 정상<li/>1-8: 각각 hotScore에서 adScore까지 다음 매개변수의 유형별 순서를 나타냅니다. 예: 1-포르노, 6-욕설, 8-광고, 기타 등등</ul> |
| score | 필수 입력     | Array | type 해당 평점 |
| hotScore                    | 필수 입력     | Number | 선정적 이미지 평점 |
| pornScore | 필수 입력     | Number | 음란성 이미지 평점 |
| illegalScore | 필수 입력     | Number | 불법 이미지 평점 |
| polityScore | 필수 입력     | Number | 정치 관련 이미지 평점 |
| terrorScore | 필수 입력     | Number | 테러 관련 이미지 평점 |
| abuseScore | 필수 입력     | Number | 욕설 관련 이미지 평점 |
| teenagerScore | 필수 입력     | Number | 청소년에게 부적절한 이미지 평점 |
| adScore | 필수 입력     | Number | adScore 이미지 평점 |
| ocrMsg | 선택 사항     | string | 이미지의 OCR 식별 정보(존재할 경우) |
| suggestion | 필수 입력     | string | 권장 값, 선택 가능 값: <ul style="margin:0"><li/>Block: 차단<li/>Review: 재심사<li/>Pass: 정상</ul>     |
| label | 필수 입력     | string                | 매개변수 type의 반환 유형 값에 대한 보충 텍스트 설명입니다. 예: 반환 값 **0**은 Normal로 보충 설명, 반환 값 **6**은 Abuse로 보충 설명, 반환 값 **8**은 Ad 로 보충 설명됨. |
| subLabel | 필수 입력     | string | 서브 태그 이름, 서브 태그 미스 시, 공백 반환             |
| labelResults | 선택 사항    | Array of [LabelResult](#labelresult)  | 음란물, 선정적인 내용, 폭력, 불법 규정 위반 등 심사 결과를 포함한 분류 점검 모델 심사 결과 |
| objectResults | 선택 사항     | Array of [ObjectResult](#objectresult) | 정치적 내용, 광고 마크, QR 코드 등 심사 정보를 포함한 점검 모델 심사 결과 |
| ocrResults | 선택 사항     | Array of [OcrResult](#ocrresult) | OCR 텍스트 관련 정보 및 텍스트 심사 상세 결과를 포함한 OCR 텍스트 심사 결과 |
| libResults | 선택 사항     | Array of [LibResult](#libresult) | 리스크 이미지 라이브러리 심사 결과 |
| screenshotTime | 필수 입력     | Number | 화면 캡처 시간 |
| sendTime | 필수 입력     | Number | 요청 발송 시간, UNIX 타임스탬프 |
| similarScore | 선택 사항     | Number | 이미지 유사도 평점 |
| stream_param | 선택 사항     | String | 푸시 스트림 매개변수 |
| app | 선택 사항     | String | 푸시 스트림 도메인 |
| appid | 선택 사항     | Number | 비즈니스 ID |
| appname | 선택 사항     | String | 푸시 스트림 path 경로 |

 

#### LabelResult
분류 모델 히트 결과.

| 이름   | 유형                 | 설명                                                     |
| ---------- | ------------------------ | ------------------------ |
| Scene      | String                                       | 모델 식별 시나리오 결과 반환, 예: 광고, 음란물, 유해 콘텐츠 등 시나리오.      |
| Suggestion | String                                       | 현재 악성 태그의 후속 작업에 대한 권장 사항을 반환합니다. 판정 결과를 받은 후, 반환값은 시스템에서 권장하는 후속 작업을 의미합니다. 비즈니스 상황에 따라 필요하면 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값: <ul style="margin:0"><li/>Block: 차단 권장<li/>Review: 수동 재심사 권장<li/>Pass: 통과 권장</ul> |
| label | String                                       | 콜백 메시지 매개변수 type의 반환 유형 값에 대한 보충 텍스트 설명입니다. 예: 반환 값 **0**은 Normal로, 반환 값 **6**은 Abuse로, 반환 값 **8**은 Ad로 보충 설명됨. |
| SubLabel   | String | 서브 태그 이름                                                   |
| Score      | Integer | 해당 태그 모델 히트 점수                                         |
| Details    | Array of [LabelDetailItem](#labeldetailitem) | 분류 모델의 서브 태그 히트 상세 결과                                   |

#### LabelDetailItem

분류 모델 서브 태그 히트 결과.

| 이름 | 유형 | 설명                    |
| -------- | -------- | --------------------------- |
| Id       | Integer  | 시리얼 넘버                        |
| Name     | String   | 서브 태그 이름                  |
| Score    | Integer  | 서브 태그 점수, 점수 범위 0점 - 100점|


#### ObjectResult

엔터티 점검 상세 결과.

| 이름   | 유형              | 설명              |
| ---------- | --------------------- | --------------------- |
| Scene      | String                                 | 식별 엔터티 시나리오 결과 반환, 예: QR 코드, logo, 이미지 OCR 등 시나리오. |
| Suggestion | String                                 | 현재 악성 태그의 후속 작업에 대한 권장 사항을 반환합니다. 판정 결과를 받은 후, 반환값은 시스템에서 권장하는 후속 작업을 의미합니다. 비즈니스 상황에 따라 필요하면 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값: <ul style="margin:0"><li/>Block: 차단 권장<li/>Review: 수동 재심사 권장<li/>Pass: 통과 권장</ul> |
| label | String                                 | 콜백 메시지 매개변수 type의 반환 유형 값에 대한 추가 텍스트 설명입니다. 예: 반환 값 **0**은 Normal로, 반환 값 **6**은 Abuse로, 반환 값 **8**은 Ad로 보충 설명됨. |
| SubLabel   | String | 서브 태그 이름 |
| Score      | Integer | 해당 시나리오 모델의 서브 태그 히트 점수, 점수 범위 0점 - 100점 |
| Names      | Array of String       | 엔터티 이름 리스트 |
| Details    | Array of [ObjectDetail](#objectdetail) | 점검 상세 결과 |

#### ObjectDetail

점검 상세 결과로 시나리오가 정치, 정치적 인물, 광고 마크, QR 코드 및 안면 속성과 관련된 내용이면 모델 점검 타깃창의 태그 이름, 태그값, 태그 점수 및 점검창의 위치 정보를 표시합니다.

| 이름 | 유형 | 설명 |
| -------- | -------- | -------- |
| Id       | Integer  | 시리얼 넘버  |
| Name     | String   | 태그 이름  |
| Value    | String   | 태그값: <ul style="margin:0"><li/>시나리오가 Ad일 때, URL 주소를 표시합니다. 예를 들어 Name이 QrCode일 때, Value 값은 `http//abc.com/aaa`<br><li/>시나리오가 FaceAttribute일 때는 안면 속성 정보를 의미합니다. 예를 들어 Name이 Age일 때, Value 값은 `18`입니다. </ul>|
| Score    | Integer  | 점수, 점수 범위 0점 - 100점 |
| Location | [Location](#location) | 점검창 좌표 |

#### Location

좌표.

| 이름 | 유형 | 설명         |
| -------- | -------- | ---------------- |
| X        | Float    | 왼쪽 상단 가로 좌표     |
| Y        | Float    | 왼쪽 상단 세로 좌표     |
| Width    | Float    | 폭             |
| Height   | Float    | 높이             |
| Rotate   | Float    | 점검창의 회전 각도 |

#### OcrResult

OCR 결과 점검 상세 내용.

| 이름   | 유형               | 설명                |
| ---------- | ---------------------- | ---------------------- |
| Scene      | String                                   | 식별 시나리오 표시, 기본 값 OCR(이미지 OCR 식별).              |
| Suggestion | String                                   | 우선순위가 가장 높은 악성 태그에 상응하는 후속 작업에 대한 권장 사항을 반환합니다. 판정 결과를 받은 후, 반환값은 시스템에서 권장하는 후속 작업을 의미합니다. 비즈니스 상황에 따라 필요하면 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값: <ul style="margin:0"><li/>Block: 차단 권장<li/>Review: 수동 재심사 권장<li/>Pass: 통과 권장</ul> |
| label | String                                   | 콜백 메시지 매개변수 type의 반환 유형 값에 대한 추가 텍스트 설명입니다. 예: 반환 값 **0**은 Normal로, 반환 값 **6**은 Abuse로, 반환 값 **8**은 Ad로 보충 설명됨. |
| SubLabel   | String | 서브 태그 이름 |
| Score      | Integer | 해당 시나리오 모델의 서브 태그 히트 점수, 점수 범위 0점 - 100점 |
| Text       | String | 텍스트 콘텐츠 |
| Details    | Array of [OcrTextDetail](#ocrtextdetail) | OCR 상세 결과 |


#### OcrTextDetail
OCR 텍스트 상세 결과.

| 이름 | 유형        | 설명                                                     |
| -------- | --------------- | --------------- |
| Text     | String                | OCR 식별 텍스트 콘텐츠 반환(OCR 텍스트 식별**5000 바이트 이내**로 제한). |
| label | String                | 콜백 메시지 매개변수 type의 반환 유형 값에 대한 추가 텍스트 설명입니다. 예: 반환 값 **0**은 Normal로, 반환 값 **6**은 Abuse로, 반환 값 **8**은 Ad로 보충 설명됨. |
| Keywords | Array of String | 해당 태그에 히트된 키워드 |
| Score    | Integer         | 해당 태그 모델의 히트 점수, 점수 범위 0점 - 100점 |
| Location | [Location](#location) | OCR 텍스트 좌표 위치 |


#### LibResult
블랙/화이트 라이브러리 상세 내용.

| 이름   | 유형           | 설명                                                     |
| ---------- | ------------------ | ------------------------------------------------------------ |
| Scene      | String                           | 모델의 시나리오 식별 결과 표시, 기본값 Similar.                 |
| Suggestion | String                           | 후속 작업에 대한 권장 사항을 반환합니다. 판정 결과를 받은 후, 반환값은 시스템에서 권장하는 후속 작업을 의미합니다. 비즈니스 상황에 따라 필요하면 위반 유형과 권장값별로 처리할 것을 권장합니다. 반환값: <ul style="margin:0"><li/>Block: 차단 권장<li/>Review: 수동 재심사 권장<li/>Pass: 통과 권장</ul> |
| label | String                           | 콜백 메시지 매개변수 type의 반환 유형 값에 대한 추가 텍스트 설명입니다. 예: 반환 값 **0**은 Normal로, 반환 값 **6**은 Abuse로, 반환 값 **8**은 Ad로 보충 설명됨. |
| SubLabel   | String             | 서브 태그 이름 |
| Score      | Integer            | 이미지 인덱스 모델 식별 점수, 점수 범위 0점 - 100점 |
| Details    | Array of [LibDetail](#libdetail) | 블랙/화이트 라이브러리 결과 상세 내용 |

#### LibDetail
사용자 정의 라이브러리/블랙/화이트 라이브러리 상세 내용.

| 이름 | 유형 | 설명                                                     |
| -------- | -------- | ------------------------------------------------------------ |
| Id       | Integer  | 시리얼 넘버                                                         |
| ImageId  | String   | 이미지ID                                                       |
| label | String  | 콜백 메시지 매개변수 type의 반환 유형 값에 대한 추가 텍스트 설명입니다. 예: 반환 값 **0**은 Normal로, 반환 값 **6**은 Abuse로, 반환 값 **8**은 Ad로 보충 설명됨. |
| Tag      | String   | 사용자 정의 태그                                                   |
| Score    | Integer  | 모델 식별 점수, 점수 범위 0점 - 100점                               |



### 콜백 메시지 예시
<dx-codeblock>
::: HTTPbody  json
{
        "ocrMsg": "",
        "type": [1],
        "socre": 99,
        "hotScore": 0,
        "pornScore": 99,
        "screenshotTime": 1610640000,
        "level": 0,
        "img": "http://1.1.1.1/download/porn/test.jpg",
        "abductionRisk": [],
        "faceDetails": [],
        "sendTime": 1615859827,
        "illegalScore": 0,
        "polityScore": 0,
        "similarScore": 0,
        "terrorScore": 0,
        "abuseScore": 0,
        "teenagerScore": 0,
        "adScore": 0,
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







