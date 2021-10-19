
## Configuration Overview

Tencent Cloud CDN supports downstream speed limit configuration for setting the maximum downstream throughput speed over one single URL on the server.
The downstream speed limit configuration can control the peak bandwidth of CDN to a certain degree. It is frequently used in scenarios such as ecommerce promotions and new game version releases and updates.

>! After the downstream speed limit is configured, the user access experience and CDN acceleration effect will be affected. Therefore, please use it with caution.

## Configuration Guide

### Configuration limitations

- Maximum number of downstream speed limit rules: 10
- Unit: KB/s; value range: 1-1,000,000 (integers only)
- Supported rule types: all content, specified file type, specified folder, and specified file. Regular matching is currently not supported.
- Rules are executed from bottom to top. Rules at the bottom have higher priority.

### Configuration instructions

Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), select **Domain Management** on the left sidebar, and then click **Manage** on the right of a domain name to enter its configuration page. Select **Access Control** tab to find the downstream speed limit configuration, which is disabled by default:
![](https://main.qcloudimg.com/raw/c9ea85be753b60096b8088b048ac626a.png)
Click **Add Speed Limit Rule** to configure a rule:
![](https://main.qcloudimg.com/raw/02e033c829da553acc5eeb9bca864528.png)
The overall configuration will be disabled after a rule is added, so the ongoing services will not be affected:
![](https://main.qcloudimg.com/raw/e0006ace8527cc13c381666b22f21790.png)
You can toggle the switch on to deploy the configured speed limit rule to the nodes over the entire CDN network:
![](https://main.qcloudimg.com/raw/4b9685cb889210accb67d11f1b389ae8.png)

## Configuration Samples

The downstream speed limit configuration of `cloud.tencent.com` is as follows:
![](https://main.qcloudimg.com/raw/7ee9a5167aa054c8e99c15267e38eba3.png)
If a user accesses the resource `http://cloud.tencent.com/test.mp4`, the server will return the content at the configured downstream speed of 200 KB/s.
If a user accesses the resource `http://cloud.tencent.com/test.flv`, the server will return the content at the configured downstream speed of 400 KB/s.
