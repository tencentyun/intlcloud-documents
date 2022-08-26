## Security Notification
### Overview
You can configure to receive alerts in the Message Center when security events are detected.
>?The EdgeOne console is now only available to beta users. [Contact us](https://intl.cloud.tencent.com/contact-us) to join the beta.

### DDoS Attack Alerts

When DDoS attacks on security acceleration and L4 proxy services are detected, and the attack data rate exceeds the configured threshold, you will receive an alert.
>?
>-  EdgeOne monitors the downstream traffic, and automatically cleanses attack traffic once it’s detected.
>-  **DDoS alarms** is only available for security acceleration and L4-proxied resources. Content acceleration resources are not supported.

1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone). Select **Security** > **Alarm Notification** on the left sidebar.
2. On the page that appears, select a site, and click **Set** in the **DDoS alarms** card.
![](https://qcloudimg.tencent-cloud.cn/raw/788fa13249fa12a1ad26809fdb00107a.png)
3. On the pop-up setting page, Click **Edit** next to **Default alarm threshold** You will receive alerts in the Message Center when the DDoS attack traffic data rate exceeds the threshold.
![](https://qcloudimg.tencent-cloud.cn/raw/c1f7e543bb17f585f433144e2580e75f.png)
>?This page displays all eligable resources. For those not configured with custom thresholds, you can modify the **Default alarm threshold**.

4. On the DDoS alarms setting page, toggle on the ![](https://qcloudimg.tencent-cloud.cn/raw/7d363152eb0ea6c823ae278c4d118dc6.png) custom alarm threshold switch for a target resource.
![](https://qcloudimg.tencent-cloud.cn/raw/b22492187707b700f09608aad4fd65df.png)
5. Click **Edit** under the **Custom threshold** column.
![](https://qcloudimg.tencent-cloud.cn/raw/414118509c8e9c6af9691c31348a8e92.png)
6. Enter the alarm threshold (at least 10 Mbps). Click **Save** to make the configuration take effect. 
![](https://qcloudimg.tencent-cloud.cn/raw/66137d737767d969aa15c938377c1451.png)
>? The default alarm threshold is 100 Mbps. You can modify it based on the attack frequency and attack history of your resource.