

## Overview

Tencent Cloud CDN supports downstream speed limit configuration for setting the maximum downstream throughput speed over one single URL on the server.
The downstream speed limit configuration can control the peak bandwidth of CDN to a certain degree. It is frequently used in scenarios such as ecommerce promotions and new game version releases and updates.

>! The downstream speed limit configuration takes effect globally for all users who access the domain name. After the downstream speed limit is configured, the user access experience and CDN acceleration effect may be affected. Therefore, configure the downstream speed limit with caution.

## Directions


### Viewing the configuration

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and click **Manage** on the right of a domain name to enter its configuration page. Open the **Access Control** tab to find the **Downstream Speed Limit Configuration** section. The **Downstream Speed Limit** switch is toggled off by default.
![](https://main.qcloudimg.com/raw/c9ea85be753b60096b8088b048ac626a.png)

### Adding rules
Click **Add Speed Limit Rule** to configure a rule:
![](https://main.qcloudimg.com/raw/02e033c829da553acc5eeb9bca864528.png)

#### Configuration limitations

- Maximum number of downstream speed limit rules: 10
- Unit: KB/s; value range: 1-1,000,000 (integers only)
- Supported rule types: all content, specified file type, specified folder, and specified file. Regular matching is currently not supported.
- Rules are executed from bottom to top. Rules at the bottom have higher priority.


## Configuration Samples

The downstream speed limit configuration of `cloud.tencent.com` is as follows:
![](https://qcloudimg.tencent-cloud.cn/raw/814d50bbc8ca84e86bb5ac8c36dffc15.png)
If a user accesses the resource `http://cloud.tencent.com/test.mp4`, the server will return the content at the configured downstream speed of 200 KB/s.
If a user accesses the resource `http://cloud.tencent.com/test.flv`, the server will return the content at the configured downstream speed of 400 KB/s.
