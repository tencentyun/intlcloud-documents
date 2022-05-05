라이브 방송 화면 캡처는 고정된 시간 간격으로 실시간 라이브 방송 스트리밍 화면을 캡처하여 생성된 이미지를 COS에 저장합니다. 그리고 화면 캡처 콜백은 주로 이미지 생성 시간, 이미지 크기, 경로 및 다운로드 가능한 주소 등 캡처 화면의 이미지 저장 정보를 푸시하는 데 사용됩니다. 콜백 템플릿에서 화면 캡처 콜백 메시지를 수신할 서버 주소를 설정하고, 해당 템플릿을 푸시 도메인과 연결해야 합니다. 라이브 방송 스트리밍에서 화면 캡처 이벤트가 트리거 될 경우, Tencent Cloud LVB 백엔드에서 화면 캡처 정보를 사용자가 설정한 수신용 서버로 콜백합니다.

본 문서에서는 화면 캡처 콜백 이벤트 발생 시 Tencent Cloud CSS가 사용자에게 전송하는 콜백 메시지 알림 필드에 대해 설명합니다.

## 주의 사항

- Tencent Cloud CSS의 콜백 기능 설정 방법을 이해하신 후 본 문서를 읽으실 것을 권장합니다. 콜백 메시지를 수신하는 방법은 [이벤트 알림 수신 방법](https://intl.cloud.tencent.com/document/product/267/38080)을 참고 바랍니다.
- 화면 캡처 콜백 이벤트를 트리거한 후 얻은 화면 캡처 정보는 라이브 방송 음란물 감지, 라이브 방송 썸네일 등 다양한 시나리오에 사용할 수 있습니다.

## 화면 캡처 이벤트 매개변수 설명
### 이벤트 유형 매개변수

| 이벤트 유형 | 필드 값 설명           |
| :------- | :------------- |
| 라이브 방송 화면 캡처 | event_type = 200 |

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

>? key는 **이벤트 센터** > [**라이브 방송 콜백**](https://console.cloud.tencent.com/live/config/callback)의 콜백 키로 주로 인증에 사용됩니다. 데이터 정보를 안전하게 보호하기 위해 입력을 권장합니다.

![](https://main.qcloudimg.com/raw/48f919f649f84fd6d6d6dd1d8add4b46.png)

### 콜백 메시지 매개변수

| 필드 이름     | 유형   | 설명                        |
| :----------- | :----- | :-------------------------- |
| app     |    string     |    푸시 도메인    |
| appname     |    string   |      푸시 스트림 경로    |
| stream_param    |     string    |     사용자 푸시 스트림 URL의 매개변수   |
| stream_id    | string | 라이브 방송 스트림 이름                  |
| channel_id   | string | 동일 라이브 방송 스트림 이름                |
| create_time  | int64  | 화면 캡처 생성 UNIX 타임스탬프        |
| file_size    | int    | 화면 캡처 파일 크기, 바이트 단위    |
| width        | int    | 화면 캡처 너비, 화소 단위          |
| height       | int    | 화면 캡처 길이, 화소 단위          |
| pic_url      | string | 화면 캡처 파일 경로 `/path/name.jpg` |
| pic_full_url | string | 화면 캡처 다운로드 URL                |

### 콜백 메시지 예시
<dx-codeblock>
::: json json
{
    "app":"test.app",
		
    "appname":"live",
    	
    "channel_id":"your_channelid",
    	
    "create_time":1622599925,
    	
    "event_type":200,
    	
    "file_size":30670,
    	
    "height":720,
    
    "pic_full_url":"http://your.cos.region.myqcloud.com/channelid/channelid-screenshot-10-12-05-1280x720.jpg",
    	
    "pic_url":"/channelid/channelid-screenshot-10-12-05-1280x720.jpg",
    	
    "sign":"ca3e25e5dc17a6f9909a9ae7281e300d",
    	
    "stream_id":"your_streamid",
    	
    "stream_param":"txSecret=ca3e25e5dc17a6f9909a9ae7281e300d&txTime=60B83800",
    	
    "t":1622600525,
    	
    "width":1280
}
:::
</dx-codeblock>










