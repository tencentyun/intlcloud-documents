## Overview
EdgeOne provides a one-stop certificate application, upload, management, and deployment service for site acceleration. This implements centralized management and quick deployment of edge SSL certificates. EdgeOne certificates are divided into the following three types:
- Universal certificate: During NS connection, once a site takes effect, the system will generate a universal certificate for its root domain (example.com) and third-level wildcard domain (*.example.com) and automatically deploy and update it.

- Uploaded custom certificate: It is a certificate you upload in the [EdgeOne](https://console.cloud.tencent.com/edgeone) or [SSL Certificates](https://console.cloud.tencent.com/ssl) console.
- Tencent Cloud-managed certificate: It is a certificate that you purchase or apply for free of charge in the [SSL Certificates console](https://console.cloud.tencent.com/ssl).

>?
>- Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.
>- Universal certificates are dedicated to the NS connection method and won't be provided by the system during CNAME connection.
>- After you switch from NS connection to CNAME connection, the universal certificate will be retained but not updated and will be automatically deleted upon expiration.
>- Uploaded custom certificates and Tencent Cloud-managed certificates in EdgeOne are synced with those in the [SSL Certificates console](https://console.cloud.tencent.com/ssl).


## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and click **Certificate management** > **Edge node certificate** on the left sidebar.
2. On the edge node certificate page, select the target site and click **Configure certificate**.
![](https://qcloudimg.tencent-cloud.cn/raw/a06314f676000b72c65fba7a0ac64a89.png)
3. On the certificate configuration page, select the target domain, and certificates in the [SSL Certificates console](https://console.cloud.tencent.com/ssl) that can be associated with the domain will be automatically displayed in the certificate list.
![](https://qcloudimg.tencent-cloud.cn/raw/c08ae1f42b16136c9913d9ebd6ee96d0.png)
4. If there are no available certificates, you can click **Upload custom certificate** to upload one.
![](https://qcloudimg.tencent-cloud.cn/raw/872ed3306bb2d76422fa71c34958d23c.png)
5. Select the target certificate and click **OK**. Then, the certificate will be automatically deployed to EdgeOne acceleration nodes.
>? If the domain has been associated with a certificate, reassociation will overwrite the old certificate.
