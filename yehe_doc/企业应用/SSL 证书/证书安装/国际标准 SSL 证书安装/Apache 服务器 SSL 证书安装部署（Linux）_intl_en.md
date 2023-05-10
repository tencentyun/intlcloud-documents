## Overview

This document describes how to install an SSL certificate on an Apache server.

> **Notes**
> 
> - The certificate name `cloud.tencent.com` is used as an example.
> - The `Apache/2.4.6` version is used as an example. The default port is `80`. You can download it from the [Apache official website](https://httpd.apache.org/download.cgi). If you need to use another version, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).
> - The current server OS is CentOS 7. Detailed steps vary slightly by OS.
> - Before you install an SSL certificate, enable port `443` on the Apache server so that HTTPS can be enabled after the certificate is installed. For more information, see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738).
> - For detailed directions on how to upload SSL certificate files to a server, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).


## Prerequisites
- A remote file copy tool such as WinSCP has been installed. Please download the latest version from the official website.
We recommend that you use CVM's file upload feature for deployment to CVM.

- Install the remote login tool such as PuTTY or Xshell. The latest official version is recommended.

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


   > **Notes**
   > 
   > For a CVM instance purchased on the Tencent Cloud official website, log in to the [CVM console](https://console.cloud.tencent.com/cvm) to get the server IP address, username, and password.
   > 


## Directions

### Installing the certificate
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and click **Download** for the certificate you need to install.

2. In the pop-up window, select **Apache** for the server type, click **Download**, and decompress the `cloud.tencent.com` certificate file package to the local directory.
 After decompression, you can get the certificate file of the corresponding type, which includes the `cloud.tencent.com_apache` folder.

  - **Folder**: `cloud.tencent.com_apache`

  - **Files in the folder**:

    - `root_bundle.crt`: certificate file

    - `cloud.tencent.com.crt`: certificate file

    - `cloud.tencent.com.key`: Private key file

  - **CSR file**: 	`cloud.tencent.com.csr` file
    

      > **Notes**
      > 
      > You can upload the CSR file when applying for a certificate or have it generated online by the system. It is provided to the CA and irrelevant to the installation.
      > 

3. Log in to the Apache server using WinSCP (a tool copying files between a local computer and a remote computer).
   

   > **Notes**
   > 
   >   - For detailed directions, see [Uploading files via WinSCP to a Linux CVM from Windows](https://intl.cloud.tencent.com/document/product/213/2131).
   >   - We recommend that you use CVM's file upload feature for deployment to CVM.

4. Copy the obtained certificate files `root_bundle.crt` and `cloud.tencent.com.crt` and the private key file `cloud.tencent.com.key` from the local directory to the `/etc/httpd/ssl` directory of the Apache server.
   

   > **Notes**
   > 
   >  If the `/etc/httpd/ssl` directory does not exist, run the `mkdir /etc/httpd/ssl` command to create it.
   > 

5. Log in to the Apache server remotely by using a login tool such as [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502).
   

   > **Notes**
   > 

   > For a newly installed Apache server, the `conf.d`, `conf`, and `conf.modules.d` directories are under the `/etc/httpd` directory by default.
   > 

6. In the `httpd.conf` configuration file under `/etc/httpd/conf`, find the `Include conf.modules.d/*.conf` configuration statement (for loading the SSL configuration directory) and check whether it is commented out. If so, remove the comment symbol (`#`) from the first line and save the configuration file.

7. In the `00-ssl.conf` configuration file under `/etc/httpd/conf.modules.d`, find the `LoadModule ssl_module modules/mod_ssl.so` configuration statement (for loading the SSL module) and check whether it is commented out. If so, remove the comment symbol (`#`) from the first line and save the configuration file.
   

   > **Notes**
   >  The directory structure varies by OS version. Find files in accordance with the actual OS version.
If `LoadModule ssl_module modules/mod_ssl.so` and `Include conf.modules.d/*.conf` configuration statements cannot be found in the configuration files above, check whether the `mod_ssl.so` module has been installed, and if not, run the `yum install mod_ssl` command to install it.
   > 

8. Edit the `ssl.conf` configuration file in the `/etc/httpd/conf.d` directory by modifying the following:

   ``` xml
   <VirtualHost 0.0.0.0:443>
        DocumentRoot "/var/www/html" 
        # Enter the certificate name
        ServerName cloud.tencent.com 
        # Enable SSL
        SSLEngine on 
        # Path of the certificate file
        SSLCertificateFile /etc/httpd/ssl/cloud.tencent.com.crt 
        # Path of the private key file
        SSLCertificateKeyFile /etc/httpd/ssl/cloud.tencent.com.key 
        # Path of the certificate chain file
        SSLCertificateChainFile /etc/httpd/ssl/root_bundle.crt 
   </VirtualHost>
   ```
9. Restart the Apache server and then you can access it through `https://cloud.tencent.com`.

  - If the security lock icon is displayed in the browser, the certificate has been installed successfully.

  - In case of a website access exception, troubleshoot the issue by referring to the following FAQs:

    - [Website Inaccessible After an SSL Certificate is Deployed](https://intl.cloud.tencent.com/document/product/1007/39821)

    - ["Your Connection is Not Secure" is Displayed After the SSL Certificate is Installed](https://intl.cloud.tencent.com/document/product/1007/40674)

    - [Why Does the Website Prompt "Connection Is Untrusted"?](https://intl.cloud.tencent.com/document/product/1007/30184)


    - [404 Error After the SSL Certificate is Deployed on IIS](https://intl.cloud.tencent.com/document/product/1007/39820)


### (Optional) Security configuration for automatic redirect from HTTP to HTTPS

To redirect HTTP requests to HTTPS, complete the following settings:
1. Edit the httpd.conf configuration file in the `/etc/httpd/conf` directory.
   

   > **Notes**
   > 
>   - The directory structure varies by Apache version. For more information, see [Apache Module mod_rewrite](http://httpd.apache.org/docs/2.4/mod/mod_rewrite.html).
>   - The `httpd.conf` configuration file is located in more than one directory. You can filter them by `/etc/httpd/*`.

2. Check whether `LoadModule rewrite_module modules/mod_rewrite.so` is in it.

  - If so, remove the comment symbol (`#`) in front of `LoadModule rewrite_module modules/mod_rewrite.so` and proceed to [step 4](https://write.woa.com/#step4).

  - If not, proceed to [step 3](https://write.woa.com/#step3).

3. Create a `*.conf` file such as `00-rewrite.conf` in `/etc/httpd/conf.modules.d` and add the following content to it:

   ``` bash
   LoadModule rewrite_module modules/mod_rewrite.so
   ```
4. Add the following to the `httpd.conf` configuration file:

   ``` bash
   <Directory "/var/www/html"> 
   # Add the following:
   RewriteEngine on
   RewriteCond %{SERVER_PORT} !^443$
   RewriteRule ^(.*)?$ https://%{SERVER_NAME}%{REQUEST_URI} [L,R]
   </Directory>
   ```
5. Restart the Apache server and then you can access it through `http://cloud.tencent.com`.
   

   > **Notes**
   > If anything goes wrong during this process, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).
