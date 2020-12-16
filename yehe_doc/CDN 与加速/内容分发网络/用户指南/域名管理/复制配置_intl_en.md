

## Configuration Overview
With the copy configuration feature, the configurations of an existing acceleration domain name can be copied to one or multiple new acceleration domain names. The feature allows you to quickly and easily connect new domain names without configuring them one by one.

>!
>- The copy configuration feature is not supported for domain names that are disabled or blocked, having expired ICP filing or self-owned certificates, or with unsupported existing configurations varying across regions.
>- If the original domain name has special configurations on the backend (instead of the console), the special configurations cannot be copied.


## Configuration Guide

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Copy Configuration** on the right of a domain name to enter its configuration page.
![](https://main.qcloudimg.com/raw/c9acd7ed82a3c675ec4369e294b2f94b.png)
You can add a new acceleration domain name. Once the new domain name is submitted, the configurations of the current domain name can be copied to the new domain name.
![](https://main.qcloudimg.com/raw/4e8c4c4cf589118a97bd71c01f798890.png)

>?
>- The submitting process cannot be interrupted. You can manage the configuration after the new domain name is successfully added.
>- The configurations of a new domain name will be deployed to CDN nodes across the entire network, not affecting your current businesses. If you want to enable the acceleration service, you need to configure the CNAME. For configuration directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).
