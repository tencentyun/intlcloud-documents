## Scenarios
This document describes how to install an SSL certificate on an Nginx server.
>?
>- The certificate name `cloud.tencent.com` is used as an example in this document.
>- Nginx version `nginx / 1.16.0` is used as an example.
>- The current server OS is CentOS 7. The detailed steps may vary slightly depending on the operating system.
>- Before you install an SSL certificate, enable port 443 on the Nginx server so that HTTPS can be enabled after the certificate is installed. For more information, see [How do I enable port 443 for a server?](https://intl.cloud.tencent.com/document/product/1007/36738).
>- To upload a SSL certificate to CVMs, see [Copying Local Files to CVMs](https://intl.cloud.tencent.com/document/product/213/34821).

## Prerequisites
- A remote file copy tool such as WinSCP has been installed (we recommend downloading the latest version from their official website).
- A remote login tool such as PuTTY or Xshell has been installed (we recommend downloading the latest version from their official websites).
- The Nginx service has been installed and configured on the current server.
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

>!For a CVM instance purchased on the Tencent Cloud official website, you can log in to the [CVM Console](https://console.cloud.tencent.com/cvm) to get the server IP address, username, and password.


## Directions

### Certificate installation
1. Download the certificate package for the domain name `cloud.tencent.com` from the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl) and decompress it to a local directory.
After decompression, you can get the certificate files of the relevant types, including the `Nginx` folder and CSR file:
 - Folder name: `Nginx`
 - Folder content:
     - `1_cloud.tencent.com_bundle.crt`: certificate file
     - `2_cloud.tencent.com.key`: private key file
  - CSR file content: `cloud.tencent.com.csr` file
>!The CSR file is uploaded by you or generated online by the system when you apply for the certificate and is provided to the CA. It is not relevant to installation.
2. Log in to the Nginx server using WinSCP (a tool copying files between a local computer and a remote computer).
3. Copy the obtained `1_cloud.tencent.com_bundle.crt` certificate file and `2_cloud.tencent.com.key` private key file from the local directory to the `/usr/local/nginx/conf` directory of the Nginx server (this is the default Nginx installation directory and needs to be adjusted as needed).
4. Log in to the Nginx server remotely by using a login tool such as [PuTTY](https://intl.cloud.tencent.com/document/product/213/32502).
5. Edit the `conf/nginx.conf` configuration file in the Nginx root directory by modifying the following:
>?
>- You can edit the file by running `vim /usr/local/nginx/conf/nginx.conf`.
>- The configuration file may be written differently on different versions; for example, use `listen 443 ssl` instead of `listen 443` and `ssl on` for `nginx/1.15.0` or later.
>
```
server {
        # The SSL access port number is 443.
        listen 443 ssl; 
	    # Enter the domain name bound to the certificate
        server_name cloud.tencent.com; 
		# Certificate file name
        ssl_certificate 1_cloud.tencent.com_bundle.crt; 
		# Private key file name
        ssl_certificate_key 2_cloud.tencent.com.key; 
        ssl_session_timeout 5m;
	    # Configure according to the following protocol
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2; 
	    # Configure the cipher suite according to the OpenSSL standard
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE; 
        ssl_prefer_server_ciphers on;
        location / {
		   # Path to the website homepage. This example is for reference only. You should configure it with the actual path.
            root /var/www/cloud.tencent.com; 
            index  index.html index.htm;
        }
    }
```
6. Run the following command in the Nginx root directory to check whether there is a problem with the configuration file.
```
./sbin/nginx -t
```
 - If yes, reconfigure or fix the problem.
 - Otherwise, proceed to [step 7](#step7).
<span id="step7"></span>
7. Restart the Nginx server; it can be accessed through `https://cloud.tencent.com`.

### (Optional) Security configuration for automatic redirect from HTTP to HTTPS

If you do not know how to access a website over HTTPS, you can configure the server to make it automatically redirect HTTP requests to HTTPS in the following steps:
1. Select one of the following configuration methods based on your actual needs:
 - Add a JS script to the page.
 - Add redirect in the backend program.
 - Redirect through a web server.
 - Nginx supports rewrite. If you did not remove pcre during the compilation, you can add `return 301 https://$host$request_uri;` to the HTTP server and modify the following to redirect requests made to default port 80 to HTTPS:
>?
>- Uncommented configuration statements can be configured as shown below.
>- The configuration file may be written differently on different versions; for example, use `listen 443 ssl` instead of `listen 443` and `ssl on` for `nginx/1.15.0` or later.

```
server {
   listen 443 ssl;
	# Enter the domain name bound to the certificate
    server_name cloud.tencent.com; 
	# Path to the website homepage. This example is for reference only. You should configure it with the actual path.
    root /var/www/cloud.tencent.com; 
    index index.html index.htm;   
	# Certificate file name
	ssl_certificate  1_cloud.tencent.com_bundle.crt; 
	# Private key file name
    ssl_certificate_key 2_cloud.tencent.com.key; 
    ssl_session_timeout 5m;
    ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:ECDHE:ECDH:AES:HIGH:!NULL:!aNULL:!MD5:!ADH:!RC4;
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
    ssl_prefer_server_ciphers on;
    location / {
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
2. After modification is complete, restart the Nginx server; it can be accessed through `http://cloud.tencent.com`.

>!If you experience any issues with the steps outlined above, please [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

