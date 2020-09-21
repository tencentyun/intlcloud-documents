## Limits
#### What are the limits for emailing?
1. No matter whether you use the console or API, you can send to up to 100 recipients in a single emailing task. You can call the emailing API for multiple times to send batch emails.
2.  You need to use the sender domain of the corresponding type to send emails, that is, you need to use a trigger-type domain name to send triggered emails and batch-type domain name to send batch emails.

#### What are the limits for sender domains?
1. You can verify up to five sender domains. We recommend you create two different domain names for triggered emails and batch emails, respectively. If you want to verify more domain names, please [contact us](https://intl.cloud.tencent.com/contact-sales).
2. We recommend you use a sub-domain name to avoid affecting the primary domain name by issues such as emailing reputation.
3. After a sender address is successfully created for a sender domain, the domain cannot be deleted. Sender domains with no sender addresses added can be deleted.

#### What are the limits for email templates?
1. You can have up to 1,000 email templates.
2. We recommend you add a specific unsubscription link or feedback address in email templates.

#### What are the limits for event pushes?
1. You can set only one URL to receive event pushes from DMS.

#### What are the limits for statistics?
1. The time range for statistics query cannot exceed 7 days.

#### What are the limits for entered characters and file upload size?
The specific character and file size limits are as detailed below:
| Name | Type | Limit |
|--|--|--|
| Task name | Input box | Up to 60 characters |
| Recipient address | Input box + import | Up to 100 addresses |
| Sender address | Input box | It must contain a verified domain name |
| Sender name | Input box | Up to 30 characters |
| Return address | Input box | Up to 3 addresses |
| Email subject | Input box | Up to 60 characters |
| Email body | HTML | Up to 200 KB |
| Custom template variable value | JSON | Up to 100 KB |
| Domain name | Input box | Up to 60 characters |
| Template name | Input box | Up to 60 characters |
| URL | Input box | Up to 60 characters |
| Email address | Input box | Up to 64 characters |