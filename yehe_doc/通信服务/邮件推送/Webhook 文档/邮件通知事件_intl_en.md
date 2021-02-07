Tencent Cloud will notify the callback address of delivery success, delivery failure, email bounce, email open, click on link, unsubscription, and other events. The protocol format of event pushes is as below:
## Sample Request
```json
{
  "event": "delivered",
  "email": "example@example.com",
  "bulkId": "qcloud-ses-4F001945B2D9BXXXXXX",
  "timestamp": 1587953211,
  "reason": "reason why the email fails to be delivered",
  "bounceType": ""
}
```

Field | Type | Description
--|--|--
event | string | Event type. For details, see [Event Types](#Event_Type).
email | string | Recipient email address
link | string | URL in the email that the recipient clicks. This field takes effect only when the value of `event` is `click`.
bulkId | string | `MessageId` returned by the `SendEmail` API
timestamp | int | Timestamp when the event is generated
reason | string | Reason why the email fails to be delivered
bounceType | string | Rejection type when the email is rejected by the recipient’s email service provider (ESP). Valid values: soft, hard. This field takes effect only when the value of `event` is `bounce`.

## Event Types[](id:Event_Type)
Value | Description
--|--
processed | Delivering. This state is an intermediate state and may not be called back.
deferred | The delivery of the email has been delayed by the recipient's ESP and is being retried.
delivered | Delivery is successful. The recipient's ESP receives the email.
dropped | The email cannot be delivered and is dropped for some reasons.
open | The recipient opens the email.
click | The recipient clicks the URL in the email.
bounce | The recipient’s ESP rejects the email (usually because the email address is incorrect).
spamreport | The recipient reports the email.
unsubscribe | The recipient clicks the unsubscribe button. The unsubscribe URL should contain the "unsubscribe" keyword.
