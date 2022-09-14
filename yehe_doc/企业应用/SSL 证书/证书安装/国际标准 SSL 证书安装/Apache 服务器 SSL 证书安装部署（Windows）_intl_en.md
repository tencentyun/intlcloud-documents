## Overview
This document describes how to install an SSL certificate on an Apache server.
>?
>- The certificate name `cloud.tencent.com` is used as an example.
>- Apache version: Apache/2.4.53. The default port is `80`. You can download it [here](https://httpd.apache.org/download.cgi/). If you need a different version, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).
>- The current server OS is Windows Server 2012 R2. Detailed steps vary slightly with the OS.
>- Before you install an SSL certificate, enable port 443 on the Apache server so that HTTPS can be enabled after the certificate is installed. For more information, see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738)
>- For more information about how to upload SSL certificate files to a server, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).

## Preparations
- Install the Apache service on the current server.
- The data required to install the SSL certificate includes the following:
<table>
<tr>
<th>Item</th>
<th>Description</th>
</tr>
<tr>
<td>Server IP address</td>
<td>IP address of the server, which is used to connect the PC to the server.</td>
</tr>
<tr>
<td>Username</td>
<td>The username used to log in to the server.</td>
</tr>
<tr>
<td>Password</td>
<td>The password used to log in to the server.</td>
</tr>
</table>

>?For a CVM instance purchased on Tencent Cloud, you can log in to the [CVM console](https://console.cloud.tencent.com/cvm) to get the server IP address, username, and password.

## Directions

### Step 1. Upload the certificate file
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and click **Download** for the certificate you need to install.
2. In the pop-up window, select **Apache** for the server type, click **Download**, and decompress the `cloud.tencent.com` certificate file package to the local directory.
   After decompression, you can get the certificate file of the corresponding type, which includes the `cloud.tencent.com_apache` file.
 - **Folder**: `cloud.tencent.com_apache`
 - **Files in the folder**:
    - `root_bundle.crt`: certificate file
    - `cloud.tencent.com.crt`: certificate file
    - `cloud.tencent.com.key`: private key file
    - `cloud.tencent.com.csr`: CSR file
>?The CSR file is uploaded by you or generated online by the system and is provided to the certificate authority (CA) when you apply for the certificate. It is not relevant to installation.
3. Log in to the Apache server via the RDP port.
>? For upload instructions, see [Uploading Files from Linux to Windows CVM using RDP](https://intl.cloud.tencent.com/document/product/213/34822).

4. Copy the `root_bundle.crt`  certificate file, `cloud.tencent.com.crt` certificate file, and `cloud.tencent.com.key` private secret file from the local directory to the `ssl.crt` and `ssl.key` folders under the `\conf` directory of the Apache server, respectively.
 ![](https://qcloudimg.tencent-cloud.cn/raw/4fa32ebe21bd423c0b11ff8fc4ac4f16.png)
<table>
<thead>
  <tr>
    <th>SSL Certificate File</th>
    <th>Folder</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td>root_bundle.crt</td>
    <td rowspan="2">ssl.crt</td>
  </tr>
  <tr>
    <td>cloud.tencent.com.crt</td>
  </tr>
  <tr>
    <td>cloud.tencent.com.key</td>
    <td>ssl.key</td>
  </tr>
</tbody>
</table>



### Step 2. Configure the file
1. Open the `httpd.conf` file in the `conf` directory of the Apache server with a text editor and delete the `#` before the following fields.
```java
#LoadModule ssl_module modules/mod_ssl.so
#Include conf/extra/httpd-ssl.conf
```
2. Open the `httpd-ssl.conf` file in the `conf\extra` directory of the Apache server with a text editor as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/2adc304cc75d70470d244c4c7fcefce3.png)
3. Modify the `httpd-ssl.conf` file and set the following field parameters to the paths of the uploaded certificate files as shown below:
```java
SSLCertificateFile "C:/apache/conf/ssl.crt/cloud.tencent.com.crt"
SSLCertificateKeyFile "C:/apache/conf/ssl.key/cloud.tencent.com.key"
SSLCACertificateFile "C:/apache/conf/ssl.crt/root_bundle.crt"
```
4. Restart the Apache server and then you can access it through `https://cloud.tencent.com`.

### (Optional) security configuration for automatic redirect from HTTP to HTTPS

1. Open the `httpd.conf` file in the `conf` directory of the Apache server with a text editor and delete the `#` before the following fields.
```java
#LoadModule rewrite_module modules/mod_rewrite.so
```
2. Configure the fields in the website running directory. For example, add the following content to the `<Directory "C:/xampp/htdocs">` field:
```java
<Directory "C:/xampp/htdocs">
RewriteEngine on
RewriteCond %{SERVER_PORT} !^443$
RewriteRule ^(.*)?$ https://%{SERVER_NAME}%{REQUEST_URI} [L,R]
</Directory>
```
3. Restart the Apache server and then you can access it through both `http://cloud.tencent.com` (which will be automatically redirected to `https://cloud.tencent.com`) and `https://cloud.tencent.com`.


