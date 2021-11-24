
## Overview
After OCSP stapling (a TLS certificate status query extension) is enabled, the server will send a pre-cached Online Certificate Status Protocol (OCSP) response during the TLS handshake for user verification, so that the user does not need to send a query request to the certificate authority (CA). OCSP stapling greatly improves the efficiency of TLS handshake and reduces user verification time.

Tencent Cloud CDN allows you to enable/disable OCSP stapling.


## Directions
### Viewing the configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to access its configuration page. Under the **HTTPS Configuration** tab, find **OCSP Stapling Configuration**, which is disabled by default:
![](https://main.qcloudimg.com/raw/a0f84d254848ea7c28a0642b3ab1866a.png)

### Modifying the configuration
If a domain name has been configured with HTTPS acceleration, you can directly toggle the OCSP stapling switch to enable/disable this feature. After the certificate configuration is deleted, OCSP stapling will automatically be invalidated:
![](https://main.qcloudimg.com/raw/af090e9a10a99f552c2a57378d0b46ff.png)

> ! If your domain name is configured for global acceleration, the OCSP stapling configuration will take effect globally. This configuration does not distinguish between requests from and outside the Chinese mainland.

