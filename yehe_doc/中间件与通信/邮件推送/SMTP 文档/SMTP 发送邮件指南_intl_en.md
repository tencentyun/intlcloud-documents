## Enabling SMTP Sending Feature
You need to enable the SMTP sending feature and apply for custom permissions through your Tencent Cloud rep first before you can send emails with the SMTP API.
## Directions
### Step 1. Go to the sender address page
Log in to the [SES console](https://console.cloud.tencent.com/ses) and click **Email Configuration** > **Sender Address** on the left sidebar to enter the sender address page.
![](https://qcloudimg.tencent-cloud.cn/raw/fa124df0a9c52d8712e203e25866a389.png)

### Step 2. Configure the SMTP Password
1. In the sender address list, find the one for which you want to enable SMTP sending, and click **Set SMTP Password** in the **Operation** column.
2. Enter the SMTP password in the pop-up window and click **OK**.



## Sending Email via SMTP API
For the SMTP sample code and specific request parameters, response parameters, and error codes, see [SMTP Sample Call](https://intl.cloud.tencent.com/document/product/1084/44456).
>?Emails with attachments can be sent as instructed in [Sending Email with Attachment via SMTP](https://intl.cloud.tencent.com/document/product/1084/44454).

## SMTP Sending Frequency
The current call rate of the SMTP API is limited to 20 times per second under the same Tencent Cloud account `appId`. In addition, the same sender can send up to 10 emails per hour to the same recipient.

We will deliver emails as soon as possible after receiving them. However, due to the different traffic throttling and reputation protection policies of different email systems, in order to improve your email delivery success rate, we recommend you send emails at a lower frequency.


