## 서버 녹음 콜백 설명[](id:date)

### 설명
네트워크의 영향을 받아 서버가 알림을 받는 순서와 이벤트가 발생하는 순서가 정확히 일치하지 않을 수 있습니다.  
서비스에는 재시도 메커니즘이 있지만 모든 메시지가 도달한다는 보장이 없습니다.  
상기 두 가지 사항을 고려할 때 비즈니스의 핵심 비즈니스 로직이 메시지 알림 서비스에 의존하는 것은 권장되지 않습니다.

### 네트워크 프로토콜

콘솔에서 콜백 주소, 즉 HTTP(S) 프로토콜 API의 URL을 설정한 경우 POST 요청을 지원해야 하며 전송 데이터 인코딩은 UTF-8을 채택합니다.

### HTTP 헤더 매개변수

<table>
<tr><th>이름</th><th>유형</th><th>필수 여부</th><th>설명</th></tr>
<tr>
<td>Signature</td>
<td>string</td>
<td>Yes</td>
<td>서명, 자세한 내용은 아래의 <a href="#Signature">서명 생성</a>을 참고하십시오</td>
</tr></table>

### 서명 생성[](id:Signature)

Signature = HMAC-SH1 ( strContent, SecretKey )

- **strContent**: body의 전체 JSON 콘텐츠(길이는 Content-Length 기준)인 서명 문자열입니다.
- **body**: 비즈니스로 콜백되는 JSON 콘텐츠로, 아래 [콜백 예시](#example)의 전체 콘텐츠가 body입니다.
- **SecretKey**: 키. 애플리케이션의 권한 키로, [콘솔 > 애플리케이션 상세 정보](https://console.tencentcloud.com/gamegme)를 통해 확인할 수 있습니다.
- **HMAC-SH1**: 서명 알고리즘입니다.


### 콜백 매개변수

<table>
<thead><tr>
<th width="20%">이름</th>
<th width="20%">유형</th>
 <th width="60%">설명</th>  
</tr></thead>
<tbody><tr>
<td>BizID</td>
<td>Integer</td> 
<td>애플리케이션의 AppID로, <a href="https://console.tencentcloud.com/gamegme">콘솔 > 애플리케이션 세부 정보</a>를 통해 확인할 수 있습니다.</td> 
</tr>
<tr>
<td>RoomID</td>
<td>String</td> 
<td>방 ID</td> 
</tr>
<tr>
<td>UserID</td>
<td>String</td> 
<td>사용자 ID</td> 
</tr>
<tr>
<td>RecordMode</td>
<td>Integer</td> 
<td >녹음 모드<ul style="margin:0">
	<li/>0: 단일 스트림
	<li/>1: 혼합 스트림
</ul ></td>
</tr>
<tr>
<td>Timestamp</td>
<td>Integer</td> 
<td>콜백 전송 시의 타임스탬프(s)</td> 
</tr>
<tr>
<td>TaskID</td>
<td>Integer</td> 
<td>클라우드 녹음 서비스에서 할당한 작업 ID입니다. 작업 ID는 녹음의 라이프사이클 프로세스에 대한 고유 식별자이며 녹음이 종료되면 의미를 잃습니다. 사용자 지정 녹음 모드를 사용하면,
작업 ID는 녹음이 시작될 때 응답 매개변수를 통해 얻을 수 있으며, 비즈니스에서 저장해 두어야 합니다. 이는 이번 녹음 작업에 대한 다음 번 작업의 요청 매개변수 입니다.</td> 
</tr>
<tr>
<td>EventType</td>
<td>Integer</td> 
<td>이벤트 유형</td> 
</tr>
</tr>
<tr>
<td>Detail</td>
<td><a href="#EventDetail">EventDetail</a></td> 
<td>이벤트 세부 정보, 형식은 EventType에 의해 결정됩니다</td> 
</tr>
</table>



### EventDetail 이벤트 세부 정보 설명[](id:EventDetail)

| EventType | 설명             | Detail                                                         |
| --------- | --------------- | ------------------------------------------------------------ |
| 1         | 오디오 파일 녹음 시작   | <ul><li>SeqNo: Number, 세그먼트 시리얼 넘버</li><li> FileName: String, 파일 이름</li></ul> |
| 2         | 오디오 파일 녹음 완료   | <ul><li>SeqNo: Number, 세그먼트 시리얼 넘버</li><li> FileName: String, 파일 이름</li></ul> |
| 3         | 오디오 파일 업로드 완료   | <ul><li>SeqNo: Number, 세그먼트 시리얼 넘버</li><li> FileName: String, 파일 이름</li></ul> |


### 콜백 예시[](id:example)

```json
{
    "BizID":1400000000,
    "RoomID":"100",
    "UserID":"999",
    "TaskID":446946705284000000,
    "RecordMode":1,
    "Timestamp":1675930605,
    "EventType":1,
    "Detail":{
    	"SeqNo":0,
    	"FileName":"1400000000_100_999/2023-02-09-16-16-45_446946705284000000_audio.mp3"
    }
}
```