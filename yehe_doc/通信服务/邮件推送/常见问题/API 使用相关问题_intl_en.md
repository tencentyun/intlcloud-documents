### What does the `ReplyToAddresses` parameter mean?
It indicates the email address that the reply message is sent to. For example, when someone receives you email and click “reply”, the reply email will be sent to the address specified by you in `ReplyToAddresses`

### When I tried to send emails, I got the error “FailedOperation.ExceedSendLimit”, indicating that the daily email sending limit has been reached. What is the limit? Can I raise the limit?
Each account can send at most 300,000 emails per day by default. To raise the limit, contact [Tencent Cloud Technical Support](https://console.cloud.tencent.com/workorder/category).

### How should I enter the `Template.TemplateData` in the `SendEmail` API?
`{}` means that no variable is passed in. For details, see the [TemplateData](https://intl.cloud.tencent.com/document/product/1084/39418#Template) field in the API documentation.
