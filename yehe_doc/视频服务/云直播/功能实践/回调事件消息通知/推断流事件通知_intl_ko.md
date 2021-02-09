라이브 방송 기능을 활성화한 후 푸시 스트리밍 콜백 템플릿에 등록된 콜백 도메인을 설정할 수 있으며, LVB 백그라운드에서 푸시 스트리밍 결과를 콜백하여 보내줍니다.
본 문서를 읽기 전 Tencent Cloud LVB의 콜백 정보 수신 방법을 확인하십시오. 자세한 내용은 [이벤트 공지 수신 방법](https://intl.cloud.tencent.com/document/product/267/38080)을 참고하십시오. 


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
<td>만료 시간 및 이벤트 공지 서명 만료 UNIX 타임스탬프<ul style="margin:0"><li>기본적으로 Tencent Cloud의 메시지 공지 만료 시간은 10분입니다. 메시지 공지에서 t 값으로 지정된 시간이 경과한 경우 무효한 공지라고 판단하며 이로써 네트워크 리플레이 공격을 방지할 수 있습니다.<li>t의 포맷은 10진법 UNIX 타임스탬프로 즉, 1970년 01월 01일(UTC/GMT의 자정)부터 경과한 초의 값입니다.</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>이벤트 공지 보안 서명 sign = MD5(key + t)<br>설명: Tencent Cloud는 암호화 <a href="#key">key</a>와 t의 문자열을 조합하여 MD5 계산으로 sign 값을 얻고 이를 공지 정보에 포함합니다. 백그라운드 서버가 공지 정보를 수신하면 똑같은 알고리즘으로 sign의 정확도 여부를 확인하고 그 정보가 실제로 Tencent Cloud 백그라운드에서 온 것인지 확인할 수 있습니다.</td>
</tr></table>

>? <span id="key"></span>key는 [사건 통지]>[라이브 방송 콜백](https://console.cloud.tencent.com/live/config/callback)의 콜백 키이며 주로 인증하는 데 쓰입니다. 데이터 정보 보안을 위해 작성을 권장합니다.
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### 콜백 메시지 매개변수

| 필드 이름      | 유형   | 설명                                                         |
| :------------ | :----- | :----------------------------------------------------------- |
| appid         | int    | 사용자 [APPID](https://console.cloud.tencent.com/developer)                                                   |
| app           | string | 푸시 스트리밍 도메인                                                     |
| appname       | string | 푸시 스트리밍 경로                                                     |
| stream_id     | string | 라이브 방송 스트리밍 이름                                                   |
| channel_id    | string | 동일 라이브 방송 스트리밍 이름                                                 |
| event_time    | int64  | 이벤트 메시지가 생성하는 UNIX 타임스탬프                                   |
| sequence      | string | 메시지 일련번호로, 푸시 스트리밍 이벤트를 식별합니다. 푸시 스트리밍 이벤트는 동일한 일련번호의 푸시 스트리밍 및 중단 메시지를 생성합니다. |
| node          | string | 라이브 방송 액세스 포인트 IP                                              |
| user_ip       | string | 사용자 푸시 스트리밍 IP                                                  |
| stream_param  | string | 사용자 푸시 스트리밍 URL이 가지는 매개변수                                        |
| push_duration | string | 스트리밍 중단 이벤트 공지 푸시 시간, 밀리초 단위                               |
| errcode       | int    | 스트리밍 중단 에러 코드                                                 |
| errmsg        | string | 스트리밍 중단 에러 설명                                               |

### 스트리밍 중단 에러 코드

| errcode | 에러 설명                   | 에러 원인                               |
| :----- | :------------------------- | :------------------------------------- |
| 1      | recv rtmp deleteStream     | 호스트 클라이언트의 자발적 스트리밍 중단                         |
| 2      | recv rtmp closeStream      | 호스트 클라이언트의 자발적 스트리밍 중단                         |
| 3      | recv() return 0            | 호스트 클라이언트의 자발적 TCP 연결 중단                |
| 4      | recv() return error        | 호스트 클라이언트의 TCP 연결 오류                    |
| 7      | rtmp message large than 1M | 수신된 스트리밍 데이터 오류                         |
| 기타   | 라이브 방송 서비스 내부 오류           | 프로세스 진행에 도움이 필요한 경우 Tencent 직원에게 문의 또는 티켓 제출|

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
