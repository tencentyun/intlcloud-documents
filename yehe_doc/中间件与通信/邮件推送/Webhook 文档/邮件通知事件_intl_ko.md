콜백 주소를 설정하면 Tencent Cloud는 ‘전송 성공, 이메일 거부, 이메일 반송, 이메일 오픈, 링크 클릭, 구독 취소’ 및 기타 이벤트 알림을 콜백 주소에 전달합니다. SES 콘솔에서 콜백 주소를 구성할 수 있습니다. 자세한 내용은 [콜백 주소](https://intl.cloud.tencent.com/document/product/1084/40183)를 참고하십시오.

## 요청 예시
```json
{
    "event":"bounce",
    "email":"example@example.com",
    "bulkId":"qcloudses-30-251200670-date-20220601142439-8jolHvR2XcXC1",
    "timestamp":1654064683,
    "reason":"551 5.1.1 recipient is not exist",
    "bounceType":"hard_bounce",
    "username":"251200670",
    "from":"test@fromexample.com",
    "fromDomain":"fromexample.com",
    "templateId":123456
}
```

| 필드         | 유형     | 설명                                                                                 |
| ---------- | ------ | ---------------------------------------------------------------------------------- |
| event      | string | 이벤트 유형. 자세한 내용은 [이메일 이벤트 알림](https://intl.cloud.tencent.com/document/product/1084/39492) 참고 |
| email      | string | 수신자 주소                                                                              |
| link       | string | 이메일에서 클릭 가능한 URL. 이 필드는 `event="click"`일 때 적용                                               |
| bulkId     | string | SendEmail 에서 반환된 MessageId                                                          |
| timestamp  | int    | 이벤트 발생 타임스탬프                                                                           |
| reason     | string | 이메일 발송 실패 원인                                                                          |
| bounceType | string | 수신자의 이메일 서비스 공급자(ESP)가 이메일을 거부한 경우의 거부 유형. 유효 값: soft\_bounce \| hard\_bounce. 이 필드는 `event="bounce"`인 경우에만 적용           |
| username   | string | Tencent Cloud 계정 appId                                                                      |
| from       | string | 발신자 주소(발신자 이름 제외)                                                                      |
 fromDomain | string | 발신자 도메인                                                                               |
| templateId | int    | 템플릿 Id                                                                               |

## 이벤트 유형[](id:Event_Type)
Value|Description
--|--
deferred|이메일 전달이 수신자의 ESP에 의해 지연되어 재시도 중
delivered|전달 성공. 수신자의 ESP가 이메일을 수신.
dropped|이메일을 전달할 수 없으며 어떤 이유로 인해 삭제됨
open|수신자가 이메일을 오픈함
click|수신자가 이메일의 URL을 클릭함
bounce|수신자의 ESP가 이메일을 거부함(일반적인 원인은 잘못된 이메일 주소)
spamreport|수신자가 이메일을 신고함
unsubscribe|수신자가 ‘구독 취소’ 버튼을 클릭함. 구독 취소 URL에는 "unsubscribe" 키워드가 포함되어야 함.
