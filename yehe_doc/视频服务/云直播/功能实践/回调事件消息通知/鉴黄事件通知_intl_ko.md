라이브 방송 음란물 감지는 라이브 방송 스트리밍에서 선정성이 있는 수상한 화면을 실시간으로 캡처하고, 생성된 이미지 파일을 COS에 저장합니다. 음란물 감지 콜백은 문제 이미지의 소속 유형, 등급 평가, 화면 캡처 시간과 같은 라이브 방송 음란물 감지 이미지 정보를 푸시하는 데 사용됩니다. 콜백 템플릿에서 음란물 감지 콜백 메시지를 수신할 서버 주소를 설정하고, 해당 템플릿을 푸시 스트림 도메인과 연결해야 합니다. 라이브 방송 스트리밍에서 음란물 감지 이벤트가 트리거 될 경우, 음란물 이미지 정보를 Tencent Cloud LVB 백그라운드에서 귀하가 설정한 수신용 서버로 콜백합니다.

본 문서에서는 음란물 감지 콜백 이벤트 발생 시 Tencent Cloud LVB가 사용자의 콜백 메시지 공지 필드로 발송하는 과정을 설명합니다.

## 주의사항
- Tencent Cloud LVB의 콜백 기능 설정 방법을 이해하신 후 본 문서를 읽으실 것을 권장합니다. 콜백 메시지를 수신하는 방법은 [이벤트 공지를 수신하는 방법](https://intl.cloud.tencent.com/document/product/267/38080)을 참조 바랍니다.
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
<td>만료 시간, 이벤트 공지 서명 만료 UNIX 타임스탬프입니다. <ul style="margin:0"><li>Tencent Cloud 메시지 공지의 기본 만료 시간은 10분입니다. 메시지 공지의 t값으로 지정된 시간이 만료되었을 경우, 해당 공지를 무효라고 판정할 수 있으며 나아가 네트워크 리플레이 공격을 방지할 수 있습니다. <li>t의 형식은 10진법 UNIX 타임스탬프입니다. 즉, 1970년 01월 01일(UTC/GMT의 자정)부터 경과한 초의 수입니다. </ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>이벤트 공지 보안 서명은 sign = MD5(key + t)입니다. <br>설명: Tencent Cloud는 암호화된 <a href="#key">key</a>와 t를 통해 문자열을 조합한 후, MD5를 통해 sign값을 계산하여 이를 공지 메시지에 입력합니다. 귀하의 백그라운드 서버는 공지 메시지를 수신한 후에 같은 계산법으로 sign이 정확한지, 나아가 메시지가 Tencent Cloud 백그라운드로부터 전달된 것인지 여부를 확인할 수 있습니다. </td>
</tr></table>

>? <span id="key"></span>key는 [기능 템플릿] > [[콜백 설정]](https://console.cloud.tencent.com/live/config/callback)의 콜백 키이며, 주로 인증하는 데 사용됩니다. 귀하의 데이터 정보를 안전하게 보호하기 위해 입력하실 것을 권장합니다.
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)




### 콜백 메시지 매개변수

| **매개변수**       | **필수 입력 여부** | **데이터 유형** | **설명**                                                     |
| :------------- | :----------- | :----------- | :----------------------------------------------------------- |
| tid            | 필수 입력         | Number       | 알람 정책 ID, 비디오 콘텐츠 알람: 20001                             |
| streamId       | 선택 사항         | String       | 스트리밍 이름                                                       |
| channelId      | 선택 사항         | string       | 채널 ID                                                      |
| img            | 필수 입력         | string       | 알람 이미지 링크                                                 |
| <span id="type"></span> type         | 필수 입력         | Array        | 이미지 유형,  0: 일반 이미지, 1~5: 부적절한 이미지 |
| confidence     | 필수 입력         | Number       | 음란물 연관 수치 신뢰도, 범위 0~100: normalScore, hotScore, pornScore로 이루어진 종합 평점 |
| normalScore    | 필수 입력         | Number       | 일반 이미지일 경우의 평점                                         |
| hotScore       | 필수 입력         | Number       | 성적인 이미지일 경우의 평점                                         |
| pornScore      | 필수 입력         | Number       | 음란성 이미지일 경우의 평점                                         |
| level          | 선택 사항         | Number       | 이미지의 등급                                                   |
| ocrMsg         | 선택 사항         | string       | 이미지의 OCR 식별 정보(존재할 경우)                              |
| screenshotTime | 필수 입력         | Number       | 화면 캡처 시간                                                     |
| sendTime       | 필수 입력         | Number       | 요청 발송 시간, UNIX 타임스탬프                                    |
| [gameDetails](#gamedetails)    | 선택 사항         | Object       | 게임 상세 정보                                                 |
| similarScore   | 선택 사항         | Number       | 이미지 유사도 평점                                               |
| stream_param   | 선택 사항         | String       | 푸시 스트림 매개변수                                                     |
| app            | 선택 사항         | String       | 푸시 스트림 도메인                                                     |
| appid          | 선택 사항         | Number       | 비즈니스 ID                                                      |
| appname        | 선택 사항         | String       | 푸시 스트림 path 경로                                               |


#### gameDetails

| **매개변수 이름**  | **필수 입력 여부** | **유형** | **설명**     |
| :------------ | :----------- | :------- | :----------- |
| battlegrounds | 선택 사항         | Object   | PUBG 정보 |
| [gameList](#gamelist)      | 선택 사항         | Array    | 게임 리스트     |

#### gameList

| **매개변수 이름** | **필수 입력 여부** | **유형** | **설명** |
| :----------- | :----------- | :------- | :------- |
| name         | 선택 사항         | String   | 게임 이름 |
| confidence   | 선택 사항         | Number   | 확률     |

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





