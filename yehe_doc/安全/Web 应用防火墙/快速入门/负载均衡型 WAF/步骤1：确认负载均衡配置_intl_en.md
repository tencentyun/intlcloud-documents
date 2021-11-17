
This document describes how to confirm your CLB configuration prior to accessing CLB WAF.
## Directions
By associating domain names with a CLB listener, CLB WAF checks and blocks HTTP or HTTPS traffic passing through the listener. Before accessing CLB WAF, make sure that your website business has been deployed on Tencent Cloud and used Tencent Cloud CLB (previously Application Load Balancer) over the public network.
>?We recommend using SaaS WAF for website business not deployed on Tencent Cloud.

To ensure traffic forwarding, it is necessary to configure your CLB instance and associating your domain name with a listener. For more details, see [Configuring an HTTP Listener](https://intl.cloud.tencent.com/document/product/214/32515) and [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).
This document takes `wow.qcloudwaf.com` as an example to illustrate how to check out the CLB listener configuration.
1. Log in to the [CLB Console](https://console.cloud.tencent.com/clb), and click **Instance Management** on the left sidebar.
2. Select a region and a CLB instance. Click **Configure Listener** on the right of the CLB instance to check its configuration.

3. Click **Listener Management** to view its configuration. As shown below, the listener name is `waftest` and the associated domain name is `wow.qcloudwaf.com` with WAF protection disabled.

## Subsequent Operations
After confirming your CLB configuration, you can proceed to the following steps:
- [Step 2. Bind Domain Name to CLB Instance](https://intl.cloud.tencent.com/document/product/627/34720)
- [Step 3. Verify the Configuration](https://intl.cloud.tencent.com/document/product/627/34721)
