
## Configuration Description
HTTPS refers to Hypertext Transfer Protocol Secure, which is a security protocol that encrypts and transfers data based on the HTTP protocol to ensure the security of data transfer. When configuring HTTPS, you need to provide a certificate for the domain name and deploy it on all ECDN nodes to implement encrypted data transfer across the network.

>!Your domain name should have been connected to ECDN, and the status should be **deploying** or **activated**.

## Adding Configuration
### Selecting domain name
1. Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Domain Management** on the left sidebar to enter the management page.
2. From the list, choose the domain name to configure, click **Manage** to enter your domain details, then select **Advanced Configuration**.  
3. To use HTTPS, you need to deploy the domain name certificate first. Click **Go to Settings** to enter the certificate configuration page.
![](https://main.qcloudimg.com/raw/f6802014b9cea8eda9fbb0eff85fc120.png)

### Configuring certificate
On the certificate configuration page, your domain name can be configured with your certificate or a certificate hosted by Tencent Cloud. For more details, please refer to [Certificate Management](https://intl.cloud.tencent.com/document/product/570/10366).
![](https://main.qcloudimg.com/raw/8a8977310c0f1d6f01a7470a4df234b6.png)



## Modifying Configuration
- **Enabling HTTP2.0:**
To use HTTP2.0 for your configured domain name, enable it on the advanced configuration page.
- **Enabling force HTTPS redirection:**
To force any HTTP request to redirect to HTTPS, enable it for your configured domain name.
You can also specify the status code to redirect, either 301 or 302 (default).
- **Modifying certificates and redirection:**
To modify your certificate or redirection for your configured domain name, click **Go to Configuration** to enter the certificate management page.

![](https://main.qcloudimg.com/raw/e93ea220aa260f173438f1a70907d9ed.png)
