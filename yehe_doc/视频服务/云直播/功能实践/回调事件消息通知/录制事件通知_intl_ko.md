라이브 방송 녹화 기능을 활성화한 후 라이브 방송 녹화 콜백 템플릿에서 로그인한 콜백 도메인을 설정하면 LVB 백그라운드에서 녹화 결과를 콜백하여 보내줍니다.

# 주의 사항

- 본 문서를 읽기 전 Tencent Cloud LVB의 콜백 기능 설정 방법, 콜백 정보 수신 방법을 확인하십시오. 자세한 내용은 [이벤트 공지 수신 방법](https://intl.cloud.tencent.com/zh/document/product/267/38080)을 참고하십시오.
- 기본적으로 녹화 비디오 파일은 [VOD](https://console.cloud.tencent.com/vod/overview) 콘솔에 저장됩니다. VOD 비즈니스 연체로 인한 사용 중단을 피하기 위해 사전에 VOD 서비스를 활성화하고 VOD 관련 리소스 패키지를 구매하십시오.


## 녹화 이벤트 매개변수 설명

### 이벤트 유형 매개변수

| 이벤트 유형 | 필드값 설명           |
| :------- | :------------- |
| 라이브 방송 녹화 | event_type = 100 |

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

>? <span id="key"></span>key는 [기능 템플릿]>[콜백 설정](https://console.cloud.tencent.com/live/config/callback)의 콜백 키이며 주로 인증하는 데 쓰입니다. 데이터 정보 보안을 위해 작성을 권장합니다.
>![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)


### 콜백 메시지 매개변수

| 필드 이름     | 유형   | 설명                                                 |
| :----------- | :----- | :--------------------------------------------------- |
| appid        | int    | 사용자 [APPID](https://console.cloud.tencent.com/developer)                                           |
| stream_id    | string | 라이브 방송 스트리밍 이름                                           |
| channel_id   | string | 동일 라이브 방송 스트리밍 이름                                         |
| file_id      | string | VOD file ID, [VOD 플랫폼](https://intl.cloud.tencent.com/zh/document/product/266/33895)에서 VOD 비디오 파일 위치 지정 가능|| file_format  | string | flv, hls, mp4, aac                                   |
| start_time   | int64  | 녹화 파일 시작 타임스탬프                                   |
| end_time     | int64  | 녹화 파일 종료 타임스탬프                                   |
| duration     | int64  | 녹화 파일 시간, 초 단위                                 |
| file_size    | uint64 | 녹화 파일 크기, 바이트 단위                               |
| stream_param | string | 사용자 푸시 스트리밍 URL이 가지는 매개변수                                |
| video_url    | string | 녹화 파일 다운로드 URL                                 |

### 콜백 메시지 예시

```
{
"event_type":100,

"appid":12345678,

"stream_id":"stream_test",

"channel_id":"stream_test",

"file_id":"1234567890",

"file_format":"hls",

"start_time":1545047010,

"end_time":1545049971,

"duration":2962,

"file_size":277941079,

"stream_param":"stream_param=test",

"video_url":"http://12345678.vod2.myqcloud.com/xxxx/yyyy/zzzz.m3u8",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873
}
```





