
라이브 방송 음란물 감지 활성화 시에는 먼저 라이브 방송 화면 캡처 기능을 활성화해야 하며, [LVB 콘솔](https://intl.cloud.tencent.com/zh/document/product/267/31072) 또는 라이브 방송 음란물 감지 화면 캡처 API를 통해 활성화할 수 있습니다. 본 문서에서는 라이브 방송 음란물 감지 화면 캡처 API를 통해 음란물 감지 기능을 실현하는 방법을 소개합니다.

## 라이브 방송 음란물 감지 활성화
라이브 방송 음란물 감지는 라이브 방송 화면 캡처를 기반으로 합니다. 따라서 해당 기능을 활성화하기 위해서는 반드시 화면 캡처 기능을 활성화해야 합니다. 자세한 작업 방법은 다음과 같습니다.

### 1. 음란물 감지 기능이 활성화된 라이브 방송 화면 캡처 템플릿 생성
[CreateLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30834)을 호출하고 PornFlag = 1 설정을 통해 음란물 감지 기능이 활성화된 라이브 방송 화면 캡처 템플릿을 생성합니다.

### 2. 음란물 감지 기능이 활성화된 라이브 방송 화면 캡처 규칙 생성
[CreateLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30835)을 호출하고, 음란물 감지 기능이 활성화된 라이브 방송 화면 캡처 규칙을 생성합니다. 1단계에서 생성한 라이브 방송 화면 캡처 템플릿 ID를 음란물 감지가 필요한 라이브 방송과 AppId, DomainName, AppName, StreamName으로 연결합니다.

### 3. 라이브 방송 시작 시 음란물 감지 기능 활성화
음란물 감지 기능이 활성화된 라이브 방송 화면 캡처 규칙을 생성하면 새로 시작되는 라이브 방송에 자동으로 음란물 감지 기능이 활성화됩니다. 현재 라이브 방송 중인 라이브 방송 스트림에 대해 음란물 감지 기능을 활성화하고 싶은 경우 해당 라이브 방송을 중지하고 다시 시작해야만 적용됩니다.

## 라이브 방송 음란물 감지 결과 획득
라이브 방송 음란물 감지 기능을 활성화한 후 음란물 감지 콜백 템플릿에 등록한 콜백 도메인을 설정할 수 있으며, LVB 백그라운드에서 음란물 감지 결과를 콜백합니다.
>!기본적으로 의심되는 결과만 콜백하며 정상 결과는 콜백하지 않습니다.

### 1. 라이브 방송 음란물 감지 콜백 템플릿 생성
[CreateLiveCallbackTemplate](https://intl.cloud.tencent.com/document/product/267/30815)을 호출하고 PornCensorshipNotifyUrl 매개변수를 사용자의 도메인으로 설정하여 라이브 방송 음란물 감지 콜백 템플릿을 생성합니다.
### 2. 라이브 방송 음란물 감지 콜백 규칙 생성

[CreateLiveCallbackRule](https://intl.cloud.tencent.com/document/product/267/30816)을 호출하고, 음란물 감지 기능이 활성화된 라이브 방송 화면 캡처 규칙을 생성합니다. 1단계에서 생성한 라이브 방송 화면 캡처 템플릿 ID를 음란물 감지 콜백이 필요한 라이브 방송과 AppId, DomainName, AppName으로 연결합니다.

### 3. 음란물 감지 결과 획득
라이브 방송 백그라운드에서 음란물 감지 결과를 HTTP POST 요청을 통해 사용자가 등록한 도메인으로 발송합니다. 음란물 감지 결과는 JSON 포맷으로 HTTP Body에 저장되며, type 필드를 통해서만 라이브 방송에 음란물 관련 콘텐츠가 있는지 판단할 수 있습니다.
>!이미지의 `type`을 이용해 음란물 이미지를 판단하는 것을 권장합니다. 시스템에서 감지하는 이미지 판정은 100%의 정확도를 보장하지 못하며 소량의 이미지는 음란물 의심으로 식별되거나 식별 결과가 맞지 않을 수 있습니다. 사람이 2차 확인하는 것을 권장합니다.  

#### 완전한 프로토콜은 다음과 같습니다.
| **매개변수** | **필수 여부** | **데이터 유형** | **설명** |
| --- | --- | --- | --- |
| tid | 필수 | Number | 알람 정책 ID, 비디오 콘텐츠 알람: 20001 |
| streamId | 선택  | String | 스트림 이름 |
| channelId | 선택  | string | 채널 ID |
| img | 필수 | string | 알람 이미지 링크 |
| type | 필수 | Array | 이미지 유형, 0: 일반 이미지, 1: 음란물 이미지, 2: 성적 이미지, 3: 정치 관련 이미지, 4: 불법 이미지, 5: 테러 관련 이미지, 6 - 9: 기타 다른 이미지 |
| confidence | 필수 | Number | 음란물 관련 신뢰도, 범위 0-100. normalScore, hotScore, pornScore 종합 평점 |
| normalScore | 필수 | Number | 일반 이미지 평점 |
| hotScore | 필수 | Number | 성적 이미지 평점 |
| pornScore | 필수 | Number | 음란물 이미지 평점 |
| level | 선택  | Number | 이미지 등급 |
| ocrMsg | 선택  | string | 이미지 OCR 식별 정보(존재하는 경우) |
| screenshotTime | 필수 | Number | 화면 캡처 시간 |
| sendTime | 필수 | Number | 요청 발송 시간, UNIX 타임스탬프 |
| abductionRisk | 선택  | Array | AbductionRisk 구성이 포함된 배열 |
| faceDetails | 선택 | Array | 얼굴 속성 faceDetail 구성이 포함된 배열 |
| gameDetails | 선택 | Object |  게임 상세 정보  |
| polityScore | 선택 | Number | 정치 관련 이미지 평점|
| illegalScore |  선택 | Number  | 불법 이미지 평점 |
| terrorScore  | 선택 | Number  | 테러 관련 이미지 평점|
| similarScore  | 선택 | Number | 이미지 유사성 평점|
| stream_param  | 선택 | String | 푸시 스트림 매개변수 |
| app  | 선택 | String | 푸시 스트림 도메인 |
| appid  | 선택 | Number | 비즈니스 ID  |
| appname  | 선택 | String | 푸시 스트림 path 경로  |



#### AbductionRisk 소개:

| **매개변수** | **필수 여부** | **데이터 유형** | **설명** |
| --- | --- | --- | --- |
| level | 필수 | Number | 리스크 등급 범위 0 - 4, 숫자가 클수록 리스크가 높으며 3과 4는 악성이므로 처리 권장 |
| type | 필수 | Number | 리스크 유형, 20002: 음란물  |

#### faceDetail 설명:
| **매개변수 이름** | **필수 여부** | **유형** | **설명** |
| --- | --- | --- | --- |
| gender | 선택 | Number | 성별 [0(female) - 100(male)] |
| age | 선택 | Number | 연령 |
| expression | 선택 | Number | 웃음 [0(normal) - 50(smile) - 100(laugh)] |
| beauty | 선택 | Number | 매력 [0 - 100] |
| x | 선택 | Number | 얼굴 프레임 왼쪽 상단 x |
| y | 선택 | Number | 얼굴 프레임 왼쪽 상단 y |
| width | 선택 | Number | 얼굴 프레임 너비 |
| height | 선택 | Number | 얼굴 프레임 높이 |

#### gameDetails 설명:
| **매개변수 이름** | **필수 여부** | **유형** | **설명** |
| --- | --- | --- | --- |
| battlegrounds | 선택 | Object | 배틀그라운드 정보 |
| gameList | 선택 | Array | 게임 리스트 |

#### gameList 설명:

| **매개변수 이름** | **필수 여부** | **유형** | **설명** |
| --- | --- | --- | --- |
| name | 선택 | String | 게임 이름 |
| confidence | 선택 | Number | 확률 |


#### 요청 예시
HTTP Body：
```
{
    "ocrMsg":"",
		
    "type":[2],
		
    "confidence":0,
		
    "normalScore":2,
		
    "hotScore":97,
		
    "pornScore":0,
		
    "screenshotTime":1575513174,
		
    "level":0,
		
    "img":"http://test-10000.cos.ap-shanghai.myqcloud.com/2019-12-05/teststream-screenshot-10-32-54-960x540.jpg",
		
    "abductionRisk":[ ],
		
    "faceDetails":[ ],
		
    "sendTime":1575513176,
		
    "illegalScore":0,
		
    "polityScore":0,
		
    "similarScore":0,
		
    "terrorScore":0,
		
    "tid":20001,
		
    "streamId":"teststream",
		
    "channelId":"teststream",
		
    "stream_param":"txSecret=40f38f69f574fd51126c421a3d96c374&txTime=5DEBEC80",
		
    "app":"testlive.myqcloud.com",
		
    "appname":"live",
		
    "appid":10000
}  
```

## 라이브 방송 음란물 감지 비활성화

라이브 방송 음란물 감지를 비활성화는 화면 캡처 규칙 삭제 또는 화면 캡처 템플릿 수정을 통해 실현됩니다. 모든 삭제 및 수정 작업은 새로운 라이브 방송에만 적용되며, 이미 시작된 라이브 방송에 대한 음란물 감지 기능을 비활성화하고 싶은 경우 라이브 방송을 중지하고 다시 시작해야만 적용됩니다.

### 1. 음란물 감지 화면 캡처 규칙 삭제를 통한 비활성화

[DeleteLiveSnapshotRule](https://intl.cloud.tencent.com/document/product/267/30833)을 호출하고 템플릿 ID에서 DomainName, AppName, StreamName의 해당 라이브 방송 화면 캡처 규칙을 삭제합니다.

### 2. 음란물 감지 화면 캡처 템플릿 삭제 또는 수정을 통한 비활성화

[ModifyLiveSnapshotTemplate](https://intl.cloud.tencent.com/document/product/267/30828)을 호출하고 라이브 방송 템플릿의 음란물 감지값을 0으로 수정합니다.
