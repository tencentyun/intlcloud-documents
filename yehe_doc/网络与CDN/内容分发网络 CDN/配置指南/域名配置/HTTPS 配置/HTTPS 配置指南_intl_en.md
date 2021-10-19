## Configuration Overview
Tencent Cloud CDN supports the HTTPS acceleration service. You can upload certificates to deploy them or directly deploy certificates hosted in Tencent Cloud SSL Certificate Service to the CDN platform. In this way, you can enable the HTTPS acceleration service to implement encrypted data transfer over the entire network.

## Configuration Guide
### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and open the **HTTPS Configuration** tab.
![](https://main.qcloudimg.com/raw/df6c4966cfee58661251f88550214576.png)
You can select **Certificate Management** on the left sidebar to view all domain names configured with HTTPS acceleration under your account.
![](https://main.qcloudimg.com/raw/91335ed0a426118b76ad6b27a53d5197.png)

### Configuring a certificate
#### 1. Select a domain name
On the **Certificate Management** page, click **Configure Certificate** and select the acceleration domain name to be configured with a certificate:
+ The status of the acceleration domain name needs to be "Deploying" or "Enabled". Disabled domain names cannot be configured with HTTPS acceleration.
+ Domain names suffixed with `.file.myqcloud.com` are the default acceleration domain names of Tencent Cloud COS and can use HTTPS acceleration without configuring any certificates.
+ Domain names suffixed with `.image.myqcloud.com` are the default acceleration domain names of Tencent Cloud CI and can use HTTPS acceleration without configuring any certificates.

![](https://main.qcloudimg.com/raw/13c71dc1fc13576620768f7ae61d6c9e.png)

#### 2. Select a certificate
If there is an existing certificate in PEM format, you can directly paste its content and private key to the corresponding fields:
+ CDN supports ECC certificate deployment.
+ The certificate content must be in PEM format. If not, please see [Converting other formats to PEM](https://intl.cloud.tencent.com/document/product/228/35212).
+ You can select a certificate hosted by Tencent Cloud for quick deployment.

![](https://main.qcloudimg.com/raw/d847eb87f076b972808b8e680705f706.png)



### Configuring in batches
Click **Batch Configuration** at the top. You can upload certificates to automatically match domain names for batch configuration:
#### 1. Select a certificate
If there is an existing certificate in PEM format, you can directly paste its content and private key to the corresponding fields:
+ CDN supports ECC certificate deployment.
+ The certificate content must be in PEM format. If not, please see [Converting other formats to PEM](https://intl.cloud.tencent.com/document/product/228/35212).
+ You can select a certificate hosted by Tencent Cloud for quick deployment.

![](https://main.qcloudimg.com/raw/fcadb92849ebd780acbbc5b35f343478.png)

#### 2. Select a domain name
Based on the uploaded or selected certificate, CDN will automatically match the domain names that allow the configuration. You can select the domain names for configuration as needed:
![](https://main.qcloudimg.com/raw/04a8ad1088655f24282201da7b5ebd74.png)



### Changing a certificate
#### Modifying a certificate
Click **Edit** on the right of a certificate to update it for the specified domain name. You can also configure certificates in batches again to override the original certificate configurations.
![](https://main.qcloudimg.com/raw/bb2ed5ec740aa67abf2750dc58baae0d.png)
Certificate updates will seamlessly take effect on nodes one by one across the entire network without affecting the HTTPS service in the production environment. You can also click **Delete** to cancel the HTTPS acceleration service.

#### Certificate expiration
Tencent Cloud will send you expiration reminders through SMS, email, and the Message Center 30, 15, and 7 days before the expiration of your certificate and on the day of its expiration. Currently, reminder recipients for SSL certificates can be customized. You can access the [Message Subscription](https://console.cloud.tencent.com/message/subscription) page for configuration.

### Region-specific configuration
If your domain name is configured for global acceleration, the configured HTTPS certificate will take effect globally. Currently, the certificates configured for the regions in and outside the Chinese mainland must be the same.

If a domain name has different certificates in/outside the Chinese mainland, you will see Chinese mainland and outside Chinese mainland tags on the **Certificate Management** page, which indicate that the domain names with tags have different legacy configurations.

Under the **Advanced Configuration** tab of the domain name, you can also see two configurations:


