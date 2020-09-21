## Event Push
#### What are the data formats of event pushes?
Currently, DMS supports the following event push data formats:
| Event | Trigger Condition |
|--|--|
| Request (request) | The emailing request succeeds |
| Successful delivery (deliver) | The email arrives at the recipient address |
| Failed delivery (invalid) | The email fails to be sent |
| Soft bounce (soft_bounce) | The recipient rejects the email |
| Spam report (report_spam) | The recipient reports the email as spam |
| Open (open) | The recipient opens the email |
| Click (click) | The recipient clicks a link in the email |

The specific event parameters are as detailed below:

| Parameter | Type | Description |
| -- | -- | -- |
| Event | string | Event type |
| Message | string | Message content |
| SendDomain | string | Sender domain |
| Recipient | string | Recipient |
| RecipientArray | list | Recipient list (request event) |
| EmailId | string | Email ID |
| EmailIds | list | Email ID list |
| RecipientSize | int | Number of requests |
| Url | string | Clicked link |
| Ip | string | Manipulated IP address |
| ExplorerName | string | Browser name |
| ExplorerVer | string | Browser version |
| OSName | string | Operating system name |
| OSVer | string | Operating system version |
| SubStat | string | Failure cause |
| Timestamp | string | Timestamp |
| Token | string | Random string (verification signature) |
| Signature | string | Signature string (verification signature) |