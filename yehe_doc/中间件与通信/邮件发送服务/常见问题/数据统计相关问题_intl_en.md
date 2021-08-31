## Statistics
#### What does each data dimension mean?
Currently, the statistics of DMS are divided into emailing data and email tracking data. The former includes the numbers of requests, successes, and failures of emailing tasks, and the latter includes the numbers of opens, clicks, and spam reports of emails after they arrive at recipient addresses.

All data dimensions are as detailed below:
| Data Dimension Name | Description |
|--|--|
| Total number | Total number of emails requested to be sent |
| Successful deliveries | Number of emails successfully arriving at recipient email addresses |
| Bounces | Number of emails bounced back by the email service provider. Possible causes include full recipient mailbox, email being marked as spam, etc. |
| Failed deliveries | Number of emails failed to be sent. Possible causes include non-existing recipient address, unreachable server, sender address being blocked, etc. |
| Success rate | Successful deliveries/(total number - failed deliveries), i.e., ratio of successfully delivered emails to valid requests |
| Invalid address rate | Failed deliveries/total number, i.e., ratio of invalid requests to all requests |
| Opens | Total number of times that a successfully delivered email is opened |
| Clicks | Total number of times that a link in a successfully delivered email is clicked |
| Unique opens | Deduplicated number of times that a successfully delivered email is opened (if it is opened for multiple times, they will be counted as one open) |
| Unique clicks | Deduplicated number of times that a link in a successfully delivered email is clicked (if it is clicked for multiple times, they will be counted as one click) |
| Spam reports | Number of times that a successfully delivered email is reported as spam |
