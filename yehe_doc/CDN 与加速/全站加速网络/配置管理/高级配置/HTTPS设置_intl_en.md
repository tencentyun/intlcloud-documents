## Configuration Description
HTTPS refers to Hypertext Transfer Protocol Secure, which is a security protocol that encrypts and transfers data based on the HTTP protocol to ensure the security of data transfer. When configuring HTTPS, you need to provide a certificate for the domain name and deploy it on all ECDN nodes to implement encrypted data transfer across the network.

>The configured HTTPS domain name should already have been connected to ECDN, and the domain name status should be **deploying** or **activated**.

## Adding Configuration
### Selecting domain name
1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the management page.
2. In the list, find the domain name to be configured, click **Manage** to enter the details page, and select **Advanced Configuration**.  
3. Deploy a domain name certificate before enabling HTTPS. Click **Configure** to enter the domain name certificate management page.

### Configuring certificate
On the certificate configuration page, you can configure private certificates, Tencent Cloud-hosted certificates, or COS upload acceleration certificate for the domain name. For detailed directions, please see [Certificate Management](https://cloud.tencent.com/document/product/570/10366).
>A COS upload acceleration certificate can be used only by COS upload acceleration domain names.

### Selecting origin-pull method
- If **HTTP origin-pull** is selected, when ECDN nodes perform origin-pull, all requests will use the HTTP protocol.  
- If **Protocol follow** is selected, the origin-pull mode of ECDN nodes will be subject to the user request method, i.e., HTTP requests use HTTP for origin-pull, and HTTPS requests use HTTPS for origin-pull.

## Modifying Configuration
- **Enable HTTP2.0**
If a domain names has been configured with a certificate, you can enable HTTP2.0 on the advanced configuration page.
- **Enable forced redirect to HTTPS
If a domain names has been configured with a certificate, you can enable forced redirect to HTTPS. Then, all HTTP requests will be forcibly converted to HTTPS.
After enabling forced redirect to HTTPS, you can specify whether to use the 301 or 302 status code, and 302 is used by default.
- **Modify the certificate and origin-pull mode**
If a domain names has been configured with a certificate, you can click **Configure** to enter the certificate management page so as to modify the certificate content or origin-pull mode.


