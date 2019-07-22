## Scenario
This document guides you through how to install an SSL certificate on an Apache server.
>
>- This document takes the domain name `www.domain.com` as an example.
>- The current server OS is CentOS 7. The detailed steps vary slightly by OS version.

## Prerequisites
- The certificate package for the domain name `www.domain.com` in the SSL Certificate Service Console has been downloaded and decompressed to a local directory.
After decompression, you can get the Apache folder and CSR file:
 - **Folder name**: Apache
 - **Folder content**:
    - `1_root_bundle.crt`   Certificate file
    - `2_www.domain.com.crt`   Certificate file
    - `3_www.domain.com.key`   Private key file
  - **CSR file content**: 	`www.domain.com.csr` file
- The remote copy tool WinSCP has been installed (you are recommended to get the latest version from its official website).
- The remote login tool PuTTY or Xshell has been installed (you are recommended to get the latest version from their official websites).
- The Apache server has been installed and configured on the current server.

>The CSR file is uploaded by you or generated online by the system when you apply for the certificate and is provided to the CA, which can be ignored during installation.

## Data
The data to be prepared before installing the SSL certificate includes:

| Name | Description | Sample Value |
|---------|---------|---------|
| Server IP address | IP address of the server, which is used to connect the PC to the server. | 192.168.22.10 |
| Username | The username used to log in to the server. | root |
| Password | The password used to log in to the server. | abc |

## Directions

### Certificate Installation
1. Log in to the Apache server using WinSCP (a tool copying files between a local computer and a remote computer).
2. Copy the obtained certificate files `1_root_bundle.crt` and `2_www.domain.com.crt` and the private key file `3_www.domain.com.key` from the local directory to the `/etc/httpd/ssl` directory of the Apache server.
> If the `/etc/httpd/ssl` directory does not exist, run `mkdir /etc/httpd/ssl` in the command line to create it.
3. Close WinSCP.
4. Log in to the Apache server using a remote login tool such as PuTTY.
5. Find the `LoadModule ssl_module modules/mod_ssl.so` (for loading the SSL module) and `Include conf.modules.d/*.conf` (for loading the SSL configuration directory) configuration statements and check whether they have been commented.
 > The directory structure varies by OS version. Please search according to the actual OS version. The `LoadModule ssl_module modules/mod_ssl.so` and `Include conf.modules.d/*.conf` configuration statements may be configured in the following configuration files:
> - The 00-ssl.conf configuration file in the `conf.modules.d` directory.
> - The httpd.conf configuration file.
> - The http-ssl.conf configuration file.
> 
> If they cannot be found in the files above, check whether the mod_ssl.so module has been installed. If no, run the `yum install mod_ssl` command to install it.
> 
 - If they are commented, remove the comment symbol (`#`) from the first line, save the configuration file, and proceed to [step 6](#step6).
 - Otherwise, directly proceed to [step 6](#step6).
<span id="step6"></span>
6. Edit the ssl.conf configuration file in the `/etc/httpd/conf.d` directory by modifying the following:
>For a newly installed Apache server, the `conf.d` directory is in the `/etc/httpd` directory by default.
>
```
<VirtualHost 0.0.0.0:443>
		DocumentRoot "/var/www/html"
		ServerName www.domain.com
		SSLEngine on
		SSLCertificateFile /etc/httpd/ssl/2_www.domain.com_cert.crt
		SSLCertificateKeyFile /etc/httpd/ssl/3_www.domain.com.key
		SSLCertificateChainFile /etc/httpd/ssl/1_root_bundle.crt
</VirtualHost>
```
The main parameters of the configuration file are described as below:
 - **SSLEngine on**: Enable SSL
 - **SSLCertificateFile**: Path of the certificate file
 - **SSLCertificateKeyFile**: Path of the private key file
 - **SSLCertificateChainFile**: Path of the certificate chain file
7. Restart the Apache server and it can be accessed using `https://www.domain.com`.

### Security Configuration for Automatic Redirect from HTTP to HTTPS (Optional)
If you don't know how to access a website over HTTPS, you can configure the server to make it automatically redirect HTTP requests to HTTPS in the following steps:
1. Edit the httpd.conf configuration file in the `/etc/httpd/conf` directory.
>
>- The directory structure varies by Apache version. For more information, see [Apache Module mod_rewrite](http://httpd.apache.org/docs/2.4/mod/mod_rewrite.html).
>- The directory where httpd.conf is located is not unique. You can filter them by `/etc/httpd/*`.
2. Check whether `LoadModule rewrite_module modules/mod_rewrite.so` is in it.
 - If yes, remove the comment symbol (`#`) in front of `LoadModule rewrite_module modules/mod_rewrite.so` and proceed to [step 4](#step4).
 - Otherwise, proceed to [step 3](#step3).
 <span id="step3"></span>
3. Create a new \*.conf file such as 00-rewrite.conf in `/etc/httpd/conf.modules.d` and add the following to it:
 ```
 LoadModule rewrite_module modules/mod_rewrite.so
 ```
<span id="step4"></span>
4. Add the following to the httpd.conf configuration file:
```
<Directory "/var/www/html"> 
# Add the following:
RewriteEngine on
RewriteCond %{SERVER_PORT} !^443$
RewriteRule ^(.*)?$ https://%{SERVER_NAME}%{REQUEST_URI} [L,R]
</Directory>
```
4. Restart the Apache server and it can be accessed using `http://www.domain.com`.

> If anything goes wrong during this procedure, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

