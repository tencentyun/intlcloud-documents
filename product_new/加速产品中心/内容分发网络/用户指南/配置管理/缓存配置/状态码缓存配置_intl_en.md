
## Configuration Scenario
Normally, when a CDN node successfully pulls a requested resource from the origin server (with a 2XX status code returned), the node will process the resource based on the cache validity period configured in the cache rule.

If a non-2XX status code is returned, the 404 status code indicates caching for 10 seconds by default, while all other status codes indicate no caching. If the origin server cannot immediately process the non-2XX status code and you do not want that all requests pass through the origin server, you can configure the status code cache validity period so the CDN node will directly respond to non-2XX status code, helping reduce pressure on the origin server.

## Configuration Guide

### Viewing configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. Under the **Cache Configuration** tab, find the status code cache configuration.
![](https://main.qcloudimg.com/raw/508f716869f48fad3424fe6eeb77a67c.png)

### Modifying configuration
Currently, you can configure the cache validity period for the following status codes for exceptions:
+ 403
+ 404

To cancel the configuration and directly perform origin-pull, you can configure the cache validity period to 0 or delete the configuration entry.
![](https://main.qcloudimg.com/raw/3f01868799d0ddeda302e52e634bbde1.png)

>If your acceleration domain name is configured for global acceleration, the configured status cache validity period will take effect globally. This configuration does not distinguish between requests from and outside of Mainland China.

