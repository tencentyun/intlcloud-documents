## Configuration
Tencent Cloud CDN supports the HTTPS acceleration service. You can upload certificates to deploy them or directly deploy certificates hosted in Tencent Cloud SSL Certificate Service to the CDN platform. In this way, you can enable the HTTPS acceleration service to implement encrypted data transfer over the entire network.

## Configuration Guide
### Viewing the configuration

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to access its configuration page. You can find the HTTPS configuration of the specified domain name under the **Advanced Configuration** tab.
![](https://main.qcloudimg.com/raw/df6c4966cfee58661251f88550214576.png)
You can access the **Certificate Management** page on the left sidebar to view all domain names configured with HTTPS acceleration under your account.
![](https://main.qcloudimg.com/raw/91335ed0a426118b76ad6b27a53d5197.png)

### Configuring a certificate
#### 1. Select a domain name
On the **Certificate Management** page, click **Configure Certificate** and select the acceleration domain name to be configured with a certificate:
+ The status of the acceleration domain name needs to be "Deploying" or "Activated". Disabled domain names cannot be configured with HTTPS acceleration.
+ The `.file.myqcloud.com` suffix is the default acceleration domain name of Tencent Cloud COS and can use HTTPS acceleration without configuring any certificates.
+ The `.image.myqcloud.com` suffix domain name is the default acceleration domain name of Tencent Cloud CI and can use HTTPS acceleration without configuring any certificates.

![](https://main.qcloudimg.com/raw/13c71dc1fc13576620768f7ae61d6c9e.png)

#### 2. Select a certificate
If there is an existing certificate in PEM format, you can directly paste its content and private key to the corresponding fields:
+ CDN supports ECC certificate deployment.
+ The certificate content must be in PEM format. If not, please see [Converting other formats to PEM](https://intl.cloud.tencent.com/document/product/228/35212).
+ You can select a Tencent Cloud-hosted certificate for quick deployment.

![](https://main.qcloudimg.com/raw/d847eb87f076b972808b8e680705f706.png)

#### 3. Origin-pull method

In addition to setting the origin-pull mode in the origin server configuration module or when connecting the acceleration domain name, you can also adjust the origin-pull protocol when configuring a certificate. CDN supports the following three origin-pull protocols:
+ HTTP origin-pull: all requests use HTTP origin-pull.
+ HTTPS origin-pull: all requests use HTTPS origin-pull.
+ Follow protocol: the origin-pull mode is based on the request protocol. HTTP requests use HTTP origin-pull, while HTTPS requests use HTTPS origin-pull.

![](https://main.qcloudimg.com/raw/62b122177e6ee043d0063c8e5328e1e5.png)

>
> + When configuring follow protocol or HTTPS origin-pull, you need to deploy a valid certificate on the origin server. Otherwise, origin-pull will fail.
> + HTTPS origin-pull currently only supports port 443. If you specify another port for the origin server, the configuration will fail.

### Configuring in batches
Click **Batch Configuration** at the top. You can upload certificates to automatically match domain names for batch configuration.
#### 1. Select a certificate
If there is an existing certificate in PEM format, you can directly paste its content and private key to the corresponding fields:
+ CDN supports ECC certificate deployment.
+ The certificate content must be in PEM format. If not, please see [Converting other formats to PEM](https://intl.cloud.tencent.com/document/product/228/35212).
+ You can select a Tencent Cloud-hosted certificate for quick deployment.

![](https://main.qcloudimg.com/raw/fcadb92849ebd780acbbc5b35f343478.png)

#### 2. Select a domain name
Based on the uploaded or selected certificate, CDN will automatically match the domain names that allow the configuration. You can select the domain names for configuration as needed:
![](https://main.qcloudimg.com/raw/04a8ad1088655f24282201da7b5ebd74.png)

#### 3. Origin-pull method
In addition to setting the origin-pull mode in the origin server configuration module or when connecting the acceleration domain name, you can also adjust the origin-pull protocol in batches when configuring certificates in batches. CDN supports the following three origin-pull protocols:
+ HTTP origin-pull: all requests use HTTP origin-pull.
+ HTTPS origin-pull: all requests use HTTPS origin-pull.
+ Follow protocol: the origin-pull mode is based on the request protocol. HTTP requests use HTTP origin-pull, while HTTPS requests use HTTPS origin-pull.

>
> + After the configurations are submitted in batches, the selected domain names will be deployed with a certificate one by one. If an exception occurs, the list page will display the "Failed to update" status, and the original configuration will continue to take effect.
> + If the update fails, you can click **Edit** on the right to configure it again.

### Changing a certificate
#### Modifying a certificate
Click **Edit** on the right of a certificate to update it for the specified domain name. You can also configure certificates in batches again to override the original certificate configurations.
![](https://main.qcloudimg.com/raw/bb2ed5ec740aa67abf2750dc58baae0d.png)
Certificate updates will seamlessly take effect on nodes one by one across the entire network without affecting the HTTPS service in the production environment. You can also click **Delete** to cancel the HTTPS acceleration service.

#### Certificate expiration
Tencent Cloud will send you expiration reminders through SMS, email, and the Message Center 30, 15, and 7 days before the expiration of your certificate and on the day of its expiration. Currently, reminder recipients for SSL certificates can be customized. You can access the [Message Subscription](https://console.cloud.tencent.com/message/subscription) page for configuration.

### Region-specific configuration
If your acceleration domain name is configured for global acceleration, the configured HTTPS certificate will take effect globally. Currently, the certificates configured for mainland China and outside mainland China must be the same.

If a domain name has different certificates in/outside mainland China, you will see mainland China and outside mainland China tags on the **Certificate Management** page, which indicate that the domain names with tags have different legacy configurations.
![](https://main.qcloudimg.com/raw/23192c43c0611c34d07490f19ea7dfb0.png)
Under the **Advanced Configuration** tab of the domain name, you can also see two configurations:
![](https://main.qcloudimg.com/raw/febb17a67f10eb81941013895e67913f.png)
If your acceleration domain name has different certificate configurations and you want to change one of the certificates, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

