

## Configuration Overview
With the Duplicate Configuration feature, you can duplicate configurations of an existing forwarding domain name to one or multiple new forwarding domain names. 

>!
>- This feature is not available for domain names that are disabled or blocked, having expired ICP filing (only for Chinese domain names), using external certificates, or with unsupported configurations varying across regions.
>- Backend configurations (i.e. configurations that not set up in the console) cannot be duplicated.


## Configuration Guide

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Duplicate Configuration** on the right of a domain name to enter its configuration page.
![](https://main.qcloudimg.com/raw/c9acd7ed82a3c675ec4369e294b2f94b.png)
Add a new forwarding domain name and submit it. The configurations of the current domain name will be duplicated to the new one.
![](https://main.qcloudimg.com/raw/4e8c4c4cf589118a97bd71c01f798890.png)

>?
>- The submitting process cannot be interrupted. You can manage the configuration after the new domain name is successfully added.
>- The configurations of a new domain name will be deployed to CDN nodes across the entire network, without affecting your running businesses. If you want to enable the acceleration service, you need to configure the CNAME. For configuration directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).
