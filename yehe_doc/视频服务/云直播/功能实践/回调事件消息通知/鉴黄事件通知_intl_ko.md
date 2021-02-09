라이브 방송 음란물 감지는 라이브 방송 스트리밍 중에 음란물로 의심되는 화면을 영상으로 실시간 캡처하여 COS에 이미지 스토리지를 생성합니다. 음란물 감지 콜백은 문제 이미지 유형, 등급 판정, 화면 캡처 시간 등 라이브 방송 음란물 이미지 정보를 푸시하는 데 쓰입니다. 콜백 템플릿에서 음란물 감지 콜백 정보를 받을 서버 주소를 설정하고 템플릿과 푸시 스트리밍 도메인을 연결해야 합니다. 라이브 방송 스트리밍에서 음란물 감지 이벤트를 트리거하면 Tencent Cloud Live Video Broadcasting(LVB) 백그라운드가 음란물 관련 이미지 정보를 설정한 수신 서버에 콜백합니다.

본문은 음란물 감지 콜백 이벤트가 트리거된 후 Tencent Cloud LVB에서 사용자에게 보내는 콜백 메시지 공지 필드를 설명합니다.

## 주의 사항
- 본 문서를 읽기 전 Tencent Cloud LVB 콜백 기능 설정 방법과 콜백 메시지 수신 방법을 확인하십시오. 자세한 사항은 [이벤트 공지 수신 방법](https://cloud.tencent.com/document/product/267/32744)을 참고하십시오.
- 기본적으로 라이브 방송 음란물 감지는 의심스러운 결과를 콜백하며 정상적인 결과는 콜백하지 않습니다.
- 이미지의 [type](#type)을 이용해 음란물　이미지인지 판단하십시오. 점검 시스템은 100% 정확하지 않기 때문에 소량의 이미지가 음란물　이미지로 의심되거나 잘못 인식된 결과가 있을 수 있습니다. 실제 응용 시나리오 판단 여부는 수동으로 2차 확인이 필요합니다.

## 화면 캡처 이벤트 매개변수 설명

### 이벤트 유형 매개변수

| 이벤트 유형 | 필드값 설명           |
| :------- | :------------- |
| 라이브 방송 음란물 감지 | event_type = 317 |

### 콜백 공용 매개변수

<table>
<tr><th>필드 이름</th><th>유형</th><th>설명</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>만료 시간 및 이벤트 공지 서명 만료 UNIX 타임스탬프<ul style="margin:0"><li>기본적으로 Tencent Cloud의 메시지 공지 만료 시간은 10분입니다. 메시지 공지에서 t 값으로 지정된 시간이 경과한 경우 무효한 공지라고 판단하며 이로써 네트워크 리플레이 공격을 방지할 수 있습니다.<li>t의 포맷은 10진법 UNIX 타임스탬프로 즉, 1970년 01월 01일(UTC/GMT의 자정)부터 경과한 초의 값입니다.</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>이벤트 공지 보안 서명 sign = MD5(key + t)<br>설명: Tencent Cloud는 암호화 <a href="#key">key</a>와 t의 문자열을 조합하여 MD5 계산으로 sign 값을 얻고 이를 공지 정보에 포함합니다. 백그라운드 서버가 공지 정보를 수신하면 똑같은 알고리즘으로 sign의 정확도 여부를 확인하고 그 정보가 실제로 Tencent Cloud 백그라운드에서 온 것인지 확인할 수 있습니다.</td>
</tr></table>

>? <span id="key"></span>key는 [이벤트 센터]>[LVB 콜백](https://console.cloud.tencent.com/live/config/callback)의 콜백 키이며 주로 인증하는 데 쓰입니다. 데이터 정보 보안을 위해 작성을 권장합니다.
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### 콜백 메시지 매개변수

| **매개변수**       | **필수 여부** | **데이터 유형** | **설명**                                                     |
| :------------- | :----------- | :----------- | :----------------------------------------------------------- |
| tid            | 필수         | Number       | 알람 정책 ID, 비디오 콘텐츠 알람: 20001                             |
| streamId       | 선택         | String       | 스트림 이름                                                       |
| channelId      | 선택         | string       | 채널 ID                                                      |
| img            | 필수         | string       | 알람 이미지 링크                                                 |
| <span id="type"></span> type          | 필수         | Array        | 이미지 유형, 0: 일반　이미지, 1: 음란물　이미지, 2: 성적 이미지, 3: 정치 관련 이미지, 4: 불법 이미지, 5: 테러 관련 이미지, 6 - 9: 기타 다른 이미지 |
| confidence     | 필수         | Number       | 음란물 관련 신뢰도, 범위 0-100; normalScore, hotScore, pornScore의 종합 평점 |
| normalScore    | 필수         | Number       | 일반 이미지인 경우의 평점                                         |
| hotScore       | 필수         | Number       | 성적 이미지인 경우의 평점                                         |
| pornScore      | 필수         | Number       | 음란물 이미지인 경우의 평점                                         |
| level          | 선택         | Number       | 이미지 등급                                                   |
| ocrMsg         | 선택         | string       | 이미지 OCR 인식 정보(존재하는 경우)                              |
| screenshotTime | 필수         | Number       | 화면 캡처 시간                                                     |
| sendTime       | 필수         | Number       | 요청 발송 시간, UNIX 타임스탬프                                    |
| abductionRisk  | 선택         | Array        | [AbductionRisk](#abductionrisk) 구조를 포함하는 배열                            |
| faceDetails    | 선택         | Array        | 얼굴 속성 [faceDetail](#facedetail) 구조를 포함하는 배열                     |
| [gameDetails](#gamedetails)    | 선택         | Object       | 게임 세부 사항 정보                                                 |
| polityScore    | 선택         | Number       | 정치 관련 이미지 평점                                         |
| illegalScore   | 선택         | Number       | 불법 이미지 평점                                         |
| terrorScore    | 선택         | Number       | 테러 관련 이미지 평점                                         |
| similarScore   | 선택         | Number       | 이미지 유사성 평점                                               |
| stream_param   | 선택         | String       | 푸시 스트리밍 매개변수                                                     |
| app            | 선택         | String       | 푸시 스트리밍 도메인                                                     |
| appid          | 선택         | Number       | 비즈니스 ID                                                      |
| appname        | 선택         | String       | 푸시 스트리밍 path 경로                                               |

#### AbductionRisk

| **매개변수** | **필수 여부** | **데이터 유형** | **설명** |
| :------- | :----------- | :----------- | :----------------------------------------------------------- |
| level    | 필수         | Number       | 위험 등급 범위 0 - 4, 숫자가 클수록 위험도가 큼, 3과 4는 악성을 나타내므로 프로세스 진행을 권장함 |
| type     | 필수         | Number       | 위험 유형, 20002: 음란성                                        |

#### faceDetail

| **매개변수 이름** | **필수 여부** | **유형** | **설명**                                  |
| :----------- | :----------- | :------- | :---------------------------------------- |
| gender       | 선택         | Number   | 성별 [0(female) - 100(male)]              |
| age          | 선택         | Number   | 연령                                      |
| expression   | 선택         | Number   | 스마일 [0(normal) - 50(smile) - 100(laugh)] |
| beauty       | 선택         | Number   | 매력 [0 - 100]                            |
| x            | 선택         | Number   | 얼굴 좌측 상단 모서리 x                            |
| y            | 선택         | Number   | 얼굴 우측 상단 모서리 y                            |
| width        | 선택         | Number   | 얼굴 너비                                |
| height       | 선택         | Number   | 얼굴 길이                                |

#### gameDetails

| **매개변수 이름** | **필수 여부** | **유형** | **설명** |
| :------------ | :----------- | :------- | :----------- |
| battlegrounds | 선택         | Object   | PUBG 정보 |
| [gameList](#gamelist)      | 선택         | Array    | 게임 리스트     |

#### gameList

| **매개변수 이름** | **필수 여부** | **유형** | **설명** |
| :----------- | :----------- | :------- | :------- |
| name         | 선택         | String   | 게임 이름 |
| confidence   | 선택         | Number   | 확률     |

### 콜백 메시지 예시

HTTP Body：

```
{
    "event_type":317,
	
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




