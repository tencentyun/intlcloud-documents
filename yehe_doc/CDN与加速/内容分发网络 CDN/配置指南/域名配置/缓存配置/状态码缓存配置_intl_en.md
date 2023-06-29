
## Configuration Overview
Normally, when a CDN node successfully pulls a requested resource from the origin server (with a 2XX status code returned), the node will process the resource based on the rules in the node cache validity configuration.
If the origin server is unable to process the non-2XX requests quickly, and you do not want all requests to be passed through to the origin server, you can configure the status code cache validity period. In this case, the CDN node will directly respond to non-2XX requests, helping reduce pressure on the origin server.
Currently supported status codes are as follows:
- 4XX: 400, 401, 403, 404, 405, 407, 414
- 5XX: 500, 501, 502, 503, 504, 509, 514

>! 
>- For now, some platforms only supports 404 and 403 codes. We will complete server upgrade as soon as possible.
>- Currently, only the status codes 404 and 403 are supported in regions outside the Chinese mainland. If the acceleration region of a domain name is "Global", then the status code cache rules except for 404 and 403 will only take effect in the Chinese mainland.


## Configuration Guide

### Viewing configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **Cache Configuration** tab to find the **Status Code Cache** section.
There is a default rule, which will cache 404 requests for 10 seconds.
![](https://main.qcloudimg.com/raw/508f716869f48fad3424fe6eeb77a67c.png)

### Adding rules
You can click **Add Rule** to add status code cache rules as needed.
<img src="https://main.qcloudimg.com/raw/3f01868799d0ddeda302e52e634bbde1.png" style="height:185px"/>

Configuration limitations
- Each status code can only have one unique rule.
- The cache time `0` means not to cache content.
