Tencent Cloud는 전송 성공, 실패, 이메일 반송, 이메일 오픈, 링크 클릭, 구독 취소 및 기타 이벤트를 메시지 알림 형식으로 콜백 주소에 전달합니다. 다음은 이벤트 푸시 프로토콜 형식입니다.
## 요청 예시
```json
{
  "event": "delivered",
  "email": "example@example.com",
  "bulkId": "qcloud-ses-4F001945B2D9BXXXXXX",
  "timestamp": 1587953211,
  "reason": "the reason when email failed to delivered",
  "bounceType": ""
}
```

필드|유형|설명
--|--|--
event|string|이벤트 유형. 자세한 내용은 [이벤트 유형](#Event_Type)을 참고하십시오.
email|string|수신자 이메일 주소
link|string|수신자가 클릭하는 이메일 URL. 이 필드는 `event="click"`일 때만 적용됩니다.
bulkId|string|SendEmail API에서 반환된 MessageId
timestamp|int|이벤트가 생성된 타임스탬프
reason|string|이메일이 전송되지 않는 이유
bounceType|string|수신자의 이메일 서비스 공급자(ESP)가 이메일을 거부한 경우의 거부 유형. 유효 값: soft &brvbar; hard, 이 필드는`event="bounce"`인 경우에만 적용됩니다.

[](id:Event_Type)
## 이벤트 유형
Value|Description
--|--
processed|전송 중. 이 상태는 중간 상태이며 콜백할 수 없습니다.
deferred|이메일 전달이 수신자의 ESP에 의해 지연되어 재시도 중
delivered|전송 성공. 수신자의 ESP가 이메일을 수신하였습니다.
dropped|이메일을 전달할 수 없으며 어떤 이유로 인해 삭제됨
open|수신자가 이메일을 오픈함
click|수신자가 이메일의 URL을 클릭함
bounce|수신자의 ESP가 이메일을 거부함(일반적인 원인은 잘못된 이메일 주소)
spamreport|수신자가 이메일을 신고함
unsubscribe|수신자가 구독 취소 버튼을 클릭함. 구독 취소 URL에는 "unsubscribe" 키워드가 포함되어야 합니다.
