## Overview

This document describes how to install an SSL certificate on an Apache server.

>?
> 
> - The certificate name `cloud.tencent.com` is used as an example.
> - The `Apache/2.4.53` version is used as an example. The default port is `80`. You can download it from the [Apache official website](https://httpd.apache.org/download.cgi/). If you need to use another version, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).
> - The current server OS is Windows Server 2012 R2. Detailed steps vary slightly by OS.
> - Before you install an SSL certificate, enable port `443` on the Apache server so that HTTPS can be enabled after the certificate is installed. For more information, see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738).
> - For detailed directions on how to upload SSL certificate files to a server, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).


## Prerequisites
- Install the Apache service on the current server.

- The data required to install the SSL certificate includes the following:

<table>
<tr>
<td rowspan="1" colSpan="1" >Name</td>
<td rowspan="1" colSpan="1" >Description</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Server IP address</td>
<td rowspan="1" colSpan="1" >IP address of the server, which is used to connect the PC to the server.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Username</td>
<td rowspan="1" colSpan="1" >The username used to log in to the server.</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >Password</td>
<td rowspan="1" colSpan="1" >The password used to log in to the server.</td>
</tr>
</table>


   >?
   > 
   > For a CVM instance purchased on the Tencent Cloud official website, log in to the [CVM console](https://console.cloud.tencent.com/cvm) to get the server IP address, username, and password.
   > 


## Directions

### Step 1. Upload the certificate file
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and click **Download** for the certificate you need to install.

2. In the pop-up window, select **Apache** for the server type, click **Download**, and decompress the `cloud.tencent.com` certificate file package to the local directory.
After decompression, you can get the certificate file of the corresponding type, which includes the `cloud.tencent.com_apache` file.

  - **Folder**: `cloud.tencent.com_apache`

  - **Files in the folder**:

    - `root_bundle.crt`: certificate file

    - `cloud.tencent.com.crt`: certificate file

    - `cloud.tencent.com.key`: Private key file

    - `cloud.tencent.com.csr`: CSR file
      

         >?
         > You can upload the CSR file when applying for a certificate or have it generated online by the system. It is provided to the CA and irrelevant to the installation.
         > 

3. Log in to the Apache server via the RDP port.
   

   >?
   >   - For detailed directions, see [Uploading Files from Linux to Windows CVM using RDP](https://intl.cloud.tencent.com/document/product/213/34822).
   >   - We recommend that you use CVM's file upload feature for deployment to CVM.

4. Copy the `root_bundle.crt` certificate file, `cloud.tencent.com.crt` certificate file, and `cloud.tencent.com.key` private key file from the local directory to the `ssl.crt` and `ssl.key` folders under the `\conf` directory of the Apache server, respectively.

<table>
<tr>
<td rowspan="1" colSpan="1" >SSL Certificate File</td>
<td rowspan="1" colSpan="1" >Folder</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >root_bundle.crt</td>
<td rowspan="2" colSpan="1" >ssl.crt</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >cloud.tencent.com.crt</td>
</tr>
<tr>
<td rowspan="1" colSpan="1" >cloud.tencent.com.key</td>
<td rowspan="1" colSpan="1" >ssl.key</td>
</tr>
</table>


### Step 2. Configure the file
1. Open the `httpd.conf` file in the `conf` directory of the Apache server with a text editor and delete the `#` before the following fields.

   ``` java
   #LoadModule ssl_module modules/mod_ssl.so
   #Include conf/extra/httpd-ssl.conf
   ```
2. Open the `httpd-ssl.conf` file in the `conf\extra` directory of the Apache server with a text editor.

3. Modify the `httpd-ssl.conf` file and set the following field parameters to the paths of the uploaded certificate files as shown below:

   ``` java
   SSLCertificateFile "C:/apache/conf/ssl.crt/cloud.tencent.com.crt"
   SSLCertificateKeyFile "C:/apache/conf/ssl.key/cloud.tencent.com.key"
   SSLCACertificateFile "C:/apache/conf/ssl.crt/root_bundle.crt"
   ```
4. Restart the Apache server and then you can access it through `https://cloud.tencent.com`.

- If the security lock icon is displayed in the browser, the certificate has been installed successfully.

- In case of a website access exception, troubleshoot the issue by referring to the following FAQs:

    - [Website Inaccessible After an SSL Certificate is Deployed](https://intl.cloud.tencent.com/document/product/1007/39821)

    - ["Your Connection is Not Secure" is Displayed After the SSL Certificate is Installed](https://intl.cloud.tencent.com/document/product/1007/40674)

    - [Why Does the Website Prompt "Connection Is Untrusted"?](https://intl.cloud.tencent.com/document/product/1007/30184)

    - [404 Error After the SSL Certificate is Deployed on IIS](https://intl.cloud.tencent.com/document/product/1007/39820)


### (Optional) Security configuration for automatic redirect from HTTP to HTTPS
1. Open the `httpd.conf` file in the `conf` directory of the Apache server with a text editor and delete the `#` before the following fields.

   ``` java
   #LoadModule rewrite_module modules/mod_rewrite.so
   ```
2. Configure the fields in the website running directory. For example, add the following content to the `<Directory "C:/xampp/htdocs">` field:

   ``` java
   <Directory "C:/xampp/htdocs">
   RewriteEngine on
   RewriteCond %{SERVER_PORT} !^443$
   RewriteRule ^(.*)?$ https://%{SERVER_NAME}%{REQUEST_URI} [L,R]
   </Directory>
   ```
3. Restart the Apache server and then you can access it through both `https://www.tencentcloud.com/` (which will be automatically redirected to `https://www.tencentcloud.com/`) and `https://www.tencentcloud.com/`.
