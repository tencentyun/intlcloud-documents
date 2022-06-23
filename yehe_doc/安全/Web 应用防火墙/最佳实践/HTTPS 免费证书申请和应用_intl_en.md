## Prerequisites
WAF supports the configuration and protection of HTTPS access to domain names. If your website has not been altered for the HTTPS protocol, you can apply for a DV certificate free of charge in the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl). After your application is approved, you can associate the certificate in the WAF console and then easily implement access and client connection to the entire website over HTTPS without modifying the real server.
## Associating HTTPS Certificate
1. Log in to the [WAF console](https://console.cloud.tencent.com/guanjia/tea-instance-new) and select **Instance management** > **Instance list** on the left sidebar.
2. On the **Instance list** page, select the target instance and click **Domain name connection**.
![](https://qcloudimg.tencent-cloud.cn/raw/25a44639607badfacf5ae16a12f47ec0.png)

3. On the **Domain name connection** page, click **Add domain name**.
4. In **Server configuration** of the domain name configuration, select **HTTPS**. In **Certificate configuration**, click **Associated certificate**.
>?The certificate format should be PEM and the content should be text.

![](https://qcloudimg.tencent-cloud.cn/raw/ed5bc393282522bb7a4e165d61ab4f71.png)

4. Select **Tencent Cloud-managed certificate** as the **Certificate source**. Then, WAF will automatically associate an available certificate of the domain name. After the configuration is completed, click **Save**.
![](https://qcloudimg.tencent-cloud.cn/raw/2103a7588353970833b5eebc0d4ca715.png)

5. Enable **HTTPS forced jump** and select the **HTTP** access protocol above. Select **HTTP** for **HTTPS origin-pull method** and set other parameters as needed; then, your website will support HTTPS access.

>! To enable **HTTPS forced jump**, you need to select both **HTTP** and **HTTPS** access protocols.

![](https://qcloudimg.tencent-cloud.cn/raw/d0c34b17b62b0c8fb6415c08e5ccbc50.png)

