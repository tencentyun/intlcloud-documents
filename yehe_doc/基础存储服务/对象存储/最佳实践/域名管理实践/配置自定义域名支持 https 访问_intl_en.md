

## Overview
You can access the objects under a bucket using your own endpoint (the custom endpoint, for example, `test.cos.com`). Detailed directions are as follows:
- [Supporting HTTPS for a custom endpoint with CDN acceleration enabled](#.E5.BC.80.E5.90.AF-cdn-.E5.8A.A0.E9.80.9F)
- [Supporting HTTPS for a custom endpoint with CDN acceleration disabled](#.E5.85.B3.E9.97.AD-cdn-.E5.8A.A0.E9.80.9F)


## Directions
### Enabling CDN Acceleration

#### Step 1. Bind a custom domain name
Bind the bucket to your own endpoint and enable CDN acceleration. For detailed directions, please see [Enabling Custom Accelerated Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).

#### Step 2. Perform HTTPS configuration
You can configure HTTPS access in the [CDN console](https://console.cloud.tencent.com/cdn). For detailed directions, please see [HTTPS Configuration Guide](https://intl.cloud.tencent.com/document/product/228/35213).


### Disabling CDN Acceleration

This section uses an example to describe how to support HTTPS access in COS by configuring custom endpoints through a reverse proxy (with CDN acceleration disabled). In this example, we use the custom endpoint `https://test.cos.com` to directly access the `testhttps-1250000000` bucket in the Guangzhou region with CDN acceleration disabled. The specific steps are as follows:

#### Step 1. Bind a custom domain name

HTTPS certificate hosting for custom origin server domain names of COS is supported in public cloud regions in the Chinese mainland and in Singapore. You can bind the certificate to the added custom origin server domain names via the console. For details, see [Method 1](#1). If no HTTPS certificate is available for your domain name, click [Apply for Free Certificate](https://console.cloud.tencent.com/ssl).

This feature is currently not supported in other regions. To use an HTTPS certificate, see [Method 2](#2).

<span id="1"></span>
- Method 1: Bind a custom origin server domain name via the COS console
Bind the `testhttps-1250000000` bucket to the `https://test.cos.com` domain and disable CDN acceleration. For detailed directions, please see [Enabling Custom Accelerated Domain Name](https://intl.cloud.tencent.com/document/product/436/31507).

<span id="2"></span>
- Method 2: Configure a reverse proxy for the domain name
Configure a reverse proxy for the `https://test.cos.com` endpoint on the server, as shown below (the Nginx configuration is for reference only):
```shell
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
        proxy_pass  http://testhttps-1250000000.cos.ap-guangzhou.myqcloud.com; // Configure the default download domain for the bucket. 
    }
}
```
`Server.crt;` and `server.key` are HTTPS certificates for your own (custom) domain. If no HTTPS certificate is available for your domain, you can apply for one at [Tencent Cloud SSL Certificate Service](https://intl.cloud.tencent.com/products/ssl).
If no certificate is available, the following configuration information can be deleted, but an alarm will occur during access. Click Continue to access the bucket:
```shell
ssl on;
ssl_certificate /usr/local/nginx/conf/server.crt;
ssl_certificate_key /usr/local/nginx/conf/server.key;
```

#### Step 2. Resolve the domain name at a server

Resolve your endpoint at your endpoint’s DNS provider.

#### Step 3. Perform advanced configurations

- **Opening the web page in a browser directly**
After configuring the custom endpoint to support HTTPS, you can download objects in the bucket using your domain. If your business requires directly accessing web pages and images in a browser, you can use the static website feature. For detailed directions, please see [Setting Up a Static Website](https://intl.cloud.tencent.com/document/product/436/14984).
After the configuration is completed, add the following code to the Nginx configuration file, restart Nginx, and refresh the browser cache.
```bash
proxy_set_header Host $http_host;
```
- **Configuring referer hotlink protection**
Public buckets might be hotlinked. You can use the hotlink protection feature to set a referer allowlist to prevent malicious hotlinking as follows:
 1. Log in to the [COS console](https://console.cloud.tencent.com/cos5), enable the hotlink protection feature, and configure an allowlist. For detailed directions, please see [Setting Hotlink Protection](https://intl.cloud.tencent.com/document/product/436/13319).
 2. Add the following code to the Nginx configuration file, restart Nginx, and refresh the browser cache.
```bash
proxy_set_header   Referer www.test.com;
```
 3. After the configuration, if you open the file directly, the error `errorcode: -46616` (error message: `not hit white refer`) will be reported. In this case, you can access the custom endpoint with a proxy to open the page.
```json
{
	errorcode: -46616,
	errormsg: "not hit white refer, retcode:-46616"
}
```


