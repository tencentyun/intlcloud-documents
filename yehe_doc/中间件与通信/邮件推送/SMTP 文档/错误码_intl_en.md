## Input Parameters
| Field | Description | Remarks |
| ------------------------- | --------- | -------------------------------------------------------------------------------------------------------------------------------- |
| Bcc | Blind carbon copy address | Currently unsupported |
| Cc | Copy address | Currently unsupported |
| Content-Transfer-Encoding | Content transfer encoding method | Currently unused. You can leave it empty. Content except attachments doesn't need to be encrypted |
| Content-Type | Content type | Currently, you can pass in only `text/plain; charset=UTF-8,text/html; charset=UTF-8 multipart/mixed`, `multipart/related`, or `multipart/alternative`; otherwise, an error will be reported |
| Date | Date and time | Currently unused |
| Delivered-To | Recipient address | Currently unused |
| From | Sender address | Required |
| Message-ID | Message ID | Currently unused |
| MIME-Version | MIME version | Currently unused. Leave it empty or pass in 1.0; otherwise, an error will be reported |
| Received | Transfer path | Currently unused |
| Reply-To | Reply-to address | Currently unused |
| Return-Path | Reply-to address | Currently unused |
| Subject | Subject | Required |
| To | Recipient address | Required |

### Attachment parameters (when sending attachment)
| Field | Description | Remarks |
| ------------------------- | --------- | ------------------------------ |
| Content-Type | Content type | We recommend you pass in `application/octet-stream` for files |
| Content-Transfer-Encoding | Content transfer encoding method | Currently, only Base64 is supported, and an error will be reported if you pass in other values |
| Content-Disposition | Content disposition method | Currently, you can only pass in `attachment`, and attachments cannot be sent if you pass in other values |
| Content-ID | Content ID    | Currently unsupported |
| Content-Location | Content location (path) | Currently unsupported |
| Content-Base | Content base location | Currently unsupported |

>?The input parameter verification requirements are generally the same as those of [SendEmail](https://intl.cloud.tencent.com/document/product/1084/39408), including the restrictions on the number of recipients, email body size, attachment format, and attachment size.

## Response Parameters
The SMTP API has no response parameters and only supports returning the `err` information. If `nil` is returned, it indicates that the API call is successful, but the actual email sending may not be necessarily successful. To get the sending status, see [GetSendEmailStatus](https://intl.cloud.tencent.com/document/product/1084 /39502).

## Error Codes
### System errors
1. There are 2,000 or more characters in a single line in the email body.
`554 5.0.0 Error: transaction failed, blame it on the weather: smtp: too longer line in input stream` or other logs that contain `too longer`.
`write tcp *.*.*.*:60575->*.*.*.*:25: write: broken pipe`

2. The attachment is too large.
If the attachment is about 9 MB in size, EOF will be returned. We recommend you keep the total attachment size below 8 MB and keep the total message size below 10 MB. Otherwise, the content will be truncated, and other exception errors such as Base64 decoding failure will be reported.
				
### Business errors
The format of a business error is as follows:
`
554 5.0.0 Error: transaction failed, blame it on the weather: ##SES-response-json: {"Response":{"RequestId":"bee4e9fb-8127-48cc-b606-bbb1e801596b","QcloudError":{"Error":{"Code":"FailedOperation.MissingEmailContent. The operation failed. The content of the email is missing (`TemplateData` and `Simple` cannot be both empty).
`
 After `##SES-response-json:` is the `json` form of the structure returned by the sending API. The fields are as described below:

| Field | Type | Description |
| ----------- | ------ | ----- |
| RequestId | string | Request ID | 
| QcloudError | stuct | Error structure | 

QcloudError:

| Field | Type | Description | 
| ----------- | ------ | ----- | 
| Code | string | Error code | 
| Message | string | Error message | 



General business error description:

| Error Code | Error Description | Remarks |
| ---------------------------------- | ------------------------------------------------------------------ | ------------------------------------- |
| FailedOperation | msg.From is null | The sender is empty |
| FailedOperation | msg.Subject is null | The subject is empty |
| FailedOperation | msg.Body is null | The message body is empty |
| FailedOperation | Content-Transfer-Encoding must in... | Check the `Content-Transfer-Encoding` parameter against the input parameter description |
| FailedOperation | Content-Type must in... | Check the `Content-Type` parameter in the header against the input parameter description |
| FailedOperation | Mime-Version must in... | Check the `Mime-Version` parameter in the header against the input parameter description |
| FailedOperation | The email is too large. Remove some content... | The email body other than attachments cannot exceed 1 MB in size |
| FailedOperation | Incorrect attachment content. Make sure the base64 content is... | The attachment content must be Base64-encoded |
| FailedOperation | The attachments are too large. Make sure they do not exceed the... | The size of a single attachment exceeds 5 MB, or the total size of all attachments exceeds 10 MB (which may be adjusted) |
| RequestLimitExceeded.SmtpRateLimit | smtp sending frequency limit... | The SMTP call rate limit is reached |

### Other business errors
You can refer to the descriptions of error codes in [SendEmail](https://intl.cloud.tencent.com/document/product/1084/39408).
