## Overview

If you worry about high fees incurred by high bandwidth or traffic usage due to hotlinking by malicious users, you can use the usage limit feature to control the usage.

When the bandwidth or traffic usage during a statistical period exceeds the configured alarm threshold, CDN will push a message notification to you; when the bandwidth cap is exceeded, you can disable CDN to avoid incurring more CDN service fees.

> !It will take about ten minutes for the usage limit configuration to take effect, during which the usage will be normally billed. For more information, see [Attack Prevention Solutions](https://intl.cloud.tencent.com/document/product/228/42355).

## Directions

### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. You will find the **Usage Limit Configuration** on the **Advanced Configuration** tab, which is disabled by default.
<img src="https://qcloudimg.tencent-cloud.cn/raw/2ddc0a57e196e3e1136b954ed46a88db.png" width="70%">

### Detailed configuration items

#### 1. Enabling the configuration

Toggle the switch on and configure the items:
<img src="https://qcloudimg.tencent-cloud.cn/raw/3806b3b7ea8cdf3f269536fd5fc22c16.png" width="60%">


- Statistic Type:
  - Instantaneous usage: It collects statistics on the traffic/bandwidth usage once every five minutes.
  - Cumulative usage: Compared with instantaneous usage, it supports a longer statistical period (every hour or calendar day).

> !Cumulative usage limit configuration is not supported for domain names with the acceleration type of dynamic content or dynamic & static content.

- Statistical Period: Per 5 minutes, per hour, or per day (before 24:00 of the day).

> !
> - A statistical period starts from 5 minutes before the configuration time:
>   For example, if the rule is configured during 09:05:01–09:09:59, the statistical period will start from 09:05:00.
> - If **Per hour** is selected as the statistical period, (1) the first statistical period will be less than one hour; (2) starting from the next statistical period, usage statistics will be collected once every hour.
>   For example, if the rule is configured at 09:23:10 on January 13, 2022, the first statistical period will be 9:20:00–9:59:59, and the next one will be 10:00:00–10:59:59.
> - If **Before 24:00 of the day** is selected as the statistical period, the statistical period will be 09:20:00–23:59:59 on January 13, 2022.

- Limit: Instantaneous usage supports both **Traffic** and **Bandwidth** options, while cumulative usage supports only **Traffic**.
  - Traffic: It collects statistics on the traffic usage of the domain name. The traffic limit is the maximum traffic for user access to the domain name.
  - Bandwidth: It collects statistics on the bandwidth usage of the domain name. The maximum bandwidth is the maximum bandwidth for user access to the domain name.
- Unblocking period: **Scheduled unblocking** and **Never unblock** are supported.
  - Scheduled unblocking: 60 minutes, 12 hours, 24 hours, or 3 days.
    For example, if the domain name `ex.com` is set to return 404 (CDN is disabled) after the limit is exceeded, and the automatic unblocking period is set to 60 minutes, then after the configured cumulative usage limit is exceeded, CDN will be disabled, and the acceleration domain name will be deactivated and will be automatically unblocked after 60 minutes.
  - Never unblock: If you worry that your domain name may be susceptible to high-traffic or high-bandwidth attacks, you can configure **Never unblock**. If the domain name is set to return 404 (CDN is disabled) after the limit is exceeded, then after the configured cumulative usage limit is exceeded, the domain name will be deactivated, and you should manually enable domain name acceleration in the console if needed.
- When cap is exceeded:
  - Return 404: After the cap is exceeded, CDN will be directly disabled for the domain name. In this case, you can go to the **Domain Management** page to activate the domain name again to resume the CDN service.
    **Note:** If the **Origin Type** is **COS Origin** or **Third-Party Object Storage Origin**, only **Return 404** (CDN is disabled) is supported. 
- Alarm Threshold:
  When the ratio of access bandwidth to traffic limit exceeds the configured percentage (only a multiple of 10 is supported, i.e., 10%–90%), CDN will push an alarm message.

> !
> - If the detected domain name bandwidth (traffic) exceeds the threshold, the **Return 404** configuration needs to be delivered node by node across the entire network; therefore, there will be a certain delay for the configuration to take effect.
> - If the alarm threshold is enabled, as the scan interval is five minutes, if the usage surges or the configured percentage value is large, it may happen that the alarm threshold is not triggered during the previous scan, and the bandwidth cap is directly reached during the next scan. In this case, CDN will send alarm notifications of the percentage and the bandwidth cap successively.

#### 2. Adding a region-specific configuration

If your acceleration domain name is configured for global acceleration and you want to configure different usage limits for acceleration in and outside the Chinese mainland, you can click **Add Special Configuration**.
![](https://qcloudimg.tencent-cloud.cn/raw/514910fe27000e0b742049d9d864632f.png)

> !
> - Currently, an added region-specific configuration can only be disabled but not deleted.
> - Region-specific configuration is not supported for domain names with the acceleration type of dynamic content or dynamic & static content.

#### Configuration examples

Suppose the domain name `cloud.tencent.com` is configured for global acceleration, and a region-specific usage limit configuration (for regions outside the Chinese mainland) is added as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/3dcecb342ba6c4bc7b44d80be6028839.png)

- Mutual independence of configurations for regions in and outside the Chinese mainland: If **Outside Chinese mainland** is selected for the region-specific configuration, the initial configuration will take effect in the Chinese mainland. After the traffic from the Chinese mainland reaches 4 GB during a statistical period (5 minutes), the 404 error will be returned for all requests from the Chinese mainland, without affecting the service outside the Chinese mainland; after the traffic from outside the Chinese mainland reaches 11 GB during a statistical period (before 24:00 of the day), the 404 error will be returned for all requests from outside the Chinese mainland, without affecting the service in the Chinese mainland.
- Acceleration region switch: If the acceleration region of a domain name is switched from global to Chinese mainland, the usage limit configuration for outside the Chinese mainland will be disabled by default and cannot be edited.

#### 3. Disabling the configuration

You can toggle off the usage limit feature. Then, even if there is existing configuration at the bottom, it will not take effect in the production environment. If you toggle the switch on, a message will be displayed asking you whether to enable this feature before the configuration takes effect across the entire network.
