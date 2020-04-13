
## Configuration Scenario
Besides resources, Tencent Cloud CDN will also cache the following headers from the origin server and return them to users by default:
+ Access-Control-Allow-Origin
+ Timing-Allow-Origin
+ Content-Disposition
+ Accept-Ranges

If your origin server has special headers that need to be cached in and returned to users by CDN, you can enable header cache.

## Configuration Guide
### Viewing configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. Under the **Cache Configuration** tab, find the HTTP header cache configuration, which is disabled by default.
![](https://main.qcloudimg.com/raw/0fb4739f743b6242c463672a2f059098.png)

### Modifying configuration
You can directly switch to enable/disable HTTP header cache, and the configuration will take effect across the entire network in about 5 minutes:
![](https://main.qcloudimg.com/raw/72128b6740c489912a6957a306ac8f1f.png)

>
> + If your acceleration domain name is configured for global acceleration, the header cache configuration will take effect globally. This configuration does not distinguish between requests from and outside of Mainland China.
> + The header cache configuration is being upgraded across the entire network. If an error message is displayed when you disable it, it may be caused by the upgrade. Please [contact us](https://cloud.tencent.com/act/event/connect-service) to disable it on the backend.





