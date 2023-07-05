## Configuration Scenario
Tencent Cloud CDN uses the `Key-Value` format to map resources during caching, where `Key` is the cache key and a unique identifier of the cached resource.

When a user accesses the resource through a URL, the access request may carry some parameters for special purposes. For example, the following links are used to represent two different images:
```
http://cloud.tencent.com/1.jpg?version=1
http://cloud.tencent.com/1.jpg?version=2
```
In this scenario, you need to disable Ignore Query String and use a complete URL as the cache key to cache image contents and distinguish between resources.
In an audio/video scenario, if you use the timestamp signature parameter for access authentication:
```
http://cloud.tencent.com/1.mp4?sign=XXXXXX
```
In this scenario, you need to enable Ignore Query String and use the URL part before "?" (i.e., `http://cloud.tencent.com/1.mp4`) as the cache key. The node will then only cache one resource, and the cache can be directly hit through signature authentication even if the timestamp signature keeps changing.

## Configuration Guide

### Viewing configuration
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of the domain name to enter its configuration page. Under the **Access Control** tab, find the Ignore Query String configuration.

When you connect an acceleration domain name:
+ If static acceleration is selected, Ignore Query String will be disabled by default.
+ For download and streaming VOD acceleration, Ignore Query String is enabled by default.

![](https://main.qcloudimg.com/raw/df480521d6283b26e91e30faeb2fa8ce.png)

### Modifying configuration
You can switch to enable/disable Ignore Query String, and the configuration will take effect across the entire network in about 5 minutes:
![](https://main.qcloudimg.com/raw/cea0d30191547030521df32f70d88e67.png)

>
> + If your acceleration domain name is configured for global acceleration, the Ignore Query String configuration will take effect globally. This configuration does not distinguish between requests from and outside of Mainland China.
> + Enabling Ignore Query String can effectively improve cache hit rate.





