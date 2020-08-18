## Prerequisites
WAF supports configuration and protection of HTTPS access to domain names. If your website has not been altered for the HTTPS protocol, you can apply for a DV certificate free of charge in the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl). After the application is approved, you can associate the certificate in the WAF Console; then, you can easily implement access and client connection to the entire website over HTTPS without modifying the real server. For more information on how to apply for a free DV SSL certificate, please see [Applying for DV Certificates](https://cloud.tencent.com/document/product/400/6814).
## Associating HTTPS Certificate
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and select **Web Application Firewall** > **Protection Settings** on the left sidebar.
2. On the protection settings page, click **Add Domain Name** to enter the domain name adding page.
3. In server configuration on the page, select **HTTPS**. In certificate configuration, click **Associate Certificate**.
![](https://main.qcloudimg.com/raw/f2509c947abbc6898217e031c15fa572.png)
4. Select "Tencent Cloud-hosted Certificate" as the certificate source. Then, WAF will automatically associate an available certificate of the domain name. After the configuration is completed, click **Save**.
![](https://main.qcloudimg.com/raw/0462e4ff8f1d785ba4c04f87336526a0.png)
5. Enable forced HTTPS redirect, select the **HTTP** access protocol above, select "HTTP" as the "HTTPS Origin-pull Method", and set other parameters as needed; then, your website will support HTTPS access.
>To enable forced HTTPS redirect, you need to select both HTTP and HTTPS access protocols.
>
![](https://main.qcloudimg.com/raw/6bc4cc021c6b70968f628868e77f948e.png)

