## Configuration Overview

For businesses that have been connected to Tencent Cloud CDN, you can view information such as domain name creation time, corresponding CNAME domain name, service region, project, service type, and supported protocols on the basic information module of the domain name. You can also modify information such as service region, service type, and project as needed.

## Configuration Guide

### Viewing basic information

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page. The domain name basic information is in the **Basic Configuration** tab.
![](https://main.qcloudimg.com/raw/2273c600e31b35d12b9480ff74205962.png)

>? The former **Internet Protocol** is now the **IPv6 Access**. If the Internet protocol of an existing domain name is **IPv4** and **IPv6**, then the IPv6 access will be automatically enabled.

### Modifying basic information

#### 1. Modify project

For domain name project modification, you can click **Modify** on the right of the project. Project modification will change the project-based statistics and sub-user permissions, please operate with caution.

> ?To create a project or manage existing projects, go to the [Project Management](https://console.cloud.tencent.com/project) page.

![](https://main.qcloudimg.com/raw/bb56a7b51526f256ccd5d98169861e98.png)


#### 2. Modify domain name service region

**Definition of the domain name service region**:

- If a domain name is configured for global acceleration, requests will be scheduled to the nearest global CDN cache node. In general, nodes in and outside the Chinese mainland serve users in and outside the Chinese mainland respectively.
- If a domain name is configured for acceleration in the Chinese mainland, access requests from global users will be served by cache nodes in the Chinese mainland.
- If a domain name is configured for acceleration outside the Chinese mainland, access requests from global users will be served by cache nodes outside the Chinese mainland.

You can click **Modify** on the right of the service region to modify it:
![](https://main.qcloudimg.com/raw/bf59e0eccd001b5ccad6262063f032db.png)

> ! Acceleration services in and outside the Chinese mainland are billed separately at different prices. For more information, please see [Billing Instruction](https://intl.cloud.tencent.com/document/product/228/2949).

#### 3. Modify service type

Tencent Cloud CDN optimizes acceleration performance based on the service type. For the best acceleration result, we recommend selecting the service type similar to that of your actual businesses. If you want to adjust it, click **Modify** on the right:
![](https://main.qcloudimg.com/raw/56f3da131520a9c9efa6c92da94dee25.png)

> !
>
> - Modifying service type will change the underlying CDN acceleration platform, which may cause a small number of failed requests and increase origin-pull bandwidth. We recommend modifying service type during off-peak hours.
> - If you cannot find the **Modify** button next to your domain name, please [contact us](https://intl.cloud.tencent.com/contact-sales) for assistance.

#### 4. Modify IPv6 access
Toggle the IPv6 access switch to enable or disable the feature. If it is enabled, CDN nodes can be accessed through IPv6 protocol.

>! 
>- IPv6 access is only supported in the Chinese mainland, so the feature cannot be enabled for the acceleration domain names outside the Chinese mainland. For global acceleration domain names, IPv6 access will only take effect in the Chinese mainland if the feature is enabled.
>- For a global acceleration domain name with the IPv6 access enabled, if its acceleration region is switched to the region outside the Chinese mainland, the IPv6 access feature will be automatically disabled and cannot be enabled.
>- IPv6 is currently not supported for streaming VOD acceleration. 
>- Some platforms are being upgraded or have special configurations, so IPv6 access is currently not supported.
