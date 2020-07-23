### What should I do if a 423 error is reported in CDN?
The 423 status code is a Tencent Cloud CDN custom status code. CDN will report a 423 error when it detects a loopback request. We recommend you check the following:
1. Check the origin server configured in the [CDN Console](https://console.cloud.tencent.com/cdn). If your origin server is also a Tencent Cloud CDN acceleration domain name, it may cause loopback requests.
2. If your origin server is configured with 301/302 HTTP to HTTP redirection and follow 301/302 is enabled in the CDN Console, a 423 error may occur. We recommend you disable follow 301/302.
>!Note: if you use this method, we recommend you enable HTTPS configuration to force HTTPS redirection and change the origin-pull method to protocol follow. Otherwise, multiple redirects may occur. For the configuration steps, please see [HTTPS Acceleration Configuration Guide](https://intl.cloud.tencent.com/document/product/228/35213).

### What should I do if a 514 status code is returned in CDN?

This is caused by the IP access limit configured in the CDN Console as shown below:
![](https://main.qcloudimg.com/raw/6422e6288811635c64052ab8daa389fc.png)

>? 
> - IP access limit is designed to restrict the number of times an IP is allowed to access a node within one second. If the limit is exceeded, a 514 error will be returned.
> - Setting a low limit may affect the use of your business by normal high-frequency users. Therefore, please set a reasonable threshold. For more information, please see [IP Access Limit Configuration](https://intl.cloud.tencent.com/document/product/228/6420).

### What should I do if a 404 status code is returned by a CDN domain name?
Check the following:
1. Check whether the origin server can be accessed normally.
2. Check whether the origin server information and the origin domain have been modified in the CDN Console. This may have caused the 404 error during origin-pull.


### Does CDN support switching to non-origin-pull automatically and return the content cached on a node in case of origin server exception?
In case of origin server exception, if the cache on the CDN node accessed by the user request has not expired, the node will directly return the requested content to the client. If the cache has expired, it will not respond and an origin-pull request will be initiated.
