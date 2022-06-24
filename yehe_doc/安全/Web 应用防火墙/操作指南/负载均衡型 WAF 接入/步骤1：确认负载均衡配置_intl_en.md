This document describes how to confirm your CLB configuration prior to accessing CLB WAF.

## Directions
By associating domain names with a CLB listener, CLB WAF checks and blocks HTTP or HTTPS traffic passing through the listener. Before accessing CLB WAF, make sure that your website business has been deployed on Tencent Cloud and used Tencent Cloud CLB (previously Application Load Balancer) over the public network.
>?We recommend using SaaS WAF for website business not deployed on Tencent Cloud.

To ensure traffic forwarding, it is necessary to configure your CLB instance and associating your domain name with a listener. For more details, see [Configuring an HTTP Listener](https://intl.cloud.tencent.com/document/product/214/32515) and [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).
Perform the following steps to view the CLB listener configuration. `clb.technicalsupport.cn` is used as an example.
1. Log in to the [CLB console](https://console.cloud.tencent.com/clb), and click **Instance Management** on the left sidebar.
2. Select a region and CLB instance. Click **Configure listener** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/8e1bf53c9374320e5cb964da31efdfa9.png)

3. On the page displayed, click **Listener Management** to view the listener configuration details. In this example, the listener name is `waftest`, and the domain name is `clb.technicalsupport.cn` and is in "Not Enabled" status.
![](https://qcloudimg.tencent-cloud.cn/raw/3630634f3449e2df0878e57d27483f87.png)

## Subsequent Operations
After confirming your CLB configuration, you can proceed to the following steps:
- [Step 2. Bind Domain Name to CLB Instance](https://intl.cloud.tencent.com/document/product/627/34720)
- [Step 3. Verify the Configuration](https://intl.cloud.tencent.com/document/product/627/34721)
