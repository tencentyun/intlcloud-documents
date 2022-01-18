라이브 방송 녹화는 푸시 도메인에 바인딩된 녹화 템플릿에 따라 실시간으로 라이브 방송 스트리밍 화면을 녹화하고, 해당 녹화 파일을 VOD에 저장합니다. 녹화 콜백은 녹화 시작 시간, 종료 시간, 생성된 녹화 파일 ID, 녹화 파일 크기 및 파일 다운로드 주소 등을 포함한 녹화 파일 정보를 푸시하는 데 사용됩니다. 콜백 템플릿에서 녹화 콜백 메시지를 수신할 서버 주소를 설정하고, 해당 템플릿을 푸시 도메인과 연결해야 합니다. 라이브 방송 스트리밍이 녹화 이벤트를 트리거한 후, Tencent Cloud CSS 백그라운드는 녹화 파일 정보를 귀하가 설정한 수신용 서버로 콜백합니다.

본 문서는 녹화 콜백 이벤트 트리거 후, Tencent Cloud CSS가 사용자에게 발송하는 콜백 메시지 알림 필드를 설명합니다.

## 주의 사항

- Tencent Cloud CSS의 콜백 기능 설정 방법을 이해하신 후 본 문서를 읽으실 것을 권장합니다. 콜백 메시지를 수신하는 방법은 [이벤트 알림 수신 방법](https://intl.cloud.tencent.com/document/product/267/38080)을 참고 바랍니다.
- 녹화된 비디오 파일은 기본적으로 [VOD](https://console.cloud.tencent.com/vod/overview) 콘솔에 저장됩니다. 요금 연체로 인해 VOD 서비스가 정지되는 일이 없도록 사전에 VOD 서비스를 개통해두실 것을 권장합니다.
- API로 [녹화 작업 생성](https://intl.cloud.tencent.com/document/product/267/37309)을 진행하는 경우, 녹화 콜백은 사용자 푸시 스트림 URL의 [stream_param](#message) 매개변수를 반환하지 않으며 다른 녹화 방식은 반환됩니다.
- HLS 연속 녹화 기능을 설정하면 중간에 스트림이 끊겨도 콜백하지 않으며, 기본적으로 연속 녹화 후 최종 생성된 파일만 콜백합니다.


## 녹화 이벤트 매개변수 설명
### 이벤트 유형 매개변수

| 이벤트 유형 | 필드 값 설명           |
| :------- | :------------- |
| 라이브 방송 녹화 | event_type = 100 |

[](id:public)
### 콜백 공용 매개변수
<table>
<tr><th>필드 이름</th><th>유형</th><th>설명</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>만료 시간, 이벤트 알림 서명 만료 UNIX 타임스탬프입니다.<ul style="margin:0"><li>Tencent Cloud 메시지 알림의 기본 만료 시간은 10분입니다. 메시지 알림의 t 값으로 지정된 시간이 만료되었을 경우, 해당 알림을 무효라고 판정할 수 있으며, 네트워크 리플레이 공격을 방지할 수 있습니다.<li>t의 형식은 10진법 UNIX 타임스탬프입니다. 즉, 1970년 01월 01일(UTC/GMT의 자정)부터 경과한 초 단위 수입니다.</ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>이벤트 알림 보안 서명은 sign = MD5(key + t)입니다.<br>설명: Tencent Cloud는 암호화된 <a href="#key">key</a>와 t의 문자열 연결 후, MD5 계산을 통해 sign 값을 얻은 후, 이를 알림 메시지에 입력합니다. 사용자의 백엔드 서버는 알림 메시지 수신 후 같은 계산법으로 sign이 정확한지 확인하고, 메시지 출처가 Tencent Cloud 백엔드인지 확인할 수 있습니다.</td>
</tr></table>

>? [](Id:key)key는 **이벤트 센터>[라이브 방송 콜백](https://console.cloud.tencent.com/live/config/callback)**의 콜백 키로 주로 인증에 사용됩니다. 데이터 정보를 안전하게 보호하기 위해 입력을 권장합니다.
![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

[](id:message)

### 콜백 메시지 매개변수

| 필드 이름     | 유형   | 설명   |
| ----------- | ----------- | ----------- |
| appid        | int    | 사용자 [APPID](https://console.cloud.tencent.com/developer) |
| app          | string | 푸시 도메인 |
| appname      | string | 푸시 스트림 경로 |
| stream_id    | string | 라이브 방송 스트림 이름 |
| channel_id   | string | 라이브 방송 스트림 이름과 동일 |
| file_id      | string | VOD file ID, [VOD 플랫폼](https://intl.cloud.tencent.com/document/product/266/33895)에서 VOD 비디오 파일의 고유 위치 지정|
| file_format  | string | FLV, HLS, MP4, AAC |
| task_id      | string | 녹화 작업 ID. API로 생성한 녹화 작업만 의미가 있습니다. [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)가 반환한 작업 ID |
| start_time   | int64  | 녹화 작업 파일 쓰기 시작 시간. 이 값은 녹화 콘텐츠의 시작 시간이 될 수 없습니다. 녹화 콘텐츠 시작 시간 = end_time – duration |
| end_time     | int64  | 녹화 작업 종료 타임스탬프 |
| duration     | int64  | 녹화 파일 길이, 단위: 초 |
| file_size    | uint64 | 녹화 파일 크기, 단위: 바이트 |
| stream_param | string | 사용자 푸시 스트림 URL의 매개변수(사용자 정의) |
| video_url    | string | 녹화 파일 다운로드 URL |



[](id:example)
### 콜백 메시지 예시
<dx-codeblock>
::: JSON JSON
{
"event_type":100,

"appid":12345678,

"app":yourapp,

"appname":yourappname,

"stream_id":"stream_test",

"channel_id":"stream_test",

"file_id":"1234567890",

"file_format":"hls",

"task_id":"UpTbk5RSVhRQ********************0xTSlNTQltlRVRLU1JAWW9EUb",

"start_time":1545047010,

"end_time":1545049971,

"duration":2962,

"file_size":277941079,

"stream_param":"stream_param=test",

"video_url":"http://12345678.vod2.myqcloud.com/xxxx/yyyy/zzzz.m3u8",

"sign":"ca3e25e**********09a9ae7281e300d",

"t":1545030873
}
:::
</dx-codeblock>



 

