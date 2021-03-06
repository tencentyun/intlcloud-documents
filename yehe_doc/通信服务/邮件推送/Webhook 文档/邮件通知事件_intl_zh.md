当邮件产生已递送、失败、退信、打开、点击、取消订阅等事件，腾讯云将以消息通知的方式，传递到回调地址。以下是事件推送的协议格式：
## 请求示例
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

字段|类型|描述
--|--|--
event|string|事件类型，详情请参见 [事件类型](#Event_Type)
email|string|收件人地址
link|string|用户点击的邮件中的链接 URL，仅在`event="click"`时生效
bulkId|string|SendEmail 接口返回的 MessageId
timestamp|int|事件产生的时间戳
reason|string|邮件递送失败的原因
bounceType|string|如果收件人邮件服务商拒信，拒信类型，取值：soft &brvbar; hard，仅在`event="bounce"`的时候生效

[](id:Event_Type)
## 事件类型
Value|Description
--|--
processed|递送中，此状态为中间状态，不一定会回调
deferred|邮件被收件人邮件服务商延迟传递，正在重试中
delivered|递送成功，收件人邮件服务商已接收此邮件
dropped|因为某种原因，这封邮件不能送达，被丢弃
open|收件人打开了此邮件
click|收件人点击了此邮件中的链接
bounce|收件人邮件服务商拒收此邮件（一般是因为邮箱地址错误）
spamreport|收件人举报了此邮件
unsubscribe|收件人点击了业务方的“退订”按钮，需要业务方在退订链接中包含"unsubscribe"关键词
