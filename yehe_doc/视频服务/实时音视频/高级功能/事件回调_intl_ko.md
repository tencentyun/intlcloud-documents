이벤트 콜백 서비스는 TRTC 서비스의 이벤트를 HTTP/HTTPS 요청 형식으로 사용자의 서버에 공지합니다. 방 이벤트 그룹(Room Event)과 미디어 이벤트 그룹(Media Event)의 일부 이벤트를 통합하였으며, 사용자는 Tencent Cloud에 관련 설정 정보를 제공해 서비스를 활성화할 수 있습니다.

[](id:deploy)
## 정보 설정
TRTC 콘솔은 콜백 정보 자체 설정을 지원하며, 설정이 완료되면 이벤트 콜백 공지를 수신할 수 있습니다. 자세한 작업 가이드는 [콜백 설정](https://cloud.tencent.com/document/product/647/52428)을 참고하십시오.


>!사용자는 다음과 같은 정보를 사전에 준비해야 합니다.
>- **필수 항목**: 콜백 공지를 수신하기 위한 HTTP/HTTPS 서버 주소입니다.
>- **옵션 항목**: 서명을 계산하는 키로, 영문 알파벳 대소문자와 숫자로 구성해 최대 32자까지 사용자 정의할 수 있습니다.

## 요청 시간 초과 후 재시도
이벤트 콜백 서버가 메시지 공지를 발송한 후 5초 이내에 사용자의 서버로부터 응답을 받지 못할 경우 공지 실패로 간주합니다. 첫 번째 공지 실패 후 즉시 재시도하며, 그 이후 실패하면 메시지가 1분 이상 지속될 때까지 **10초** 간격으로 계속 재시도합니다.

[](id:format)
## 이벤트 콜백 메시지 포맷

이벤트 콜백 메시지는 HTTP/HTTPS POST 요청 형식으로 사용자의 서버에 전송됩니다.

- **문자 인코딩 포맷**: UTF-8
- **요청**: body 포맷은 JSON
- **응답**: HTTP STATUS CODE = 200, 서버가 응답 패키지의 세부 내용을 무시합니다. 원활한 프로토콜 연결을 위해 클라이언트 응답 콘텐츠에 JSON: {'code':0} 추가를 권장합니다.
- **패킷 예시**: 다음은 '방 이벤트 그룹 - 방 입장' 이벤트의 패킷 예시입니다.
<dx-codeblock>
::: JSON JSON
{
    'EventGroupId': 1,                #방 이벤트 그룹
    'EventType': 103,                 #방 입장 이벤트
    'CallbackTs': 1615554923704,      #콜백 시간, 단위: 밀리초
    'EventInfo': {
        'RoomId': 12345,                #방 번호 숫자
        'EventTs': 1615554922,          #이벤트 발생 시간, 단위: 초
        'EventTs': 1615554922661,       #이벤트 발생 시간, 단위: 초
        'UserId': 'test',               #사용자ID
        'UniqueId': 1615554922656,      #고유 식별자
        'Role': 20,                     #사용자 역할, 호스트
        'TerminalType': 3,        #단말 유형, IOS
        'UserType': 3,        #사용자 유형, Native SDK
        'Reason': 1        #입장 원인: 정상 입장
	}
}
:::
</dx-codeblock>



## 매개변수 설명
[](id:message)
### 콜백 메시지 매개변수

- 이벤트 콜백 메시지의 header는 다음과 같은 필드를 포함합니다.
<table id='header'>
<tr><th>필드 이름</th><th>값</th></tr></thead><tr>
<td>Content-Type</td><td>application/json</td>
</tr><tr>
<td>Sign</td><td>서명값</td>
</tr><tr>
<td>SdkAppId</td><td>sdk application id</td>
</tr></table>
- 이벤트 콜백 메시지의 body는 다음과 같은 필드를 포함합니다.
<table id='body'>
<tr><th>필드 이름</th><th>유형</th><th>의미</th>
</tr><tr>
<td>EventGroupId</td><td>Number</td>
<td><a href='#eventId'>이벤트 그룹 ID</a></td>
</tr><tr>
<td>EventType</td>
<td>Number</td>
<td><a href='#event_type'>콜백 공지 이벤트 유형</a></td>
</tr><tr>
<td>CallbackTs</td>
<td>Number</td>
<td>이벤트 콜백 서버가 사용자의 서버로 보낸 콜백 요청의 Unix 타임스탬프, 단위: 밀리초</td>
</tr><tr>
<td>EventInfo</td>
<td>JSON Object</td>
<td><a href='#event_infor'>이벤트 정보</a></td>
</tr>
</tbody></table>

[](id:eventId)
### 이벤트 그룹 ID

| 필드 이름            | 값   | 의미       |
| ----------------- | ---- | ---------- |
| EVENT_GROUP_ROOM  | 1    | 방 이벤트 그룹 |
| EVENT_GROUP_MEDIA | 2    | 미디어 이벤트 그룹 |

[](id:event_type)
### 이벤트 유형

| 필드 이름                  | 값   | 의미             |
| ----------------------- | ---- | ---------------- |
| EVENT_TYPE_CREATE_ROOM  | 101  | 방 생성         |
| EVENT_TYPE_DISMISS_ROOM | 102  | 방 삭제         |
| EVENT_TYPE_ENTER_ROOM   | 103  | 방 입장          |
| EVENT_TYPE_EXIT_ROOM    | 104  | 방 퇴장         |
|  EVENT_TYPE_CHANGE_ROLE   | 105  |    역할 전환      |
| EVENT_TYPE_START_VIDEO  | 201  | 비디오 데이터 푸시 시작 |
| EVENT_TYPE_STOP_VIDEO   | 202  | 비디오 데이터 푸시 중지 |
| EVENT_TYPE_START_AUDIO  | 203  | 오디오 데이터 푸시 시작 |
| EVENT_TYPE_STOP_AUDIO   | 204  | 오디오 데이터 푸시 중지 |
| EVENT_TYPE_START_ASSIT  | 205  | 서브 채널 데이터 푸시 시작 |
| EVENT_TYPE_STOP_ASSIT   | 206  | 서브 채널 데이터 푸시 중지 |

[](id:event_infor)
### 이벤트 정보



| 필드 이름  | 유형   | 의미                              |
| ------- | ------ | --------------------------------- |
|RoomId      |     String/Number       |     방 이름(유형이 클라이언트 방 번호 유형과 일치)    |
|EventTs      |    Number     |      이벤트 발생 시간의 Unix 타임스탬프, 단위: 초 (호환 보관)|
|EventMsTs    |     Number     |     이벤트 발생 시간의 Unix 타임스탬프, 단위: 밀리초  |
| UserId  | String | 사용자 ID                            |
| UniqueId  | Number | 고유 식별자(option: 방 이벤트 그룹) [](id:UniqueId)<br> 클라이언트에 네트워크 전환, 진행 프로세스 이상으로 인한 퇴장 및 재입장 등의 특수 상황이 발생하면, 콜백 서버는 동일한 사용자의 방 입장/퇴장 콜백을 여러 번 수신하게 됩니다. UniqueId는 사용자의 동일한 회차의 방 입장/퇴장을 표시하는 데 사용합니다.|
| Role    | Number | [역할 유형](#role_type)(option: 입장 및 퇴장 시 사용)  |
|TerminalType  |  Number    |   [단말 유형](#terminal)(option: 방 입장 시 사용)|
|UserType  |  Number   |    [사용자 유형](#usertype)(option: 방 입장 시 사용)|
| Reason  | Number | [구체적 원인](#reason) (option: 입장 및 퇴장 시 사용) |


>! '클라이언트의 특수한 행동으로 인한 반복 콜백 필터링' 정책이 배포되었습니다. 2021년 7월 30일 이후에 콜백 서비스에 연결한 경우 기본적으로 새로운 정책이 적용되며, 방 이벤트 그룹은 더 이상 [UniqueId](#UniqueId)(고유 식별자)를 사용하지 않습니다.


[](id:role_type)
### 역할 유형

| 필드 이름             | 값   | 의미 |
| ------------------ | ---- | ---- |
| MEMBER_TRTC_ANCHOR | 20   | 호스트 |
| MEMBER_TRTC_VIEWER | 21   | 시청자 |


[](id:terminal)
### 단말 유형
| 필드 이름             | 값   | 의미 |
| ------------------ | ---- | ---- |
| TERMINAL_TYPE_WINDOWS | 1 | Windows   |
| TERMINAL_TYPE_ANDROID | 2  | Android |
| TERMINAL_TYPE_IOS | 3  | iOS |
| TERMINAL_TYPE_LINUX | 4  | Linux |
| TERMINAL_TYPE_OTHER | 100  | 기타 |

[](id:usertype)
### 사용자 유형
| 필드 이름             | 값   | 의미 |
| ------------------ | ---- | ---- |
| USER_TYPE_WEBRTC | 1 | webrtc   |
| USER_TYPE_APPLET | 2  | 미니프로그램 |
| USER_TYPE_NATIVE_SDK | 3  | Native SDK |


[](id:reason)
### 구체적 원인

| 필드 이름    | 의미                              |
| -------  | --------------------------------- |
|방 입장   |<li/>1: 정상 입장 <li/>2: 네트워크 전환 <li/>3: 요청 시간 초과 후 재시도 <li/>4: 크로스 룸 마이크 연결 방 입장 |
|방 퇴장 | <li/>1: 정상 퇴장 <li/>2: 요청 시간 초과로 퇴장 <li/>3: 방 사용자 삭제됨 <li/>4: 마이크 연결을 취소하고 방 퇴장 <li/>5: 강제 종료|




### 서명 계산
서명은 HMAC SHA256 암호화 알고리즘에 의해 계산됩니다. 사용자의 이벤트 콜백 수신 서버가 콜백 메시지를 수신하면 같은 방식으로 서명을 계산하며, 서명이 동일하면 Tencent Cloud TRTC의 이벤트 콜백이 위조되지 않았음을 의미합니다. 서명 계산 방식은 다음과 같습니다:
```
//서명(Sign) 계산 공식에서 key는 서명 계산용 암호화 키를 의미합니다.
Sign = base64(hmacsha256(key, body))
```

>! body는 콜백 요청을 수신하는 원시 패킷이므로 변경해서는 안 됩니다. 예시는 다음과 같습니다.
>```
>body='{\n\t\'EventGroupId\':\t1,\n\t\'EventType\':\t103,\n\t\'CallbackTs\':\t1615554923704,\n\t\'EventInfo\':\t{\n\t\t\'RoomId\':\t12345,\n\t\t\'EventTs\':\t1608441737,\n\t\t\'UserId\':\t\'test\',\n\t\t\'UniqueId\':\t1615554922656,\n\t\t\'Role\':\t20,\n\t\t\'Reason\':\t1\n\t}\n}'
>```
