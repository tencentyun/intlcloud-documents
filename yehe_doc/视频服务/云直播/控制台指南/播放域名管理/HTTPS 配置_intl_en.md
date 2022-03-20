## Overview
The HTTPS protocol is a network protocol built based on the SSL and HTTP protocols for encrypted transfer and authentication, which is more secure than the HTTP protocol. If you want to enable HTTPS acceleration, you can do so by enabling the HTTPS feature for the playback domain name and configuring a correct and valid certificate. You can purchase a certificate from Tencent Cloud [SSL Certificate Service](https://intl.cloud.tencent.com/product/ssl). If you already have one, you can upload it to the CSS console for configuration. Currently, CSS only supports the PEM format. If your certificate is in another format, you need to convert it to PEM format first. The format requirements and configuration method for the certificate are as follows:

## Prerequisites
- You have logged in to the [CSS console](https://console.cloud.tencent.com/live).
- You have [added a playback domain name](https://intl.cloud.tencent.com/document/product/267/35970).

## Directions 
### Step 1. Edit the HTTPS configuration
1. Enter **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** and click the **playback domain name** to be configured or **Manage** on the right to enter the domain name details page.
2. Select **Advanced Configuration** and find the **HTTPS Configuration** section.
3. Click **Edit** and click ![](https://main.qcloudimg.com/raw/897761946b06e8f904bfa6301d282817.png) to enable the HTTPS service.
4. Select the source of the certificate to be configured, enter relevant information, and click **Save**.
<table>
<tr><th>Certificate Source</th><th>Required Configuration Items</th></tr>
<tr>
<td>Self-owned certificate</td>
<td><ul style="margin:0">
<li>Certificate Name: enter a custom name used to identify the certificate..</li>
<li>Certificate Content: enter the content of the <code>.crt</code> file for Nginx. For more information, please see <a href="#content">Certificate content</a>.</li>
<li>Private Key Content: enter the content of the <code>.key</code> file for Nginx. For more information, please see <a href="#private_key">Certificate key</a>.</li><ul></td>
</tr><tr>
<td>Tencent Cloud-hosted certificate</td>
<td>Certificate List: select an uploaded certificate in <a href="https://console.cloud.tencent.com/ssl">SSL Certificate Service</a>.</td>
</tr></table>
<img src="https://main.qcloudimg.com/raw/b42458905e48db6b45def7a1d8ecc349.png"></img>

#### Certificate description
A certificate provided by the [CA](https://intl.cloud.tencent.com/document/product/1007/30192#354) includes Apache, IIS, Nginx, and Tomcat files. **The encryption service of CSS uses Nginx, so you should select the content of the Nginx files for the configuration.** 
Go to **SSL Certificate Service console** > **[Certificate Management](https://console.cloud.tencent.com/ssl)**, select the target certificate, click **Download** in the "Operation" column, and decompress the downloaded package to get the following files:
  ![](https://main.qcloudimg.com/raw/f67e31bfa2c233cf8dc0c4a1e58cb6fc.png)
- <b id="content">Certificate content</b>: enter the entire content between `-----BEGIN CERTIFICATE-----` and `-----END CERTIFICATE-----` in the `.crt` file for Nginx.
**Sample content:**
![](https://main.qcloudimg.com/raw/e6c61fda3637a2f11e56cec30f0f7bd3.png)
>?If your certificate is issued by an intermediate CA and contains multiple certificates, the certificate content should be spliced as follows:
> -----BEGIN CERTIFICATE-----
> -----END CERTIFICATE-----
> -----BEGIN CERTIFICATE-----
> -----END CERTIFICATE-----
- <b id="private_key">Certificate private key</b>: enter the entire content between ` -----BEGIN RSA PRIVATE KEY----- ` and `-----END RSA PRIVATE KEY----- ` in the `.key` file for Nginx.
**Sample content:**
![](https://main.qcloudimg.com/raw/1ca20b0021b49ccb407df43675be37ba.png)

### Step 2. Verify the configuration
The HTTPS configuration will take effect in about 2 hours. Please visit the domain name about 2 hours after the certificate is submitted. If HTTPS is displayed in the address bar of the browser, the configuration is successful.
![](https://main.qcloudimg.com/raw/b1f54ec35855e5d2adbaeae96a04ef13.png)

### Step 3. Modify the configuration
The HTTPS feature can be enabled and disabled. Once it is disabled, CSS will no longer provide HTTPS service for the domain name. If the certificate has expired, it should be replaced with a new valid one.

