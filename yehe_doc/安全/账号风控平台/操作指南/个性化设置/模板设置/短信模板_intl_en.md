## Scenarios
By default, Customer Identity and Access Management (CIAM) provides each tenant with a free SMS quota of 50 SMS messages. After a tenant exceeds the free quota, the platform will stop sending SMS messages for the tenant, including console test SMS messages and the OTP SMS messages of authentication sources for portal login. To ensure the normal use of services, administrators need to configure SMS templates to provide SMS services for platform services.

## Configuring SMS templates
1. Log in to the [CIAM console](https://console.cloud.tencent.com/ciam) and select **Custom settings** -> **Template settings** -> **SMS message template** in the left navigation pane.

2. On the **SMS message template** tab, click **Edit** in the upper right corner.

3. On the edit page, configure the parameters for SMS service configuration and verification code SMS, and then click **OK**.

![img](https://qcloudimg.tencent-cloud.cn/raw/305a27c279875c970f919ae60062b444.png)
>? Different SMS service configurations require different parameters. The platform currently **only supports Tencent Cloud SMS** and will allow users to configure other SMS services in the future. The following parameters are required to configure Tencent Cloud SMS.

### Configuring Tencent Cloud SMS
#### Getting the SDK AppID
1. Log in to the [SMS console](https://console.cloud.tencent.com/smsv2) and select **Application Management** -> **Application List** in the left navigation pane.
2. On the **Application List** page, click **Create Application**, configure the application name, application intro, and tags, and then click **Create**.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/9fb501511973763e47f74f82920b48a7.png)
3. On the **Application List** page, select the desired application and click ![](https://qcloudimg.tencent-cloud.cn/raw/0aa6ed67999bf503415c391177264941.png) to copy the SDK AppID of the application.
   ![img](https://qcloudimg.tencent-cloud.cn/raw/724fe2cc923fd53679e351c270135084.png)

#### Getting the SecretId and SecretKey
1. Log in to the [Cloud Access Management console](https://console.cloud.tencent.com/cam/overview) and select **Users** -> **User List** in the left navigation pane.
2. On the **User List** page, select the desired sub-account and click the **username** to go to the **User Details** page.
3. On the **User Details** page, click **API Key**, select the desired key, and then click ![](https://qcloudimg.tencent-cloud.cn/raw/0aa6ed67999bf503415c391177264941.png) to copy the SecretId of the sub-account. Click **Show** and verify your identity to view the SecretKey of the sub-account.
   
### Configuring SMS templates
To configure SMS templates, you need to obtain the SMS signature and template ID required to send an SMS message in the following ways:
#### Getting the SMS signature
1. Log in to the [SMS console](https://console.cloud.tencent.com/smsv2) and select **Global SMS** -> **Signatures** in the left navigation pane.
2. On the **Signatures** page, click **Create Signature**, fill in the parameters, and then click **OK**.
![img](https://qcloudimg.tencent-cloud.cn/raw/85c2234c81b711647d38e90a51d74982.png)
3. Upon approval, you can view the SMS signature on the **Signatures** page.

#### Getting the template ID
1. Log in to the [SMS console](https://console.cloud.tencent.com/smsv2) and select **Global SMS** -> **Body Templates** in the left navigation pane.
2. On the **Body Templates** page, click **Create Body Template**, fill in the parameters, and then click **OK**.
![img](https://qcloudimg.tencent-cloud.cn/raw/198eb832687a1796828b428eb1af64d5.png)
3. Upon approval, you can view the template ID on the **Body Templates** page.