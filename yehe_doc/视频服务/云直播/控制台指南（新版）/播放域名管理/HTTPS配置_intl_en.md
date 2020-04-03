## Operation Scenarios
The HTTPS protocol is a network protocol built based on the SSL and HTTP protocols for encrypted transfer and authentication, which is more secure than the HTTP protocol. If you want to enable HTTPS acceleration, you can do so by enabling the HTTPS feature for the playback domain name and configuring a correct and valid certificate. You can purchase a certificate from Tencent Cloud [SSL Certificate Service](https://intl.cloud.tencent.com/product/ssl). If you already have one, you can upload it to the LVB Console for configuration. Currently, LVB only supports the PEM format. If your certificate is in another format, you need to convert it to PEM format first. The format requirements and configuration method for the certificate are as follows:

## Prerequisites
- You have logged in to the [LVB Console](https://console.cloud.tencent.com/live).
- You have added a **playback domain name**.

## Directions
### Step 1. Edit the HTTPS configuration
1. Go to **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)**, click the **playback domain** to be configured or **Manage** to enter the Domain Management page.
2. Select **Advanced Configuration** to view the **HTTPS Configuration** tab.
3. Click **Edit** to enter the HTTPS configuration page and set as follows:
	1. Toggle HTTPS service on.
	2. Enter the certificate name, certificate content, and private key content.
	3. Click **Save**.

![](https://main.qcloudimg.com/raw/18435c1538e15846adb77f73ff2d9c05.png)

- **Certificate Name**: custom and used to identify a certificate.
- **Certificate Content**: a certificate provided by the CA includes Apache, IIS, Nginx, and Tomcat files. The encryption service of LVB uses Nginx, so you should select the content of the Nginx files for the configuration.
  ![](https://main.qcloudimg.com/raw/f67e31bfa2c233cf8dc0c4a1e58cb6fc.png)
	The .crt file is the content of the certificate:
	![](https://main.qcloudimg.com/raw/dc6e10861dbe5c4043e07073240cf3b0.png)
  Please enter the entire content between -------BEGIN CERTIFICATE----- and -----END CERTIFICATE----- in the HTTPS certificate content box.
	>If your certificate is issued by an intermediate CA and contains multiple certificates, the certificate content should be spliced as follows:
	> -----BEGIN CERTIFICATE-----
	> -----END CERTIFICATE-----
	> -----BEGIN CERTIFICATE-----
	> -----END CERTIFICATE-----
- **Certificate Private Key**: the content of the .key file in the Nginx files.
  ![](https://main.qcloudimg.com/raw/fdfe6829c5910da0742e2c3d845a8447.png)
  Please enter the entire content between -----BEGIN RSA PRIVATE KEY----- and -----END RSA PRIVATE KEY----- in the HTTPS private key box.

### Step 2. Verify the configuration
The HTTPS configuration will take effect in about 2 hours. Please visit the domain name about 2 hours after the certificate is submitted. If HTTPS is displayed in the address bar of the browser, the configuration is successful.
![](https://main.qcloudimg.com/raw/b1f54ec35855e5d2adbaeae96a04ef13.png)

### Step 3. Modify the configuration
The HTTPS feature can be enabled and disabled. Once it is disabled, LVB will no longer provide HTTPS service for the domain name. If the certificate has expired, it should be replaced with a new valid one.


 >For more information on certificate, please see [SSL Certificate Operation Guide](https://intl.cloud.tencent.com/document/product/1007/30168).
