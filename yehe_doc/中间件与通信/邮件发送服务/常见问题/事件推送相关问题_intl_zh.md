## 事件推送相关问题
#### 事件推送的数据格式是怎样的？
目前腾讯云 DMS 支持的事件推送数据格式如下表:
| 事件 | 触发条件 |
|--|--|
| 请求 (request) | 邮件发送请求成功 |
| 送达 (deliver) | 邮件送达收件人邮箱 |
| 无效 (invalid) | 邮件未发送成功 |
| 退信 (soft_bounce) | 邮件接收方拒收该邮件 |
| 举报 (report_spam) | 用户举报该邮件 |
| 打开 (open) | 用户打开该邮件 |
| 点击 (click) | 用户点击该邮件内的链接 |

具体的事件参数说明如下：

| 参数 | 类型 | 说明 |
| -- | -- | -- |
| Event | string | 事件类型 |
| Message | string | 消息内容 |
| SendDomain | string | 发信域名 |
| Recipient | string | 收件人 |
| RecipientArray | list | 收件人列表（请求事件） |
| EmailId | string | 邮件Id |
| EmailIds | list | 邮件Id列表 |
| RecipientSize | int | 请求个数 |
| Url | string | 被点击的链接 |
| Ip | string | 操作的Ip地址 |
| ExplorerName | string | 浏览器名称 |
| ExplorerVer | string | 浏览器版本 |
| OSName | string | 操作系统名称 |
| OSVer | string | 操作系统版本 |
| SubStat | string | 失败原因 |
| Timestamp | string | 时间戳 |
| Token | string | 随机字符串（验证签名） |
| Signature | string | 签名字符串（验证签名） |