## Scenarios
This document describes how to install an SSL certificate on an Apache server.
>?
>- The certificate name `www.domain.com` is used as an example in this document.
>- `Apache/2.4.6` is used as an example. The default port is `80`.
>- The current server OS is CentOS 7. Detailed steps vary slightly with the OS version.
>- Before installing the SSL certificate, open the port 443 on the Apache server to ensure that HTTPS can be enabled after certificate installation. For more information, see [How Do I Open the Port 443 on the Server?](https://intl.cloud.tencent.com/document/product/1007/36738).
>- To upload a SSL certificate to CVMs, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).

## Prerequisites
- A remote file copy tool such as WinSCP has been installed. You are recommended to download the latest version from the official website.
- A remote login tool such as PuTTY or Xshell has been installed. You are recommended to obtain the latest version from the official website.
- You have configured Apache service on the current server.
- The data required to install the SSL certificate includes:
<table>
<tr>
<td>Name</td>
<td>Description</td>
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

>?For a CVM instance purchased on the Tencent Cloud official website, log in to the [CVM Console](https://console.cloud.tencent.com/cvm) to obtain the server IP address, username, and password.

## Directions

### Certificate installation
1. Download the certificate package `www.domain.com` from the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl) and decompress it to a local directory.
After decompression, you can obtain the relevant certificate files, including the Apache folder and CSR file:
 - **Folder name**: Apache
 - **Folder content**:
    - `1_root_bundle.crt`: certificate file
    - `2_www.domain.com.crt`: certificate file
    - `3_www.domain.com.key`: private key file
  - **CSR file**: `www.domain.com.csr` file
>?The CSR file is uploaded by you or generated online by the system when you apply for the certificate and is provided to the CA. It is irrelevant to the installation.
2. Log in to the Apache server using WinSCP (a tool for copying files between a local computer and a remote computer).
3. Copy the obtained certificate files `1_root_bundle.crt` and `2_www.domain.com.crt` and the private key file `3_www.domain.com.key` from the local directory to the `/etc/httpd/ssl` directory of the Apache server.
>?If the `/etc/httpd/ssl` directory does not exist, run the `mkdir /etc/httpd/ssl` command to create one.
4. Remotely log in to the Apache server. For example, you can use [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502) for remote login.
>?For a newly installed Apache server, the files `conf.d`, `conf`, and `conf.modules.d` are in the `/etc/httpd` directory by default.
5. In the `httpd.conf` configuration file of the `/etc/httpd/conf` directory, find the `Include conf.modules.d/*.conf` configuration statement (for loading the SSL configuration directory) and check whether it is commented out. If it is commented out, delete the comment symbol (`#`) from the first line and save the configuration file.
6. In the `00-ssl.conf` configuration file of the `/etc/httpd/conf.modules.d` directory, find the `LoadModule ssl_module modules/mod_ssl.so` configuration statement (for loading the SSL module) and check whether it is commented out. If it is commented out, delete the comment symbol (`#`) from the first line and save the configuration file.
>!  Because directory structures vary with the OS version, search for the configuration statement based on the OS version you use.
> If the configuration statements `LoadModule ssl_module modules/mod_ssl.so` and `Include conf.modules.d/*.conf` are not found in the files mentioned above, check whether the mod_ssl.so module has been installed. If no, run the `yum install mod_ssl` command to install it.
7. Edit the 'ssl.conf' configuration file in the `/etc/httpd/conf.d` directory by modifying the following:
```
<VirtualHost 0.0.0.0:443>
		DocumentRoot "/var/www/html" 
		#Enter the certificate name
		ServerName www.domain.com 
		#Enable SSL
		SSLEngine on 
		#Enter the path where the certificate resides
		SSLCertificateFile /etc/httpd/ssl/2_www.domain.com.crt 
		#Enter the path where the private key resides
		SSLCertificateKeyFile /etc/httpd/ssl/3_www.domain.com.key 
		#Enter the path where the certificate chain resides
		SSLCertificateChainFile /etc/httpd/ssl/1_root_bundle.crt 
</VirtualHost>
```
8. Restart the Apache server and then it can be accessed using `https://www.domain.com`.

### Security configuration for automatic redirection from HTTP to HTTPS (optional)
If you do not know how to configure website access over HTTPS, you can configure the server to make it automatically redirect HTTP requests to HTTPS through the following steps:
1. Edit the httpd.conf configuration file in the `/etc/httpd/conf` directory.
>!
>- The directory structure varies with the Apache version. For more information, see [Apache Module mod_rewrite](http://httpd.apache.org/docs/2.4/mod/mod_rewrite.html).
>- httpd.conf is located in more than one directories. You can filter them by `/etc/httpd/*`.
2. Check whether `LoadModule rewrite_module modules/mod_rewrite.so` is in it.
 - If yes, remove the comment symbol (`#`) in front of `LoadModule rewrite_module modules/mod_rewrite.so` and proceed to [step 4](#step4).
 - Otherwise, proceed to [step 3](#step3).
[](id:step3)
3. Create a new \*.conf file such as 00-rewrite.conf in `/etc/httpd/conf.modules.d` and add the following to it:
 ```
 LoadModule rewrite_module modules/mod_rewrite.so
 ```
[](id:step4)
4. Add the following to the httpd.conf configuration file:
```
<Directory "/var/www/html"> 
# Add the following:
RewriteEngine on
RewriteCond %{SERVER_PORT} !^443$
RewriteRule ^(.*)?$ https://%{SERVER_NAME}%{REQUEST_URI} [L,R]
</Directory>
```
5. Restart the Apache server and then it can be accessed using `http://www.domain.com`.

>!If any problems occur during this process, please [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).


