If you set a callback address, Tencent Cloud will notify the callback address of successful delivery, email rejection, bounce, open, click, unsubscription, and other events. You can configure a callback address in the SES console. For more details, see [Callback Address](https://intl.cloud.tencent.com/document/product/1084/40183).

## Sample Request
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

| Field | Type | Description |
| ---------- | ------ | ---------------------------------------------------------------------------------- |
| event      | string | Event type. For more information, see [Email Event Notification](https://intl.cloud.tencent.com/document/product/1084/39492). |
| email      | string | Recipient address                                                                              |
| link       | string | Clickable URL in the email. This field takes effect only when the value of `event` is `click`.                                               |
| bulkId     | string | `MessageId` returned by `SendEmail`                                                          |
| timestamp  | int    | Event occurrence timestamp                                                                           |
| reason     | string | Cause of email delivery failure                                                                          |
| bounceType | string | Rejection type when the email is rejected by the recipient’s email service provider (ESP). Valid values: soft\_bounce \| hard\_bounce. This field takes effect only when the value of `event` is `bounce`.          |
| username   | string | Tencent Cloud account appId                                                                      |
| from       | string | Sender address (excluding the sender name)                                                                     |
| fromDomain | string | Sender domain                                                                               |
| templateId | int    | Template ID                                                                               |

## Event Types[](id:Event_Type)
Value | Description
--|--
deferred | The delivery of the email has been delayed by the recipient's ESP and is being retried.
delivered | Delivery is successful. The recipient's ESP receives the email.
dropped | The email cannot be delivered and is dropped for some reasons.
open | The recipient opens the email.
click | The recipient clicks the URL in the email.
bounce | The recipient’s ESP rejects the email (usually because the email address is incorrect).
spamreport | The recipient reports the email.
unsubscribe | The recipient clicks the unsubscribe button. The unsubscribe URL should contain the "unsubscribe" keyword.
