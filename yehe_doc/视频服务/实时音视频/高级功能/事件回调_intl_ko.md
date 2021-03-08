이벤트 콜백 서비스는 HTTP/HTTPS 요청 형식으로 TRTC 서비스의 이벤트 알림을 사용자의 서버로 공지합니다. 이벤트 콜백 서비스는 방 이벤트(Room Event) 그룹과 미디어 이벤트(Media Event) 그룹의 일부 이벤트를 통합하였으며, 사용자는 Tencent Cloud에 관련 구성 정보를 제공해 서비스를 활성화할 수 있습니다.

<span id="deploy"></span>
## 설정 정보
TRTC 콘솔은 콜백 정보 셀프 설정을 지원하며 설정이 완료되면 이벤트 콜백 알림을 수신할 수 있습니다.


>!사용자는 다음과 같은 정보를 사전에 준비해야 합니다.
>- **필수항목**: 콜백 알림을 수신하기 위한 HTTP/HTTPS 서버 주소입니다.
>- **선택항목**: 서명을 계산하는 키로 영문 알파벳 대소문자와 숫자로 구성해 최대 32자까지 사용자가 정의할 수 있습니다.

## 요청시간 초과 후 재시도
이벤트 콜백 서버가 메시지 발송 알림을 보낸 뒤 5초 이내에 사용자의 서버로부터 응답을 받지 못할 경우 알림 실패로 간주합니다. 첫 번째 알림 실패 후 즉시 재시도하며, 그 이후 실패하면 메시지가 1분 이상 지속될 때까지 **10초** 간격으로 계속 재시도합니다.

<span id="format)"></span>
## 이벤트 콜백 메시지 포맷

이벤트 콜백 메시지는 HTTP/HTTPS POST 요청 형식으로 사용자의 서버로 전송되며 다음을 참고하십시오.

- 문자 인코딩 포맷: UTF-8.
- 요청: body 양식은 JSON입니다.
- 응답:HTTP STATUS CODE = 200, 서버가 응답 패키지의 세부 콘텐츠를 무시합니다. 원활한 프로토콜 연결을 위해 클라이언트 응답 콘텐츠에 JSON: {"code":0} 추가를  권장합니다.


## 매개변수 설명
<span id="message)"></span>
### 콜백 메시지 매개변수

- 이벤트 콜백 메시지의 header는 다음과 같은 필드를 포함합니다: 
<table id="header">
<tr><th>필드 이름</th><th>값</th></tr></thead><tr>
<td>Content-Type</td><td>application/json</td>
</tr><tr>
<td>Sign</td><td>서명값</td>
</tr><tr>
<td>SdkAppId</td><td>sdk application id</td>
</tr></table>
- 이벤트 콜백 메시지의 body는 다음과 같은 필드를 포함합니다.
<table id="body">
<tr><th>필드 이름</th><th>유형</th><th>의미</th>
</tr><tr>
<td>EventGroupId</td><td>Number</td>
<td><a href="#eventId">이벤트 그룹 ID</a></td>
</tr><tr>
<td>EventType</td>
<td>Number</td>
<td><a href="#event_type">콜백 알림 이벤트 유형</a></td>
</tr><tr>
<td>CallbackTs</td>
<td>Number</td>
<td>이벤트 콜백 서버가 사용자의 서버로 보낸 콜백 요청의 Unix 타임스탬프, 단위는 ms</td>
</tr><tr>
<td>EventInfo</td>
<td>JSON Object</td>
<td><a href="#event_infor">이벤트 정보</a></td>
</tr>
</tbody></table>

<span id="eventId)"></span>
### 이벤트 그룹 ID

| 필드 이름            | 값   | 의미       |
| ----------------- | ---- | ---------- |
| EVENT_GROUP_ROOM  | 1    | 방 이벤트 그룹 |
| EVENT_GROUP_MEDIA | 2    | 미디어 이벤트 그룹 |

<span id="event_type)"></span>
### 이벤트 유형

| 필드 이름                  | 값   | 의미             |
| ----------------------- | ---- | ---------------- |
| EVENT_TYPE_CREATE_ROOM  | 101  | 방 생성         |
| EVENT_TYPE_DISMISS_ROOM | 102  | 방 해체         |
| EVENT_TYPE_ENTER_ROOM   | 103  | 방 입장          |
| EVENT_TYPE_EXIT_ROOM    | 104  | 방 퇴장         |
| EVENT_TYPE_START_VIDEO  | 201  | 영상 데이터 푸시 시작 |
| EVENT_TYPE_STOP_VIDEO   | 202  | 영상 데이터 푸시 중지 |
| EVENT_TYPE_START_AUDIO  | 203  | 음성 데이터 푸시 시작 |
| EVENT_TYPE_STOP_AUDIO   | 204  | 음성 데이터 푸시 중지 |
| EVENT_TYPE_START_ASSIT  | 205  | 메타데이터 푸시 시작 |
| EVENT_TYPE_STOP_ASSIT   | 206  | 메타데이터 푸시 중지 |

<span id="event_infor)"></span>
### 이벤트 정보

| 필드 이름  | 유형   | 의미  |
| ------- | ------ | --------------------------------- |
|RoomId      |     String/Number       |     방 이름(유형이 클라이언트 방 번호 유형과 일치)    |
| EventTs | Number | 이벤트 발생 시간의 Unix 타임스탬프, 단위는 s    |
| UserId  | String | 사용자 ID                            |
| Role    | Number | [역할 유형](#role_type)(option: 입장 및 퇴장 시 휴대) |
| Reason  | Number | [구체적 원인](#reason) (option: 입장 및 퇴장 시 휴대) |

<span id="role_type)"></span>
### 역할 유형

| 필드 이름             | 값   | 의미 |
| ------------------ | ---- | ---- |
| MEMBER_TRTC_ANCHOR | 20   | 호스트 |
| MEMBER_TRTC_VIEWER | 21   | 시청자 |

<span id="reason)"></span>
#### 구체적 원인

| 필드 이름    | 의미                              |
| -------  | --------------------------------- |
|방 입장   |<li/>1：정상 입장<li/>2：네트워크 전환<li/>3：요청시간 초과 후 재시도<li/>4： 크로스 룸 마이크 연결 방 입장|
|방 퇴장 | <li/>1：정상 퇴장<li/>2：요청시간 초과 후 나가기<li/>3：사용자가 다른 단말에서 접속, 로컬 로그아웃<li/>4：방 사용자가 삭제됨<li/>5：마이크 연결을 취소하고 퇴장<li/>6：강제 종료|



### 서명 계산
서명은 HMAC SHA256 암호화 알고리즘에 의해 계산됩니다. 사용자의 이벤트 콜백 수신 서버가 콜백 메시지를 수신하면 같은 방식으로 서명을 계산하며, 서명이 동일하면 Tencent Cloud TRTC의 이벤트 콜백이 위조되지 않았음을 의미합니다. 서명 계산 방식은 다음과 같습니다:
```
//서명(Sign) 계산 공식에서 key는 서명 계산용 암호화 키를 의미합니다.
Sign = base64（hmacsha256(key, body)）
```



