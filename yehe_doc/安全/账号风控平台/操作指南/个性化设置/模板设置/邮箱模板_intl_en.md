## Scenarios
By default, Customer Identity and Access Management (CIAM) provides each tenant with a free email quota of 50 emails. After a tenant exceeds the free quota, the platform will stop sending emails for the tenant, including console test email OTPs and the OTP emails of authentication sources for portal login. To ensure the normal use of services, administrators need to configure email templates to provide email services for platform services.

## Configuring email templates
1. Log in to the [CIAM console](https://console.cloud.tencent.com/ciam) and select **Custom settings** -> **Template settings** -> **Email template** in the left navigation pane.
2. On the **Email template** tab, click **Edit** in the upper right corner.
3. On the edit page, configure the parameters for email service configuration and email template settings, and then click **OK**.

![img](https://qcloudimg.tencent-cloud.cn/raw/fb47cf6b665d5147ec1ed4415b6ba7dd.png)
>? Different email service configurations require different parameters. The platform currently **only supports Tencent Cloud SES** and will allow users to configure other email services in the future. The following parameters are required to configure Tencent Cloud SES.

### Configuring Tencent Cloud SES
The email template settings support different email gateways. After you select a supported email service, the page dynamically loads the configuration information required by the email service.

#### Getting the SecretId and SecretKey
1. Log in to the [Cloud Access Management console](https://console.cloud.tencent.com/cam/overview) and select **Users** -> **User List** in the left navigation pane.
2. On the **User List** page, select the desired sub-account and click the **username** to go to the **User Details** page.
3. On the **User Details** page, click **API Key**, select the desired key, and then click ![](https://qcloudimg.tencent-cloud.cn/raw/0aa6ed67999bf503415c391177264941.png) to copy the SecretId of the sub-account. Click **Show** and verify your identity to view the SecretKey of the sub-account.

#### Getting the sender address
1. Log in to the [SES console](https://console.cloud.tencent.com/ses). In the left navigation pane, click **Configuration** -> **Sender Domain**.
2. On the **Sender Domain** page, click **Create**, enter a domain name, and then click **Submit**. The domain name will be used to create the sender address. For more information, please see [Sender Domain](https://cloud.tencent.com/document/product/1288/55191).
![](https://qcloudimg.tencent-cloud.cn/raw/8331f149f7911553fcfd56c7510ef220.png)
3. On the [Sender Address](https://console.cloud.tencent.com/ses/address) page, click **Create**, configure the parameters, and then click **Submit** to create the sender address. The address will be used to send emails from CIAM.
![img](https://qcloudimg.tencent-cloud.cn/raw/3a9042295c24923e96a7c10892811da5.png)

### Configuring email templates
1. On the [Email Template](https://console.cloud.tencent.com/ses/template) page, click **Create**, configure the parameters, and then click **Submit**. Then, you can use the template to call SES.
![img](https://qcloudimg.tencent-cloud.cn/raw/a7a938fc0fc21dbf3cf34dafce17fa2e.png)

**Parameter description:**
<table>
<thead>
<tr>
<th>Parameter</th>
<th>Description</th>
<th>Parameter template</th>
</tr>
</thead>
<tbody><tr>
<td>Template name</td>
<td>A custom name.</td>
<td>-</td>
</tr>
<tr>
<td>Template type</td>
<td>Choose one as needed. <ul><li>HTML rich text: Supports more styles to show rich content. </li><li>Plain text: Supports text only. </ul></li></td>
<td>-</td>
</tr>
<tr>
<td>Template summary</td>
<td>A custom summary.</td>
<td>-</td>
</tr>
<tr>
<td  rowspan=3 >Email body</td>
<td>Verification code: When you apply for a verification code email template, the email body must contain only the OTP and time placeholders. </td>
<td>Tencent Security: Your email OTP is {{ otp }}. The OTP is valid for {{ time }} seconds. </td>
</tr>
<tr>
<td>Reset password: When you apply for a reset password email template, the email body must contain only the name, mailverifycode, and time placeholders. </td>
<td>Tencent Security: Dear {{ name }}, you have requested to reset your password. The verification code for resetting your password is  {{ mailverifycode }}. The code is valid for  {{ time }} seconds. </td>
</tr>
<tr>
<td>Retrieve username: When you apply for a retrieve username email template, the email body must contain only the name placeholder. </td>
<td>Tencent Security: Dear user, you have requested to retrieve your username {{ name }}. </td>
</tr>
</tbody></table> 

2. On the **Email Template** page, you can view the template you just created and copy the template ID.

3. In the Email template settings section of CIAM, you need to fill in the IDs of the three approved sending templates: verification code, reset password, and retrieve username.

 ![img](https://qcloudimg.tencent-cloud.cn/raw/a4a8e103fc369ac4f876a4d0ca4860f7.png)

## Testing email services
1. After configuring the email template settings, you can click **Test now**.
![img](https://qcloudimg.tencent-cloud.cn/raw/3d901eef499a2c9fb907483b2996cbe4.png)
2. In the **Email service test** window displayed, enter a valid test email address, select a test template, and then click **Send** to verify the configuration.
![img](https://qcloudimg.tencent-cloud.cn/raw/c075109687a2ea6a9011b5cf0cac24ba.png)