SEO optimization configuration is a feature that solves the problem with incorrect weights of domain name search results due to frequent IP changes by CDN after a domain name is connected to CDN. By identifying whether an access IP belongs to a search engine, you can choose to directly pull the resource from the origin server, ensuring the stability of search engine weight.
> As search engine IPs are updated very frequently, Tencent Cloud CDN can only guarantee that most but not all search engine IPs can be identified.

## Configuration Guide
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar to enter the management page. Find the desired domain name and click **Manage** in the "Operation" column.
![img](https://main.qcloudimg.com/raw/99e0c24b4530c30b9abe27325bb1b317.png)
2. Click **Advanced Configuration** and you can see the **SEO Optimization** module. Automatic origin-pull for search engine is disabled by default.
> The SEO optimization configuration feature is available only when the connected domain name is your **own**. After this feature is enabled, if a domain name has multiple origin server addresses, the first one will be the default origin-pull address.
>
![img](https://main.qcloudimg.com/raw/cd67f24a23eb2241ff4a35ab27777c6c.png)
