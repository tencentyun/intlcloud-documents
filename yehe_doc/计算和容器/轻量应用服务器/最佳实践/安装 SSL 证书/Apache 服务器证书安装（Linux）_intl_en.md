## Overview
This document describes how to install an SSL certificate in a Lighthouse instance and enable HTTPS access. The example instance uses an LAMP application image with Apache software pre-installed.

<dx-alert infotype="explain" title="">
The SSL certificate used in the document is provided by Tencent Cloud. For more information on this service, see [Overview](https://intl.cloud.tencent.com/document/product/1007/30152) and [Purchase Guide](https://intl.cloud.tencent.com/document/product/1007/30147).
</dx-alert>



## Preparation
- Install the remote file copy tool such as WinSCP. The latest official version is recommended.
- Install the remote login tool such as PuTTY or Xshell. The latest official version is recommended.
- Open port 443 in your firewall policy. For more information, see [Managing Firewall](https://intl.cloud.tencent.com/document/product/1103/41393).
- The data required to install the SSL certificate includes the following:
<table>
<tr>
<th style="width:35%">Name</th>
<th>Description</th>
</tr>
<tr>
<td>Lighthouse instance's public IP address</td>
<td>Instance IP address used to connect a local computer to the instance.</td>
</tr>
<tr>
<td>Username</td>
<td>The username used to log in to the Lighthouse instance, such as `root`.</td>
</tr>
<tr>
<td>Password or SSH key</td>
<td>The password matching the username used to log in to the Lighthouse instance, or the bound SSH key.</td>
</tr>
</table>
<dx-alert infotype="notice" title="">
You can log in to the [Lighthouse console](https://console.cloud.tencent.com/lighthouse), find the target instance, and enter its details page to view its public IP address. After the instance is created, first reset the password and remember it, or bind an SSH key and save the private key file. For more information, see [Resetting Password](https://intl.cloud.tencent.com/document/product/1103/41553) and [Managing Keys](https://intl.cloud.tencent.com/document/product/1103/41392).
</dx-alert>



## Directions
### Installing certificate
1. Log in to the [SSL Certificates Service console](https://console.cloud.tencent.com/ssl), download and decompress the SSL certificate file (with the name `cloud.tencent.com` as an example here) to a local directory.
After decompression, you can get the relevant certificate files, including the Apache folder and CSR file:
   - **Folder name**: Apache
   - **Files in the folder**:
     - `1_root_bundle.crt`: Certificate file
     - `2_cloud.tencent.com.crt`: Certificate file
     - `3_cloud.tencent.com.key`: Private key file
   - **CSR file**: `cloud.tencent.com.csr` file
 <dx-alert infotype="explain" title="">
 You can upload the CSR file when applying for a certificate or have it generated online by the system. It is provided to the CA and irrelevant to the installation.
 </dx-alert>
2. Log in to the Lighthouse instance. See [Logging In to Linux Instance via WebShell](https://intl.cloud.tencent.com/document/product/1103/41523).
3. Run the following commands in sequence to enter the Apache installation directory and create the `ssl` folder.
```
cd /usr/local/lighthouse/softwares/apache
```
```
sudo mkdir ssl
```
4. Copy the obtained `1_root_bundle.crt`, `2_cloud.tencent.com.crt`, and `3_cloud.tencent.com.key` files from the local directory to the created `/usr/local/lighthouse/softwares/apache/ssl` directory. For more information, see [Uploading Local Files to Lighthouse](https://intl.cloud.tencent.com/document/product/1103/41530).
5. Run the following command to edit the `httpd.conf` configuration file.
```
sudo vim /usr/local/lighthouse/softwares/apache/conf/httpd.conf
```
6. Press **i** to enter the edit mode and make the following changes:
   1. Delete the `#` in `#LoadModule ssl_module modules/mod_ssl.so`.
   2. Delete the `#` in `#LoadModule socache_shmcb_module modules/mod_socache_shmcb.so`.
   3. Replace `localhost` in `ServerName localhost` with the certificate name. A modified sample is as shown below:
```
ServerName cloud.tencent.com
```
   4. Delete the `#` in `#Include conf/extra/httpd-ssl.conf`.
7. Press **Esc** and enter **:wq** to save the changes.
8. Run the following command to modify the `httpd-ssl.conf` configuration file.
```
sudo vim /usr/local/lighthouse/softwares/apache/conf/extra/httpd-ssl.conf
```
9. Press **i** to enter the edit mode and make the following changes in `<VirtualHost _default_:443>`:
   1. Replace `www.example.com:443` in `ServerName www.example.com:443` with the certificate name. A modified sample is as shown below:
```
ServerName cloud.tencent.com
```
   2. Modify the paths of the certificate files:
<dx-codeblock>
::: plaintext 
SSLCertificateFile "/usr/local/lighthouse/softwares/apache/ssl/2_cloud.tencent.com.crt"
SSLCertificateKeyFile "/usr/local/lighthouse/softwares/apache/ssl/3_cloud.tencent.com.key"
SSLCertificateChainFile "/usr/local/lighthouse/softwares/apache/ssl/1_root_bundle.crt"
:::
</dx-codeblock>
  3. Add the following content:
```
<Directory "/usr/local/lighthouse/softwares/apache/htdocs">
          Options Indexes FollowSymLinks
          AllowOverride all
          Require all granted
</Directory>
```
10. Press **Esc** and enter **:wq** to save the changes.
11. Run the following command to restart the Apache service.
```
sudo /usr/local/lighthouse/softwares/apache/bin/httpd -k restart
```
After the successful restart, you can use `https://cloud.tencent.com` for access as shown below:
![](https://main.qcloudimg.com/raw/29d3b81c61d0fbb974703a3ab9140f9f.png)

### (Optional) Setting automatic redirect of HTTP request to HTTPS
You can configure the instance to automatically redirect HTTP requests to HTTPS in the following steps:

1. Run the following command to edit the `httpd.conf` configuration file .
```
sudo vim /usr/local/lighthouse/softwares/apache/conf/httpd.conf
```
2. Press **i** to enter the edit mode and make the following changes:
   1. Delete the `#` in `#LoadModule rewrite_module modules/mod_rewrite.so`.
   2. Find &lt;Directory &quot;/home/www/htdocs/&quot;&gt; and add the following content: 
```
RewriteEngine on
RewriteCond %{SERVER_PORT} !^443$
RewriteRule ^(.*)?$ https://%{SERVER_NAME}%{REQUEST_URI} [L,R]
```
The result should be as follows:
![](https://main.qcloudimg.com/raw/bf7abb0339ef8093b2e6756a64b3b29e.png)
3. Press **Esc** and enter **:wq** to save the changes.
4. Run the following command to restart the Apache service.
```
sudo /usr/local/lighthouse/softwares/apache/bin/httpd -k restart
```
At this point, you have successfully set the automatic redirect to HTTPS. You can use `http://cloud.tencent.com` to redirect to the HTTPS page.

