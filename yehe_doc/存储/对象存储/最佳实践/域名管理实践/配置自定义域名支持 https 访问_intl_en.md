## Overview
You can access the objects under a bucket using your own endpoint (the custom endpoint, for example, `test.cos.com`). Detailed directions are as follows:
- [Supporting HTTPS for a custom endpoint with CDN acceleration enabled](#.E5.BC.80.E5.90.AF-cdn-.E5.8A.A0.E9.80.9F)
- [Supporting HTTPS for a custom endpoint with CDN acceleration disabled](#.E5.85.B3.E9.97.AD-cdn-.E5.8A.A0.E9.80.9F)



## Enabling CDN Acceleration

#### Directions

#### 1. Bind a custom endpoint
Bind the bucket to your own endpoint and enable CDN acceleration. For detailed directions, please see [Enabling Custom Accelerated Domain Name](https://intl.cloud.tencent.com/document/product/436/31506).
#### 2. Configure HTTPS access
You can configure HTTPS access in the [CDN console](https://console.cloud.tencent.com/cdn). For detailed directions, please see [HTTPS Configuration Guide](https://intl.cloud.tencent.com/document/product/228/35213).


## Disabling CDN Acceleration

This section uses an example to describe how to support HTTPS access in COS by configuring custom endpoints through a reverse proxy (with CDN acceleration disabled). In this example, we use the custom endpoint `https://test.cos.com` to directly access the `testhttps-1250000000` bucket in the Guangzhou region with CDN acceleration disabled. The specific steps are as follows:

#### Directions

#### 1. Bind a custom endpoint
Bind the `testhttps` bucket to the `https://test.cos.com` endpoint and disable CDN acceleration. For detailed directions, please see [Enabling Custom Accelerated Domain Name](https://intl.cloud.tencent.com/document/product/436/31507).

#### 2. Configure a reverse proxy for the endpoint
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
`Server.crt;` and `server.key` are HTTPS certificates for your own (custom) endpoint. If no HTTPS certificate is in place for your endpoint, you can apply for one at [Tencent Cloud SSL Certificate Service](https://intl.cloud.tencent.com/product/ssl).
If no certificate is available, the following configuration information can be deleted, but an alarm will occur during access. Click Continue to access the bucket:
```shell
ssl on;
ssl_certificate /usr/local/nginx/conf/server.crt;
ssl_certificate_key /usr/local/nginx/conf/server.key;
```

#### 3. Resolve the endpoint to the server

Resolve your endpoint at your DNS hosting provider. If you are using Tencent Cloud’s DNS service, please go to the [DNSPod console](https://console.cloud.tencent.com/cns) to map `test.cos.com` to the server’s IP in Step 2. For more information, please see **Adding a DNS Record**.

#### 4. Advanced settings

- **Opening the web page in a browser directly**

After configuring the custom endpoint to support HTTPS, you can download objects in the bucket using your endpoint. If your business requires directly accessing web pages and images in a browser, you can use the static website feature. For detailed directions, please see [Setting up a Static Website](https://intl.cloud.tencent.com/document/product/436/14984).
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
