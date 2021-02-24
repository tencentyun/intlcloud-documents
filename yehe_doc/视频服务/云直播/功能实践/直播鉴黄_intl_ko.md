
라이브 방송 음란물 감지를 활성화하려면 먼저 라이브 방송 화면 캡처 기능을 활성화해야 합니다. 이는 [LVB 콘솔](https://intl.cloud.tencent.com/document/product/267/31072) 또는 라이브 방송 화면 캡처 및 음란물 감지 API를 통해 실현할 수 있습니다. 본 문서에서는 라이브 방송 화면 캡처 및 음란물 감지 API를 통해 라이브 방송 음란물 감지 기능을 사용하는 방법을 설명합니다.

## 라이브 방송 음란물 감지 활성화
라이브 방송 음란물 감지는 라이브 방송 화면 캡처를 기반으로 하므로, 라이브 방송 음란물 감지 기능을 사용하려면 먼저 라이브 방송 화면 캡처 기능을 활성화해야 합니다. 다음은 구체적인 활성화 방법입니다.

### 1. 음란물 감지 기능이 적용된 라이브 방송 화면 캡처 템플릿 생성
[라이브 방송 화면 캡처 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/30834)을 호출한 후에 PornFlag = 1을 설정하여 음란물 감지 기능이 적용된 라이브 방송 화면 캡처 템플릿을 생성합니다.

### 2. 음란물 감지 기능이 적용된 라이브 방송 화면 캡처 규칙 생성
[라이브 방송 화면 캡처 규칙 생성](https://intl.cloud.tencent.com/document/product/267/30835)을 호출해 음란물 감지 기능이 적용된 라이브 방송 화면 캡처 규칙을 생성한 후, 1단계에서 생성한 라이브 방송 화면 캡처 템플릿 ID를 음란물 감지 기능이 필요한 라이브 방송 AppId, DomainName, AppName, StreamName 차원에 연결합니다.

### 3. 라이브 방송 시작 후 음란물 감지 시작
음란물 감지 규칙이 적용된 라이브 방송 화면 캡처 규칙을 생성하고 나면 새로 시작되는 라이브 방송에 자동으로 음란물 감지 기능이 적용됩니다. 진행 중인 라이브 방송 스트리밍에서 음란물 감지 기능을 활성화하려면 방송을 정지하고 다시 시작해야 합니다.

## 라이브 방송 음란물 감지 결과 획득
라이브 방송 음란물 감지 기능을 활성화하고 나면 음란물 감지 콜백 템플릿에서 접속할 콜백 도메인을 설정할 수 있습니다. 이를 통해 LVB 백그라운드에서 음란물 감지 결과가 귀하에게 콜백됩니다.
>! 기본적으로 의심스러운 결과만 콜백하며, 정상적인 결과는 콜백하지 않습니다.

### 1. 라이브 방송 음란물 감지 콜백 템플릿 생성
[라이브 방송 콜백 템플릿 생성](https://intl.cloud.tencent.com/document/product/267/30815)을 호출한 후에 PornCensorshipNotifyUrl 매개변수를 귀하의 도메인으로 설정하여 라이브 방송 음란물 감지 콜백 템플릿을 생성합니다.
### 2. 라이브 방송 음란물 감지 콜백 규칙 생성

[라이브 방송 콜백 규칙 생성](https://intl.cloud.tencent.com/document/product/267/30816)을 호출해 음란물 감지 기능이 적용된 라이브 방송 화면 캡처 규칙을 생성한 후, 이전 단계에서 생성한 라이브 방송 화면 캡처 템플릿 ID를 음란물 감지 콜백이 필요한 라이브 방송 AppId, DomainName, AppName 차원에 연결합니다.

### 3. 음란물 감지 결과 획득
라이브 방송 백그라운드에서는 음란물 감지 결과를 HTTP POST 요청을 통해 귀하가 접속한 도메인으로 전송합니다. 음란물 감지 결과는 HTTP Body에 JSON 포맷으로 저장되므로, 해당 라이브 방송의 음란물 여부는 type 필드에서만 확인할 수 있습니다.
>!이미지를 사용한 `type`으로 음란물 판정을 진행할 것을 권장합니다. 검사 시스템의 정확도가 100%를 달성할 수는 없기 때문에, 일부 이미지가 음란물 의심 판정을 받거나 잘못된 식별 결과가 나올 수 있습니다. 육안으로 2차 확인 작업을 진행할 것을 권장합니다.  

#### 전체 프로토콜은 다음과 같습니다.
| 매개변수 | 필수 입력 여부 | 데이터 유형 | 설명 |
| --- | --- | --- | --- |
| tid | 필수 입력 | Number | 알람 정책 ID, 비디오 콘텐츠 알람: 20001 |
| streamId | 선택 사항  | String | 스트림 이름 |
| channelId | 선택 사항  | string | 채널 ID |
| img | 필수 입력 | string | 알람 이미지 링크 |
| type | 필수 입력 | Array | 이미지 유형, 0: 일반 이미지, 1~5: 부적절한 이미지 |
| confidence | 필수 입력 | Number | 음란물 연관 수치 신뢰도, 범위 0~100: normalScore, hotScore, pornScore로 이루어진 종합 평점 |
| normalScore | 필수 입력 | Number | 일반 이미지일 경우의 평점 |
| hotScore | 필수 입력 | Number | 성적인 이미지일 경우의 평점 |
| pornScore | 필수 입력 | Number | 음란성 이미지일 경우의 평점 |
| level | 선택 사항  | Number | 이미지의 등급 |
| ocrMsg | 선택 사항  | string | 이미지의 OCR 식별 정보(존재할 경우) |
| screenshotTime | 필수 입력 | Number | 화면 캡처 시간 |
| sendTime | 필수 입력 | Number | 요청 발송 시간, UNIX 타임스탬프 |
| gameDetails | 선택 사항 | Object |  게임 상세 정보  |
| similarScore  | 선택 사항 | Number | 이미지 유사도 평점|
| stream_param  | 선택 사항 | String | 푸시 스트림 매개변수 |
| app  | 선택 사항 | String | 푸시 스트림 도메인 |
| appid  | 선택 사항 | Number | 비즈니스 ID  |
| appname  | 선택 사항 | String | 푸시 스트림 path 경로  |


#### gameDetails 설명:
| **매개변수 이름** | **필수 입력 여부** | **유형** | **설명** |
| --- | --- | --- | --- |
| battlegrounds | 선택 사항 | Object | PUBG 정보 |
| gameList | 선택 사항 | Array | 게임 리스트 |

#### gameList 설명:

| **매개변수 이름** | **필수 입력 여부** | **유형** | **설명** |
| --- | --- | --- | --- |
| name | 선택 사항 | String | 게임 이름 |
| confidence | 선택 사항 | Number | 확률 |


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
            
    "sendTime":1575513176,
            
    "similarScore":0,
            
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

라이브 방송 음란물 감지는 화면 캡처 규칙을 삭제하거나 화면 캡처 템플릿을 수정해 비활성화할 수 있습니다. 삭제 또는 수정 작업은 새로운 라이브 방송에만 적용됩니다. 이미 시작된 라이브 방송에 적용 중인 음란물 감지 기능을 비활성화하려면 반드시 방송을 중지한 다음 다시 실행해야 합니다.

### 1. 음란물 감지 화면 캡처 규칙 삭제를 통한 방법

[라이브 방송 화면 캡처 규칙 삭제](https://intl.cloud.tencent.com/document/product/267/30833)를 호출한 후 템플릿 ID에서 DomainName, AppName, StreamName의 해당 라이브 방송 화면 캡처 규칙을 삭제합니다.

### 2. 음란물 감지 화면 캡처 템플릿 삭제 또는 수정을 통한 방법

[라이브 방송 화면 캡쳐 템플릿 수정](https://intl.cloud.tencent.com/document/product/267/30828)을 호출한 후에 라이브 방송 템플릿의 음란물 감지 태그를 0으로 수정합니다.
