## Configuration Description
HTTPS refers to Hypertext Transfer Protocol Secure, which is a security protocol that encrypts and transfers data based on the HTTP protocol to ensure the security of data transfer. When configuring HTTPS, you need to provide a certificate for the domain name and deploy it on all ECDN nodes to implement encrypted data transfer across the network.

>The configured HTTPS domain name should already have been connected to ECDN, and the domain name status should be  **activated**.

## Adding Configuration
### Selecting domain name
1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the management page.
2. In the list, find the domain name to be configured, click **Manage** to enter the details page, and select **Advanced Configuration**.  
3. Deploy a domain name certificate before enabling HTTPS. Click **Configure** to enter the domain name certificate management page.
![](https://main.qcloudimg.com/raw/f6802014b9cea8eda9fbb0eff85fc120.png)

### Configuring certificate
On the certificate configuration page, you can configure private certificates or Tencent Cloud-hosted certificates for the domain name. For detailed directions, please see [Certificate Management](https://intl.cloud.tencent.com/document/product/570/10366).
![](https://main.qcloudimg.com/raw/8a8977310c0f1d6f01a7470a4df234b6.png)

## Modifying Configuration
- **Enable HTTP2.0**
If a domain names has been configured with a certificate, you can enable HTTP2.0 on the advanced configuration page.
- **Enable forced HTTPS redirection**
If a domain names has been configured with a certificate, you can enable forced HTTPS redirection. Then, all HTTP requests will be forcibly redirected to HTTPS.
After enabling forced HTTPS redirection, you can specify whether to use the 301 or 302 status code for redirection, and 302 is used by default.
- **Modify the certificate **
If a domain name has been configured with a certificate, you can click **Configure** to enter the certificate management page to modify the certificate content.

![](https://main.qcloudimg.com/raw/e93ea220aa260f173438f1a70907d9ed.png)
