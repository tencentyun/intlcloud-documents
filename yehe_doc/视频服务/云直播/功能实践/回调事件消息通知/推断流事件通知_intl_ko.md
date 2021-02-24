스트리밍 푸시/중단 콜백은 라이브 방송 푸시 스트리밍 성공과 중단을 포함한 라이브 방송 푸시 스트리밍 상태 정보에 사용됩니다. 콜백 템플릿에서 푸시 스트리밍 콜백과 스트리밍 중단 콜백 메시지를 수신할 서버 주소를 설정하고, 해당 템플릿을 푸시 스트림 도메인과 연결해야 합니다. 해당하는 푸시 스트리밍 주소를 생성하고 라이브 스트리밍 푸시를 시작할 경우, Tencent Cloud LVB 백그라운드는 푸시 스트리밍 결과를 귀하가 설정한 수신용 서버로 콜백합니다.

본 문서에서는 스트리밍 푸시/중단 콜백 이벤트 트리거 발생 시 Tencent Cloud LVB가 사용자의 콜백 메시지 공지 필드로 발송하는 과정을 설명합니다.

## 주의사항
Tencent Cloud LVB의 콜백 기능 설정 방법을 이해하신 후 본 문서를 읽으실 것을 권장합니다. 콜백 메시지를 수신하는 방법은 [이벤트 공지를 수신하는 방법](https://intl.cloud.tencent.com/document/product/267/38080)을 참조 바랍니다. 


## 스트리밍 중단 이벤트 매개변수 설명
### 이벤트 유형 매개변수

| 이벤트 유형 | 필드값 설명 |
|---------|---------|
| 라이브 방송 푸시 스트리밍 | event_type = 1 |
| 라이브 방송 스트리밍 중단 | event_type = 0 |

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

| 필드 이름      | 유형   | 설명                                                         |
| :------------ | :----- | :----------------------------------------------------------- |
| appid         | int    | 사용자 [APPID](https://console.cloud.tencent.com/developer)                                                   |
| app           | string | 푸시 스트림 도메인                                                     |
| appname       | string | 푸시 스트림 경로                                                     |
| stream_id     | string | 라이브 방송 스트리밍 이름                                                   |
| channel_id    | string | 동일 라이브 방송 스트리밍 이름                                                 |
| event_time    | int64  | 이벤트 메시지가 생성하는 UNIX 타임스탬프                               |
| sequence      | string | 메시지 일련번호로, 푸시 스트리밍 이벤트를 식별합니다. 푸시 스트리밍 이벤트는 동일한 일련번호의 푸시 스트리밍 및 중단 메시지를 생성합니다.|
| node          | string | 라이브 방송 액세스 포인트 IP                                              |
| user_ip       | string | 사용자 푸시 스트림 IP                                                  |
| stream_param  | string | 사용자 푸시 스트림 URL이 가지는 매개변수                                        |
| push_duration | string | 스트리밍 중단 이벤트 공지 푸시 시간, 밀리초 단위                               |
| errcode       | int    | 스트리밍 중단 에러 코드                                                 |
| errmsg        | string | 스트리밍 중단 에러 설명                                               |

### 스트리밍 중단 에러 코드

| errcode | 에러 설명                   | 에러 원인                               |
| :----- | :------------------------- | :------------------------------------- |
| 1      | recv rtmp deleteStream     | 호스트 클라이언트의 자발적 스트리밍 중단(스트리밍 삭제 시간)                         |
| 2      | recv rtmp closeStream      | 호스트 클라이언트의 자발적 스트리밍 중단(스트리밍 비활성화 시간)                         |
| 3      | recv() return 0            | 호스트 클라이언트의 자발적 TCP 연결 중단                |
| 4      | recv() return error        | 호스트 클라이언트의 TCP 연결 오류                    |
| 7      | rtmp message large than 1M | 수신된 스트리밍 데이터 오류                         |
| 기타   | 라이브 방송 서비스 내부 오류           | 프로세스 진행에 도움이 필요한 경우 Tencent 비지니스 직원에게 문의 또는 티켓 제출|

### 콜백 메시지 예시

```
{
"app":"test.domain.com",

"appid":12345678,

"appname":"live",

"channel_id":"test_stream",

"errcode":0,

"errmsg":"ok",

"event_time":1545115790,

"event_type":1,

"node":"100.121.160.92",

"sequence":"6674468118806626493",

"stream_id":"test_stream",

"stream_param":"stream_param=test",

"user_ip":"119.29.94.245",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873
}
```
