The following video shows you how to install an SSL certificate on an Nginx server:



## Overview

This document describes how to install an SSL certificate on an Nginx server.

>?
>
> - The certificate name `cloud.tencent.com` is used as an example.
> - The `nginx/1.18.0` version is used as an example.
> - The current server OS is CentOS 7. Detailed steps vary slightly by OS.
> - Before you install an SSL certificate, enable the default HTTPS port `443` on the Nginx server so that HTTPS can be enabled after the certificate is installed. For more information, see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738).
> - For detailed directions on how to upload SSL certificate files to a server, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).


## Prerequisites
- Install the remote file copy tool such as WinSCP. The latest official version is recommended.
We recommend that you use CVM's file upload feature for deployment to CVM.

- Install the remote login tool such as PuTTY or Xshell. The latest official version is recommended.

- Install the Nginx service containing `http_ssl_module` module in the current server.

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

### Installing the certificate
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and click **Download** for the certificate you need to install.

2. In the pop-up window, select **Nginx** for the server type, click **Download**, and decompress the `cloud.tencent.com` certificate file package to the local directory.
After decompression, you can get the certificate file of the corresponding type, which includes the `cloud.tencent.com_nginx` folder.

  - **Folder**: `cloud.tencent.com_nginx`

  - **Files in the folder**:

    - `cloud.tencent.com_bundle.crt`: Certificate file

    - `cloud.tencent.com_bundle.pem`: Certificate file (optional)

    - `cloud.tencent.com.key`: Private key file

    - `cloud.tencent.com.csr`: CSR file
      

         >?
         >
         > You can upload the CSR file when applying for a certificate or have it generated online by the system. It is provided to the CA and irrelevant to the installation.
         >

3. Log in to the Nginx server using WinSCP (a tool copying files between a local computer and a remote computer).
   

>?
>   - For detailed directions, see [Uploading files via WinSCP to a Linux CVM from Windows](https://intl.cloud.tencent.com/document/product/213/2131).
>   - We recommend that you use CVM's file upload feature for deployment to CVM.

4. Copy the `cloud.tencent.com_bundle.crt` certificate file and `cloud.tencent.com.key` private key file from the local directory to the `/etc/nginx` directory (this is the default Nginx installation directory and needs to be adjusted as needed) of the Nginx server.

5. Log in to the Nginx server remotely with such a login tool as [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502).

6. Edit the `nginx.conf` configuration file in the Nginx root directory as follows:
   

>?
>   - If you cannot find the following content, manually add it. Run the `nginx -t` command to find the path of the Nginx configuration file.
> As shown below: ![tapd_10132091_base64_1665978617_57.png](https://qcloudimg.tencent-cloud.cn/image/document/b772c59a0bdd1d7bfc97a2320cb95df7.png)
>   - This operation can edit the file by running `vim /etc/nginx/nginx.conf`.
>   - The configuration file may be written differently on different versions; for example, use `listen 443 ssl` instead of `listen 443` and `ssl on` on `nginx/1.15.0` or later.



   ``` bash
   server {
        # The default SSL access port is 443
        listen 443 ssl; 
        # Enter the domain name bound to the certificate
        server_name cloud.tencent.com; 
        # Enter the relative or absolute path of the certificate file
        ssl_certificate cloud.tencent.com_bundle.crt; 
        # Enter the relative or absolute path of the private key file
        ssl_certificate_key cloud.tencent.com.key; 
        ssl_session_timeout 5m;
        # Configure the following protocols
        ssl_protocols TLSv1.2 TLSv1.3; 
        # Configure the cipher suite according to the OpenSSL standard
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE; 
        ssl_prefer_server_ciphers on;
        location / {
            # Path to the website homepage. This example is for reference only. You need to set it to the actual path.
            # For example, if your website homepage is under the "/etc/www" path of the Nginx server, change the "html" behind "root" to "/etc/www".
            root html; 
            index  index.html index.htm;
        }
    }
   ```
   
   
7. Run the following command to check whether there is a problem with the configuration file.

   ``` bash
   nginx -t
   ```
  - If yes, reconfigure or fix the problem as prompted.

  - If not, proceed to [step 8](https://write.woa.com/#step8).

8. Run the following command to reload the Nginx server.

   ``` bash
   nginx -s reload
   ```
9. If the server is reloaded successfully, you can access it through `https://cloud.tencent.com`.


### (Optional) Security configuration for automatic redirect from HTTP to HTTPS

To redirect HTTP requests to HTTPS, complete the following settings:
1. Select one of the following configuration methods based on your actual needs:

  - Add a JavaScript script to the page.

  - Add redirect in the backend program.

  - Redirect through a web server.

  - Nginx supports rewrite. If you did not remove PCRE during the compilation, you can add `return 301 https://$host$request_uri;` to the HTTP server to redirect requests made to the default HTTP port 80 to HTTPS.
    

>?
> - Uncommented configuration statements can be configured as follows.
> - The configuration file may be written differently on different versions; for example, use `listen 443 ssl` instead of `listen 443` and `ssl on` on `nginx/1.15.0` or later.
  


      ``` bash
      server {
       # The default SSL access port is 443
       listen 443 ssl;
       # Enter the domain name bound to the certificate
       server_name cloud.tencent.com; 
       # Enter the relative or absolute path of the certificate file
       ssl_certificate  cloud.tencent.com_bundle.crt; 
       # Enter the relative or absolute path of the private key file
       ssl_certificate_key cloud.tencent.com.key; 
       ssl_session_timeout 5m;
       # Configure the cipher suite according to the OpenSSL standard
       ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
       # Configure the following protocols
       ssl_protocols TLSv1.2 TLSv1.3;
       ssl_prefer_server_ciphers on;
       location / {
         # Path to the website homepage. This example is for reference only. You need to set it to the actual path. 
         # For example, if your website homepage is under the "/etc/www" path of the Nginx server, change the "html" behind "root" to "/etc/www".
         root html;
         index index.html index.htm;
       }
      }
      server {
       listen 80;
       # Enter the domain name bound to the certificate
       server_name cloud.tencent.com; 
       # Redirect requests made to an HTTP domain name to HTTPS
       return 301 https://$host$request_uri; 
      }
      ```
      
      
2. Run the following command to check whether there is a problem with the configuration file.

   ``` bash
   nginx -t
   ```
  - If yes, reconfigure or fix the problem as prompted.

  - If not, proceed to [step 3](https://write.woa.com/#step3).

3. Run the following command to reload the Nginx server.

   ``` bash
   nginx -s reload
   ```
   
4. If the server is reloaded successfully, you can access it through `https://cloud.tencent.com`.

- If the security lock icon is displayed in the browser, the certificate has been installed successfully.

- In case of a website access exception, troubleshoot the issue by referring to the following FAQs:

    - [Website Inaccessible After an SSL Certificate is Deployed](https://intl.cloud.tencent.com/document/product/1007/39821)

    - ["Your Connection is Not Secure" is Displayed After the SSL Certificate is Installed](https://intl.cloud.tencent.com/document/product/1007/40674)

    - [Why Does the Website Prompt "Connection Is Untrusted"?](https://intl.cloud.tencent.com/document/product/1007/30184)

    - [404 Error After the SSL Certificate is Deployed on IIS](https://intl.cloud.tencent.com/document/product/1007/39820)
      

>!
> If anything goes wrong during this process, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).
