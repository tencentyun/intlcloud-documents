## Scenario
This document guides you through how to install an SSL certificate on an Nginx server.
>
>- This document takes the domain name `www.domain.com` as an example.
>- The current server OS is CentOS 7. The detailed steps vary slightly by OS version.
>
## Prerequisites
- The certificate package for the domain name `www.domain.com` in the SSL Certificate Service Console has been downloaded and decompressed to a local directory.
After decompression, you can get the Nginx folder and CSR file:
 - **Folder name**: Nginx
 - **Folder content**:
    - `1_www.domain.com_bundle.crt`   Certificate file
    - `2_www.domain.com.key`   Private key file
  - **CSR file content**: 	`www.domain.com.csr` file
- The remote copy tool WinSCP has been installed (you are recommended to get the latest version from its official website).
- The remote login tool PuTTY or Xshell has been installed (you are recommended to get the latest version from their official websites).
- The Nginx server has been installed and configured on the current server.

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
1. Log in to the Nginx server using WinSCP (a tool copying files between a local computer and a remote computer).
2. Copy the obtained `1_www.domain.com_bundle.crt` certificate file and `2_www.domain.com.key` private key file from the local directory to the `/usr/local/nginx/conf` directory of the Nginx server.
> If the `/usr/local/nginx/conf` directory does not exist, run `mkdir /usr/local/nginx/conf` in the command line to create it.
3. Close WinSCP.
4. Log in to the Nginx server using a remote login tool such as PuTTY.
5. Edit the conf/nginx.conf configuration file in the Nginx root directory by modifying the following:
```
server {
        listen 443;
        server_name www.domain.com; # Enter the domain name bound to the certificate
        ssl on;
        ssl_certificate 1_www.domain.com_bundle.crt;# Certificate file name
        ssl_certificate_key 2_www.domain.com.key;# Private key file name
        ssl_session_timeout 5m;
        ssl_protocols TLSv1 TLSv1.1 TLSv1.2; # Configure according to this protocol
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE;# Configure according to this suite
        ssl_prefer_server_ciphers on;
        location / {
            root /var/www/www.domain.com; # Path of the website homepage. This example is for reference only. You should configure it with the actual path.
            index  index.html index.htm;
        }
    }
```
The main parameters of the configuration file are described as below:
 - **listen 443**: The SSL access port number is 443
 - **ssl on**: Enable SSL
 - **ssl_certificate**: Certificate file
 - **ssl_certificate_key**: Private key file
 - **ssl_protocols**: The protocol used
 - **ssl_ciphers**: Configure the cipher suite according to the OpenSSL standard
6. Run the following command to check whether there is a problem with the configuration file in the Nginx root directory.
```
./sbin/nginx -t
```
 - If yes, reconfigure or fix the problem as prompted.
 - Otherwise, proceed to [step 7](#step7).
<span id="step6"></span>
7. Restart the Nginx server and it can be accessed using `https://www.domain.com`.

### Security Configuration for Automatic Redirect from HTTP to HTTPS (Optional)

If you don't know how to access a website over HTTPS, you can configure the server to make it automatically redirect HTTP requests to HTTPS in the following steps:
1. Select one of the following configuration methods based on your actual needs:
 - Add a JS script to the page.
 - Add redirect in the backend program.
 - Redirect through a web server.
 - Nginx supports the rewrite feature. If you did not remove pcre during the compilation, you can add `rewrite ^(.*) https://$host$1 permanent;` to the HTTP server and modify the following to redirect requests to the default port 80 to HTTPS:
```
server {
    listen 443;
    server_name www.domain.com; # Enter the domain name bound to the certificate
    ssl on;
    root /var/www/www.domain.com; # Path of the website homepage. This example is for reference only. You should configure it with the actual path.
    index index.html index.htm;   # The index.html file in the folder configured above
    ssl_certificate  1_www.domain.com_bundle.crt; # Certificate file name
    ssl_certificate_key 2_www.domain.com.key; # Private key file name
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
    server_name www.domain.com; # Enter the domain name bound to the certificate
    rewrite ^(.*)$ https://$host$1 permanent; # Redirect HTTP domain name requests to HTTPS
}
```
2. After completing the modification, restart the Nginx server and it can be accessed using `http://www.domain.com`.

> If anything goes wrong during this procedure, [contact us](https://intl.cloud.tencent.com/document/product/1007/30951).

