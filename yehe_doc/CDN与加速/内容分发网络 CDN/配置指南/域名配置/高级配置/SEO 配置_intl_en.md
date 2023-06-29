## Overview
SEO configuration is a feature that solves the problem of incorrect weights for domain name searches due to frequent IP changes by CDN after a domain name is connected to CDN. By identifying whether an access IP belongs to a search engine, you can choose to directly pull the resource from the origin server, ensuring the stability of search engine weights.


> !
> - As search engine IPs are changed frequently, Tencent Cloud CDN can only guarantee that most but not all search engine IPs can be identified.
> - The SEO configuration feature is available only when the connected domain name is an [external origin](https://intl.cloud.tencent.com/document/product/228/6289). After this feature is enabled, if a domain name has multiple origin server addresses, the first one will be the default origin-pull address.
> - This feature is not supported in regions outside the Chinese mainland currently. If the acceleration region of your domain name is outside the Chinese mainland, this feature cannot be enabled. If your domain name is configured for global acceleration, the SEO configuration will take effect only within Chinese mainland.


## Directions

### Viewing the configuration

Log in to [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the sidebar, and click **Manage** on the right of a domain name to enter its configuration page. You will find the SEO configuration on the **Advanced Configuration** tab. It is disabled by default:
![](https://main.qcloudimg.com/raw/44f35a715f922cda12191d50e1cfc723.png)

### Modifying the configuration
You can toggle the switch to enable or disable SEO configuration:
![](https://main.qcloudimg.com/raw/8ea737dbd456397286f3ef8ff965aaf2.png)


