라이브 방송 화면 캡처는 일정 시간 간격으로 실시간 라이브 방송 스트리밍의 영상을 캡처하고 이미지를 생성합니다. 콜백 공지를 통해 화면 캡처 정보를 얻을 수 있습니다. 화면 캡처 데이터는 라이브 방송 음란물 감지, 라이브 방송 썸네일 등 다양한 시나리오에 사용할 수 있습니다.

## 주의 사항

- 본 문서를 읽기 전 Tencent Cloud LVB의 콜백 기능 설정 방법, 콜백 정보 수신 방법을 확인하십시오. 자세한 내용은 [이벤트 공지 수신 방법](https://intl.cloud.tencent.com/document/product/267/38080)을 참고하십시오.
- 화면 캡처 콜백 이벤트를 트리거한 후 얻은 화면 캡처 정보는 라이브 방송 음란물 감지, 라이브 방송 썸네일 등 다양한 시나리오에 사용할 수 있습니다.

## 화면 캡처 이벤트 매개변수 설명

### 이벤트 유형 매개변수

| 이벤트 유형 | 필드값 설명           |
| :------- | :------------- |
| 라이브 방송 화면 캡처 | event_type = 200 |

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


| 필드 이름     | 유형   | 설명                        |
| :----------- | :----- | :-------------------------- |
| stream_id    | string | 라이브 방송 스트리밍 이름                  |
| channel_id   | string | 동일 라이브 방송 스트리밍 이름                |
| create_time  | int64  | 화면 캡처 생성 UNIX 타임스탬프        |
| file_size    | int    | 화면 캡처 파일 크기, 바이트 단위    |
| width        | int    | 화면 캡처 너비, 화소 단위          |
| height       | int    | 화면 캡처 길이, 화소 단위          |
| pic_url      | string | 화면 캡처 파일 경로 `/path/name.jpg`  |
| pic_full_url | string | 화면 캡처 다운로드 URL                |

### 콜백 메시지 예시

```
{
"event_type":200,

"stream_id":"stream_name",

"channel_id":"stream_name",

"create_time":1545030273,

"file_size":7520,

"width":640,

"height":352,

"pic_url":"/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"pic_full_url":"http://testbucket-1234567890.cos.region.myqcloud.com/2018-12-17/stream_name-screenshot-19-06-59-640x352.jpg",

"sign":"ca3e25e5dc17a6f9909a9ae7281e300d",

"t":1545030873
}
```








