

## Configuration Overview
Besides resources, Tencent Cloud CDN will also cache the following headers from the origin server and return them to users by default:
+ Access-Control-Allow-Origin
+ Timing-Allow-Origin
+ Content-Disposition
+ Accept-Ranges

If your origin server has special headers that need to be cached and returned to users by CDN, you can enable header cache.

## Configuration Guide
### Viewing the configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Cache Configuration** tab to find the **HTTP Header Cache Configuration** section. The configuration is enabled by default, and you can disable it as needed.
![](https://main.qcloudimg.com/raw/0fb4739f743b6242c463672a2f059098.png)





