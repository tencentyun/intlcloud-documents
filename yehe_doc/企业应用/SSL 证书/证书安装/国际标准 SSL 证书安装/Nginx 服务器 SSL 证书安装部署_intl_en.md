The following video shows you how to install an SSL certificate on an Nginx server:
<div class="doc-video-mod"><iframe src="https://cloud.tencent.com/edu/learning/quick-play/3386-59866?source=gw.doc.media&withPoster=1&notip=1"></iframe></div>

## Overview
This document describes how to install an SSL certificate on an Nginx server.
>?
>- The certificate name `cloud.tencent.com` is used as an example.
>- The Nginx version `nginx/1.18.0` is used as an example.
>- The current server OS is CentOS 7. Detailed steps vary slightly with the OS.
>- Before you install an SSL certificate, enable port 443 on the Nginx server so that HTTPS can be enabled after the certificate is installed. For more information, see [How Do I Enable Port 443 for a VM?](https://intl.cloud.tencent.com/document/product/1007/36738).
>- For more information about how to upload SSL certificate files to a server, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).
>
## Prerequisites
- A remote file copy tool such as WinSCP has been installed. Please download the latest version from the official website.
- A remote login tool such as PuTTY or Xshell has been installed. Please download the latest version from the official website.
- The Nginx service has been installed and configured on the current server.
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

### Certificate Installation
1. Log in to the [SSL Certificate Service console](https://console.cloud.tencent.com/ssl), and click **Download** for the certificate you need to install.
2. In the pop-up window, select **Nginx** for the server type, click **Download**, and decompress the `cloud.tencent.com` certificate file package to the local directory.
After decompression, you can get the certificate file of the corresponding type, which includes the `cloud.tencent.com_nginx` folder.
 - **Folder**: `cloud.tencent.com_nginx`
 - **Files in the folder**:
     - `cloud.tencent.com_bundle.crt`: certificate file
     - `cloud.tencent.com_bundle.pem`: certificate file
     - `cloud.tencent.com.key`: private key file
     - `cloud.tencent.com.csr`: CSR file
>?The CSR file is uploaded by you or generated online by the system and is provided to the certificate authority (CA) when you apply for the certificate. It is not relevant to installation.
3. Log in to the Nginx server using WinSCP (a tool copying files between a local computer and a remote computer).
4. Copy the `cloud.tencent.com_bundle.crt` and `cloud.tencent.com.key` files from the local directory to the `/usr/local/nginx/conf` directory of the Nginx server (this is the default Nginx installation directory and needs to be adjusted as needed).
5. Log in to the Nginx server remotely by using a login tool such as [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502).
6. Edit the `conf/nginx.conf` configuration file in the Nginx root directory by modifying the following:
>?
>- With this operation, you can edit the file by running `vim /usr/local/nginx/conf/nginx.conf`.
>- You may need to configure the configuration file differently based on the Nginx version. For example, use `listen 443 ssl` instead of `listen 443` and `ssl on` for version `nginx/1.15.0` or later.
>
```
server {
        # The SSL access port number is 443
        listen 443 ssl; 
	    #Enter the domain name bound to the certificate
        server_name cloud.tencent.com; 
		# Certificate filename
        ssl_certificate cloud.tencent.com_bundle.crt; 
		# Private key filename
        ssl_certificate_key cloud.tencent.com.key; 
        ssl_session_timeout 5m;
	    # Configure according to the following protocol
        ssl_protocols TLSv1.2 TLSv1.3; 
	    # Configure the cipher suite according to the OpenSSL standard
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE; 
        ssl_prefer_server_ciphers on;
        location / {
		   # Path to the website homepage. This example is for reference only. You should configure it with the actual path
		   #For example, fill in /etc/www if your website running directory is /etc/www.
            root html; 
            index  index.html index.htm;
        }
    }
```
7. Run the following command in the Nginx root directory to check whether there is a problem with the configuration file.
```
./sbin/nginx -t
```
 - If yes, reconfigure or fix the problem as prompted.
 - If no, proceed to [step 7](#step7).
[](id:step7)
8. Restart the Nginx server and then you can access the `cloud.tencent.com` website over the HTTPS protocol.

### (Optional) security configuration for automatic redirect from HTTP to HTTPS
You can redirect HTTP requests to HTTPS by configuring the following settings:
1. Select one of the following configuration methods based on your actual needs:
 - Add a JavaScript script to the page.
 - Add redirect in the backend program.
 - Redirect through a web server.
 - Nginx supports rewrite. If you did not remove pcre during the compilation, you can add `return 301 https://$host$request_uri;` to the HTTP server to redirect requests made to default port 80 to HTTPS.
>?
>- Uncommented configuration statements can be configured as shown below.
>- You may need to configure the configuration file differently based on the Nginx version. For example, use `listen 443 ssl` instead of `listen 443` and `ssl on` for version `nginx/1.15.0` or later.
>
```
server {
   listen 443 ssl;
	#Enter the domain name bound to the certificate
    server_name cloud.tencent.com; 
	# Certificate filename
	ssl_certificate  cloud.tencent.com_bundle.crt; 
	# Private key filename
    ssl_certificate_key cloud.tencent.com.key; 
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_prefer_server_ciphers on;
    location / {
			# Path to the website homepage. This example is for reference only. You should configure it with the actual path 
			#For example, fill in /etc/www if your website running directory is /etc/www.
		root html;
        index  index.html index.htm;
    }
}
server {
    listen 80;
	#Enter the domain name bound to the certificate
    server_name cloud.tencent.com; 
	# Redirect requests made to an HTTP domain name to HTTPS
    return 301 https://$host$request_uri; 
}
``` 
2. After modification is complete, restart the Nginx server and then you can access the `cloud.tencent.com` website over the HTTPS protocol.

>!If you experience any issues with the above steps, please [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

