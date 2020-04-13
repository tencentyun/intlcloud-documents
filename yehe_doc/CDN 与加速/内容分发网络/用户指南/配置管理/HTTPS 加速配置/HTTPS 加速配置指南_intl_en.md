## Configuration Scenario
Tencent Cloud CDN supports HTTPS acceleration service. You can upload certificates or directly deploy certificates hosted in Tencent Cloud SSL Certificates Service to the CDN platform. You can thus enable HTTPS acceleration service to implement encrypted data transfer over the entire network.

## Configuration Guide
### Viewing configuration

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. You can find the HTTPS configuration of the specified domain name under the **Advanced Configuration** tab.
![](https://main.qcloudimg.com/raw/df6c4966cfee58661251f88550214576.png)
You can go to **Certificate** page on the left sidebar to view all domain names configured with HTTPS acceleration under your account.
![](https://main.qcloudimg.com/raw/91335ed0a426118b76ad6b27a53d5197.png)

### Configuring the domain name
#### 1. Select a domain name
On the **Certificate** page, click **Configure Certificate** and select the acceleration domain name to be configured with a certificate:
+ The status of the acceleration domain name needs to be "Deploying" or "Activated". Disabled domain names cannot be configured with HTTPS acceleration.
+ The `.file.myqcloud.com` suffix is the default acceleration domain name of Tencent Cloud COS and can use HTTPS acceleration with no certificate configured.
+ The `.image.myqcloud.com` suffix domain name is the default acceleration domain name of Tencent Cloud CI and can use HTTPS acceleration with no certificate configured.

![](https://main.qcloudimg.com/raw/13c71dc1fc13576620768f7ae61d6c9e.png)

#### 2. Select a certificate
If there is an existing certificate in PEM format, you can directly paste its content and private key to the corresponding fields:
+ CDN supports ECC certificate deployment.
+ The certificate content must be in PEM format. If not, please see [Format conversion](https://intl.cloud.tencent.com/document/product/228/35212).
+ You can select a certificate hosted by Tencent Cloud for quick deployment.

![](https://main.qcloudimg.com/raw/d847eb87f076b972808b8e680705f706.png)

#### 3. Origin-pull method

In addition to configuring the origin-pull method when connecting the acceleration domain name or in the origin server configuration section, you can also adjust the origin-pull protocol when configuring a certificate. CDN supports the following three origin-pull protocols:
+ HTTP origin-pull: all requests use HTTP origin-pull.
+ HTTPS origin-pull: all requests use HTTPS origin-pull.
+ Follow protocol: the origin-pull method is based on the request protocol. HTTP requests use HTTP origin-pull, while HTTPS requests use HTTPS origin-pull.

![](https://main.qcloudimg.com/raw/62b122177e6ee043d0063c8e5328e1e5.png)

>
> + If follow protocol or HTTPS origin-pull is configured, you need to deploy a valid certificate on the origin server, otherwise the origin-pull will fail.
> + Currently, HTTPS origin-pull only supports port 443. If another port is specified for the origin server, the configuration will fail.

### Batch configuration
Click **Batch Configuration** at the top. You can upload certificates to automatically match domain names for batch configuration.
#### 1. Select a certificate
If there is an existing certificate in PEM format, you can directly paste its content and private key to the corresponding fields:
+ CDN supports ECC certificate deployment.
+ The certificate content must be in PEM format. If not, please see [Format conversion](https://intl.cloud.tencent.com/document/product/228/35212).
+ You can select a certificate hosted by Tencent Cloud for quick deployment.

![](https://main.qcloudimg.com/raw/fcadb92849ebd780acbbc5b35f343478.png)

#### 2. Select a domain name
CDN will automatically match domain names that allow configuration based on the uploaded or selected certificate. You can select domain names for configuration as needed:
![](https://main.qcloudimg.com/raw/04a8ad1088655f24282201da7b5ebd74.png)

#### 3. Origin-pull method
In addition to configuring the origin-pull method when connecting the acceleration domain name or in the origin server configuration section, you can also adjust the origin-pull protocol when configuring certificates in batches. CDN supports the following three origin-pull protocols:
+ HTTP origin-pull: all requests use HTTP origin-pull.
+ HTTPS origin-pull: all requests use HTTPS origin-pull.
+ Follow protocol: the origin-pull method is based on the request protocol. HTTP requests use HTTP origin-pull, while HTTPS requests use HTTPS origin-pull.

>
> + After batch configurations are submitted, the selected domain names will be deployed with certificates one by one. If an exception occurs, the list page will display a status that shows the update has failed, and the original configuration will still take effect.
> + If the update fails, you can click **Edit** on the right to configure it again.

### Changing certificate
#### Certificate modification
Click **Edit** on the right of the certificate to update it for the specified domain name. You can also configure certificates in batches again to override the original certificate configuration.
![](https://main.qcloudimg.com/raw/a3400bb74990a53a02bc17d7d609b150.png)
Certificate update will take effect on nodes one by one across the entire network seamlessly without affecting HTTPS service in the production environment. You can also click **Delete** to cancel the HTTPS acceleration service.

#### Certificate expiration
Tencent Cloud will send you expiration reminders through SMS, email, and Message Center 30 days, 15 days, and 7 days before your certificate expires as well as on its expiration date. Currently, recipients can be customized for SSL certificates. You can enter the [Message Subscription](https://console.cloud.tencent.com/message/subscription) page for configuration.

### Region-specific configuration
If your acceleration domain name is configured for global acceleration, the configured HTTPS certificate will take effect globally. The certificates configured for Mainland China and outside Mainland China must be the same for the time being.

If a domain name has different certificates within and outside of Mainland China, you will see Mainland China and Outside Mainland China tags on the **Certificate** page, indicating that the domain names have different legacy configurations.

Under the **Advanced Configuration** tab of the domain name, you can also see two configurations.
If your acceleration domain name has different certificate configurations and you want to modify one of the certificates, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

