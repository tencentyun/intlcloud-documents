## Configuration Overview

For businesses that have been connected to Tencent Cloud CDN, you can view information such as domain name creation time, corresponding CNAME domain name, acceleration region, project, service type, and supported protocols on the basic information module of the domain name. You can also modify information such as acceleration region, service type, and project as needed.

## Configuration Guide

### Viewing basic information

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, click **Manage** on the right of a domain name to enter its configuration page. The domain name basic information is in the **Basic Configuration** tab.
![](https://main.qcloudimg.com/raw/5b6d2f8572ba022c5a18bb787953b1d0.png)



### Modifying domain name acceleration region

Click **Modify** on the right of the acceleration region to change it.
- If a domain name is configured for global acceleration, requests will be scheduled to the nearest global CDN cache node. In general, nodes in and outside the Chinese mainland serve users in and outside the Chinese mainland respectively.
- If a domain name is configured for acceleration in the Chinese mainland, access requests from global users will be served by cache nodes in the Chinese mainland.
- If a domain name is configured for acceleration outside the Chinese mainland, access requests from global users will be served by cache nodes outside the Chinese mainland.



> ! Acceleration services in and outside the Chinese mainland are billed separately at different prices. For more information, please [click here](https://intl.cloud.tencent.com/document/product/228/2949).


### Modifying project

Click **Modify** on the right of the domain name project to change it.


> !
> - Please note that project modification will change the project-based statistics and sub-user permissions. Please modify with caution.
> - To create a project or manage existing projects, go to the [Project Management](https://console.cloud.tencent.com/project) page.






### Modifying service type

Tencent Cloud CDN optimizes acceleration performance based on the service type. For the best acceleration result, we recommend selecting the service type similar to that of your actual businesses. If you want to adjust it, click **Modify** on the right:


> !
> - Modifying service type will change the underlying CDN acceleration platform, which may cause a small number of failed requests and increase origin-pull bandwidth. We recommend modifying service type during off-peak hours.
> - If you cannot find the **Modify** button next to your domain name, please [contact us](https://intl.cloud.tencent.com/zh/contact-sales) for assistance.

### Modifying IPv6 access
Toggle the IPv6 access switch to enable or disable it. CDN nodes can be accessed over IPv6 protocol after IPv6 access is enabled.

>! 
>- Some platforms are being upgraded, IPv6 access is currently not supported. Please stay tuned for the official launch.
>- IPv6 access is only available in the Chinese mainland. For global acceleration domain names, if IPv6 access is enabled, it will take effect only in the Chinese mainland. For domain names with acceleration outside the Chinese mainland, it cannot be enabled.
>- For global acceleration domain names with IPv6 access enabled, if the acceleration region is switched to the regions outside the Chinese mainland, IPv6 access will be disabled automatically and cannot be enabled.


