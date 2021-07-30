Normally, live streaming domain names use the Hypertext Transfer Protocol (HTTP). HTTP can be converted to Hyper Text Transfer Protocol over Secure Socket Layer (HTTPS) using SSL/TLS protocol for encrypted data transmission. You can go to **Certificate Management** to query and configure SSL certificates for domain names.

## How to Configure
The purpose of configuring an SSL certificate for a domain name is to encrypt key user data for secure transmission. A Secure Sockets Layer (SSL) certificate allows a site to switch from HTTP to its SSL-based encrypted version, HTTPS. 

[](id:c_ssl)
## Configuring Certificate
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** in the CSS console, and click **Certificate Management** to go to the certificate management page.
![](https://main.qcloudimg.com/raw/e39413b101a445ed747d78c8c9e7c8ac.png)
2. Click **Configure Certificate** to add a certificate configuration.
![](https://main.qcloudimg.com/raw/5aeee06ba8b978b823be16e9191bf705.png)
3. In the certificate configuration pop-up, select a certificate source:
  - **Self-owned certificate**: enter remarks, content, and key of this certificate. After the configuration is saved, the certificate info will be synced to [Certificate Management](https://console.cloud.tencent.com/ssl) in the SSL Certificate Service console. For details about how to set the certificate content and key, please see [HTTPS Configuration](https://intl.cloud.tencent.com/document/product/267/31066).
![](https://main.qcloudimg.com/raw/998de2fdadf6ed9ab52e7fdcef288f51.png)
  - **Tencent Cloud-hosted certificate**: select a certificate you purchased in the SSL Certificate Service console.
![](https://main.qcloudimg.com/raw/4f36c491c7392798bc81410ecc65ae6e.png)
4. After the certificate is confirmed to be available, click **Next** to enter the domain name configuration page.
5. In **Bind Domain Names**, select one or more playback domain names which match the certificate. If a selected domain name is already bound to a certificate, the new certificate will apply.
6. In **Selected**, you can view selected domain names and whether their HTTPS configuration is enabled.
![](https://main.qcloudimg.com/raw/bc1a0c51023d295120b8c94420b7b628.png)
7. Choose whether to enable HTTPS Configuration for selected domain names:
  >? 
  >- Toggling **Enable HTTPS Configuration** on will enable HTTPS configuration for the domain names.
  >- **Enable HTTPS Configuration** is enabled by default. If you toggle this button off, the HTTPS configuration status of the domain names will not change after binding, with only their certificate updated.
6. Click **Confirm**.


[](id:check)
## Viewing Certificate Configuration
After you [configure a certificate](#c_ssl), you can go to **[Certificate Management](https://console.cloud.tencent.com/live/common/certificate)** to view its configuration, including the domain name, remarks, source, HTTPS configuration, and expiration time.
![](https://main.qcloudimg.com/raw/e4012e075b695afc912840462e0c5694.png)

[](id:update)
## Updating Certificate Configuration
1. Go to **[Certificate Management](https://console.cloud.tencent.com/live/common/certificate)**, find the target certificate configuration in the list, and click **Update** on its right.
![](https://main.qcloudimg.com/raw/bfad71179c2ab41cd3c35e23e47e0224.png)
2. On the certificate configuration page, [configure the certificate](#c_ssl) again.
3. Click **Confirm**.

[](id:delete)
## Deleting Certificate Configuration
1. Go to **[Certificate Management](https://console.cloud.tencent.com/live/common/certificate)**, find the target certificate configuration in the list, and click **Delete** on its right.
![](https://main.qcloudimg.com/raw/a5d8f92c8aa7f2264c56e5ef6bf1f15b.png)
2. In the confirmation pop-up, click **Confirm**.
![](https://main.qcloudimg.com/raw/10305e0609cfcda523505cbcf8a099c8.png)
>! After unbinding the certificate, the domain names cannot use HTTPS configuration.


