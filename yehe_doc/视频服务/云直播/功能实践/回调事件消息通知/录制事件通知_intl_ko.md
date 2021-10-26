라이브 방송 녹화는 푸시 도메인에 바인딩된 녹화 템플릿에 따라 실시간으로 라이브 방송 스트리밍 화면을 녹화하고, 해당 녹화 파일을 VOD에 생성합니다. 녹화 콜백은 녹화 파일 정보를 푸시하는 데 사용됩니다. 녹화 시작 시간, 종료 시간, 생성된 녹화 파일 ID, 녹화 파일 크기 및 파일 다운로드 주소 등이 포함됩니다. 콜백 템플릿에서 녹화 콜백 메시지를 수신할 서버 주소를 설정하고, 해당 템플릿을 푸시 스트림 도메인과 연결해야 합니다. 라이브 방송 스트리밍에서 녹화 이벤트가 트리거될 경우, Tencent Cloud CSS 백그라운드는 녹화 파일 정보를 귀하가 설정한 수신용 서버로 콜백합니다.

본 문서에서는 녹화 콜백 이벤트 트리거 시 Tencent Cloud CSS가 사용자의 콜백 메시지 공지 필드로 발송하는 과정을 설명합니다.

## 주의 사항

- Tencent Cloud CSS의 콜백 기능 설정 방법을 이해하신 후 본 문서를 읽으실 것을 권장합니다. 콜백 메시지를 수신하는 방법은 [이벤트 공지를 수신하는 방법](https://intl.cloud.tencent.com/document/product/267/38080)을 참조하십시오.
- 녹화된 비디오 파일은 기본적으로 [VOD](https://console.cloud.tencent.com/vod/overview) 콘솔에 저장됩니다. 연체로 인해 VOD 서비스가 정지되는 일이 없도록 사전에 VOD 서비스를 개통해두실 것을 권장합니다.
- API로 [녹화 작업 생성](https://intl.cloud.tencent.com/document/product/267/37309)을 진행할 경우, 녹화 콜백은 사용자 푸시 스트림 URL의 [stream_param](#message) 매개변수로 반환하지 않으며 다른 녹화 방식은 반환됩니다.
- HLS 연속 녹화 기능을 설정하면 중간에 스트림이 끊겨도 콜백하지 않으며, 기본적으로 연속되고 최종 파일이 생성될 때만 콜백합니다.


## 녹화 이벤트 매개변수 설명
### 이벤트 유형 매개변수

| 이벤트 유형 | 필드 값 설명           |
| :------- | :------------- |
| 라이브 방송 녹화 | event_type = 100 |

<span id="public"></span> 
### 콜백 공용 매개변수
<table>
<tr><th>필드 이름</th><th>유형</th><th>설명</th></tr>
<tr>
<td>t</td>
<td>int64</td>
<td>만료 시간, 이벤트 공지 서명 만료 UNIX 타임스탬프입니다. <ul style="margin:0"><li>Tencent Cloud 메시지 공지의 기본 만료 시간은 10분입니다. 메시지 공지의 t 값으로 지정된 시간이 만료되었을 경우, 해당 공지를 무효라고 판정할 수 있으며 나아가 네트워크 리플레이 공격을 방지할 수 있습니다. <li>t의 포맷은 10진법 UNIX 타임스탬프입니다. 즉, 1970년 01월 01일(UTC/GMT의 자정)부터 경과한 초의 수입니다. </ul></td>
</tr><tr>
<td>sign</td>
<td>string</td>
<td>이벤트 공지 보안 서명은 sign = MD5(key + t)입니다.<br>설명: Tencent Cloud는 암호화된 <a href="#key">key</a>와 t를 통해 문자열을 스티칭한 후, MD5를 통해 sign 값을 계산하여 이를 공지 메시지에 입력합니다. 사용자의 백그라운드 서버는 공지 메시지를 수신한 후에 같은 알고리즘으로 sign이 정확한지, 나아가 메시지가 Tencent Cloud 백그라운드로부터 전달된 것인지 여부를 확인할 수 있습니다.</td>
</tr></table>

>? <span id="key"></span>key는 [이벤트 센터]>[라이브 방송 콜백](https://console.cloud.tencent.com/live/config/callback)의 콜백 보안키로 주로 인증에 사용됩니다. 데이터 정보를 안전하게 보호하기 위해 입력하는 것을 권장합니다.
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)


<span id="message"></span> 
### 콜백 메시지 매개변수

| 필드 이름     | 유형   | 설명                                                 |
| :----------- | :----- | :--------------------------------------------------- |
| appid        | int    | 사용자 [APPID](https://console.cloud.tencent.com/developer)                                           |
| stream_id    | string | 라이브 방송 스트림 이름                                           |
| channel_id   | string | 동일한 라이브 방송 스트림 이름                                         |
| file_id      | string | VOD file ID, [VOD 플랫폼](https://intl.cloud.tencent.com/document/product/266/33895)에서 VOD 파일의 고유 위치를 지정할 수 있습니다.|
| file_format  | string | flv, hls, mp4, aac                                   |
| task_id	| string| 녹화 작업 ID. API로 녹화 작업을 생성한 경우에만 의미가 있으며, [CreateRecordTask](https://intl.cloud.tencent.com/document/product/267/37309)에서 반환하는 작업 ID입니다. |
| start_time   | int64  | 녹화 파일 시작 타임스탬프                                   |
| end_time     | int64  | 녹화 파일 종료 타임스탬프                                   |
| duration     | int64  | 녹화 파일 길이. 단위: 초                                 |
| file_size    | uint64 | 녹화 파일 크기. 단위: 바이트                               |
| stream_param | string | 사용자 푸시 스트림 URL의 매개변수(사용자 정의)                                |
| video_url    | string | 녹화 파일 다운로드 URL                                 |


<span id="example"></span> 
### 콜백 메시지 예시


```
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
```



