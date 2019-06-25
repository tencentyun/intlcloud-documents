You can access the objects under a bucket using your own domain name (the custom domain name, such as `test.cos.com`). See the following procedures:
- [Configure custom domain names to support HTTPS access when CDN acceleration is enabled](https://intl.cloud.tencent.com/document/product/436/11142)
- [Configure custom domain names to support HTTPS access when CDN acceleration is disabled](https://intl.cloud.tencent.com/document/product/436/11142)

<span id="Enable CDN Acceleration"></span>
## Enabling CDN Acceleration
### 1. Bind custom domain name
Bind a bucket to your own domain name and enable CDN acceleration. For more information, see [Domain Name Management - Custom Domain Names](https://intl.cloud.tencent.com/document/product/436/18424).
### 2. Configure HTTPS access
Configure HTTPS in the CDN Console. For more information, see [HTTPS Configuration](https://intl.cloud.tencent.com/document/product/228/6295).
<span id="Disable CDN Acceleration"></span>

## Disabling CDN Acceleration
This section uses an example to describe the steps of supporting HTTPS access in COS by configuring custom domain names through reverse proxy (CDN acceleration is disabled). In this example, we use the custom domain name `https://test.cos.com` to directly access the bucket testhttps-12345678 in South China without enabling CDN acceleration. Specific steps are as follows:

### 1. Bind custom domain name
Bind the bucket testhttps to the domain name `https://test.cos.com` and disable CDN acceleration. For more information, see [Domain Name Management - Custom Domain Names](https://intl.cloud.tencent.com/document/product/436/18424).
### 2. Configure the reverse proxy for a domain name
Configure a reverse proxy for the domain name `https://test.cos.com` on the server, as shown below (the Nginx configuration is for reference only):
```
server {
    listen        443;
    server_name  test.cos.com ;

    ssl on;
    ssl_certificate /usr/local/nginx/conf/server.crt;
    ssl_certificate_key /usr/local/nginx/conf/server.key;

    error_log logs/test.cos.com.error_log;
    access_log logs/test.cos.com.access_log;
    location / {
        root /data/www/;
        proxy_pass  http://testhttps-12345678.cos.ap-guangzhou.myqcloud.com; //Configure the default download domain name for a bucket 
    }
        
}
```
`Server.crt;` and `server.key` are HTTPS certificates for your own (custom) domain names. If no HTTPS certificate is in place for your domain names, you can apply for one on the [Tencent Cloud SSL Certificate](https://intl.cloud.tencent.com/product/ssl) page.
If no certificate is available, the following configuration information can be deleted, but an alarm will occur during access. Click Continue to access the bucket:

```
    ssl on;
    ssl_certificate /usr/local/nginx/conf/server.crt;
    ssl_certificate_key /usr/local/nginx/conf/server.key;
```

### 3. Resolve domain names to the server
Resolve your domain names at your DNS resolution provider. If you are using Tencent Cloud DNS, go to the [Cloud DNS Console](https://console.cloud.tencent.com/cns/domains) to resolve the domain name `test.cos.com` to the IP of the server in step 2. 
### Other configurations
#### Open the web page directly in a browser
- After configuring the custom domain name to support HTTPS access, you can download objects in the bucket using your domain name. According to your business needs, you can directly access web pages and images in a browser through the static website feature. For more information, see [Static Website Settings](https://intl.cloud.tencent.com/document/product/436/6249).

- After the configuration is completed, add the following information to the Nginx configuration, restart Nginx, and refresh the browser cache.

```
proxy_set_header Host $http_host;
```
#### Configure the refer hotlink protection
There is a risk of hotlinking for public buckets. You can enable the Referer whitelist by setting hotlink protection to prevent malicious hotlinking. Follow the steps below:
1. Enable the hotlink protection feature in the [COS Console](https://console.cloud.tencent.com/cos4/index) and select Whitelist. For more information, see [Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/6250).
2. Add the following information to the Nginx configuration, restart Nginx, and refresh the browser cache.
```
proxy_set_header   Referer www.test.com;
```
3. After the configuration, an error (error code: `errorcode: -46616`; error message: the refer whitelist is not hit) may occur if you directly open the file. However, by using a custom domain name configured with a proxy, the web page can be opened.
![](//mc.qcloudimg.com/static/img/005099e6a30398c600bb945b6b1c34e7/image.png)

