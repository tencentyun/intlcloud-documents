
## Problem Description

My website is still slow after it’s connected to Tencent Cloud CDN.

## Possible Reasons

- 1. You have not configured a CNAME record for the connected domain name at a DNS service provider, so the CDN acceleration service for the domain name is not in effect. Please [check DNS](#step1).
- 2. The node cache validity is not configured properly. Please [check the node cache validity configuration](#step2).
- 3. The resource URL is accessed for the first time after CDN activation, and it has not been prefetched before. Please [prefetch the URL](#step3).
- 4. The website architecture has defects. Please [optimize the website architecture](#step4).



## Solutions

[](id:step1)
### Check DNS
This example shows you how to run `nslookup` to check the DNS record of a CDN acceleration domain name:
```
Run `nslookup` for the acceleration domain name
```
![](https://main.qcloudimg.com/raw/e60f03d058f29134524166c211791568.png)
If the result domain name is not suffixed with `dnsv1.com` as shown above, then the CDN acceleration service for your domain name is not in effect. Please check the CNAME record of the domain name at the DNS service provider as instructed in [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

[](id:step2)
###  Check the node cache validity configuration
Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page, and switch to the **Cache Configuration** tab to find the **Node Cache Validity Configuration** section.
![](https://main.qcloudimg.com/raw/7722e07d356878b4e031984df0328759.png)

- Check the node cache rules of the resource: whether the validity is "0", too short, or is configured as "No Cache".
  Access requests will be forwarded to the origin server if the request resources are not cached on nodes, in which case the acceleration is not effective. Please configure the cache validity as required by your business.
- Check whether the header `Cache-Control` is set as `no-store/no-cache/private` for your origin server.
  - If it is, you need to enable **Force Cache** for the CDN nodes to cache resources as configured.
  - If **Force Cache** is not enabled and the header is configured as so, CDN nodes will not cache resources even the cache validity is configured.

For more configuration rules, please see [Node Cache Validity Configuration (New)](https://intl.cloud.tencent.com/document/product/228/38424).

[](id:step3)
### Prefetch the URL

It is normal that the speed is slow when accessing a resource for the first time which has not been prefetched before. Please log in to the [CDN console](https://console.cloud.tencent.com/cdn), click **Purge and Prefetch** on the left sidebar, and then submit the URL for prefetch. For more information, please see [Prefetch Cache](https://intl.cloud.tencent.com/document/product/228/39000).
![](https://main.qcloudimg.com/raw/83e7ceeb26fca38870fe020231542988.png)

[](id:step4)
### Optimize the website architecture

Requests for dynamic resources are always forwarded to the origin server to pull the latest resources, slowing the access speed. If your website has many dynamic resources, we recommend separating them from static resources and using CDN for your static resources only.
