## Scenario
The HTTPS protocol is a network protocol built based on the SSL and HTTP protocols for encrypted transfer and authentication, which is more secure than the HTTP protocol. If you want to enable HTTPS acceleration, you can do so by enabling the HTTPS feature for the playback domain name and configuring a correct and valid certificate. You can purchase a certificate from Tencent Cloud [SSL Certificate Service](https://intl.cloud.tencent.com/product/ssl). If you already have one, you can upload it to the LVB Console for configuration. Currently, LVB only supports the PEM format. If your certificate is in another format, you need to convert it to PEM format first. The format requirements and configuration method for the certificate are as follows:


## Steps
### Step 1. Log in to the console
 Log in to the [LVB Console](https://console.cloud.tencent.com/live), select **Manage Domain** in the left sidebar, click the playback domain name to be configured or click **Manage** in the operation column to enter the domain name management page.
 ![](https://main.qcloudimg.com/raw/e8f36e73f5d5cb0cb083a6f8a84f4837.png)

### Step 2. Edit the HTTPS configuration
In the **Advanced Configuration** tab, click **Edit** in the **HTTPS Configuration** module, enable the HTTPS service, enter the certificate name, certificate content, and private key content, and click "Save" to start the HTTPS service.
![](https://main.qcloudimg.com/raw/18435c1538e15846adb77f73ff2d9c05.png)
- **Certificate Name**: certificate names are customized for the purpose of differentiation.
- **Certificate Content**: A certificate provided by the CA includes Apache, IIS, Nginx, and Tomcat files. The encryption service of LVB uses Nginx, so you need to select the content of the Nginx files for the configuration.
  ![](https://main.qcloudimg.com/raw/f67e31bfa2c233cf8dc0c4a1e58cb6fc.png)
	The .crt file is the content of the certificate:
	![](https://main.qcloudimg.com/raw/dc6e10861dbe5c4043e07073240cf3b0.png)
  Please enter the entire content including -------BEGIN CERTIFICATE----- and -----END CERTIFICATE----- in the HTTPS certificate content box.
	> Note: If your certificate was issued by an intermediate CA and consists of multiple certificates, please splice the certificates as follows:
	> -----BEGIN CERTIFICATE-----
	> -----END CERTIFICATE-----
	> -----BEGIN CERTIFICATE-----
	> -----END CERTIFICATE-----
- **Certificate Private Key**: the content of the .key file in the Nginx files.
  ![](https://main.qcloudimg.com/raw/fdfe6829c5910da0742e2c3d845a8447.png)
  Please enter the entire content including -----BEGIN RSA PRIVATE KEY----- and -----END RSA PRIVATE KEY----- in the HTTPS certificate private key box.

### Step 3. Verify the configuration
The HTTPS configuration will take effect in about 2 hours. Please visit the domain name about 2 hours after the certificate is submitted. If HTTPS is displayed in the address bar of the browser, the configuration is successful.
![](https://main.qcloudimg.com/raw/b1f54ec35855e5d2adbaeae96a04ef13.png)

### Step 4. Modify the configuration
The HTTPS feature can be enabled and disabled. Once it is disabled, LVB will no longer provide HTTPS service for the domain name. An expired certificate needs to be replaced by a new valid one.
  
